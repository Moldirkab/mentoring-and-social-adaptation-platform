# Technology Comparison and Selection

## 1. Introduction

The Mentoring and Social Adaptation Platform is designed to support children living in orphanages, boarding-school graduates transitioning to independent life, mentors, coordinators, and administrators. The platform will provide mentor–mentee recommendations, mentor verification, meeting management, life-skills goals, progress tracking, communication, and coordinator monitoring.

The purpose of this technology comparison is to evaluate alternative technologies and justify the proposed technical decisions according to the project's functional requirements, security needs, maintainability, and implementation constraints.

The team has selected a microservices architecture consisting of five business services. The selected technologies remain proposed decisions and will be verified through implementation and testing.

## 2. Architecture Style Comparison

Three architectural approaches were considered: a monolithic application, a modular monolith, and microservices.

| Criteria                                       | Monolithic Application               | Modular Monolith        | Microservices                      |
| ---------------------------------------------- | ------------------------------------ | ----------------------- | ---------------------------------- |
| Initial implementation                         | Simple                               | Relatively simple       | More complex                       |
| Separation of responsibilities                 | Limited without additional structure | Clear internal modules  | Independently deployable services  |
| Independent deployment                         | No                                   | No                      | Yes                                |
| Independent scaling                            | Limited                              | Limited                 | Supported per service              |
| Fault isolation                                | Limited                              | Limited                 | Better when failures are contained |
| Inter-service communication                    | Internal function calls              | Internal function calls | Network communication              |
| Development and operational overhead           | Low                                  | Low to medium           | High                               |
| Suitability for independent AI-service scaling | Limited                              | Limited                 | Strong                             |

**Selected approach: Microservices.**

Microservices are selected to separate the platform's main business capabilities, particularly AI-assisted matching, identity management, mentoring workflows, and communication. This architecture allows services to be developed and deployed independently and provides a foundation for scaling computationally intensive matching operations separately.

However, microservices introduce additional complexity in deployment, monitoring, data consistency, and communication. The team will address these challenges using Docker Compose, defined service interfaces, automated tests, and clear data ownership.

### 2.1 Proposed Microservices

| Service                           | Main responsibilities                                                                                                                    | Data ownership                                                                                                                 |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Identity & Access Service         | Registration, login, roles, permissions, tokens, and consent management                                                                  | Accounts, roles, organisations, consents, and refresh tokens                                                                   |
| Profile & Core Management Service | Mentor and mentee profiles, preferences, mentor applications, document metadata, and mentor verification                                 | Profiles, preferences, applications, and document metadata                                                                     |
| AI Matching Service               | Eligibility filtering, sentence embeddings, weighted compatibility scoring, optional LLM reranking, and ranked recommendations           | Matching configuration, pseudonymised profile representations, embeddings, and recommendation logs, if persistence is required |
| Mentoring & Progress Service      | Coordinator-approved matches, meeting scheduling, meeting notes, life-skills goals, milestones, progress tracking, and inactivity alerts | Matches, meetings, notes, goals, milestones, and progress records                                                              |
| Communication & Signaling Service | Real-time messaging, notifications, reporting problems, video-call integration, and communication-related records                        | Messages, notifications, delivery status, and video-call metadata                                                              |

The API Gateway, RabbitMQ, PostgreSQL, and MinIO are supporting infrastructure rather than additional business microservices.

## 3. Backend Platform Comparison

Three backend technologies were considered: Python with FastAPI, Python with Django REST Framework, and Node.js with NestJS.

| Criteria                                               | FastAPI                      | Django REST Framework                          | NestJS                                                       |
| ------------------------------------------------------ | ---------------------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| Development of REST APIs                               | Strong                       | Strong                                         | Strong                                                       |
| Python machine-learning ecosystem                      | Excellent                    | Excellent                                      | Requires integration with Python-based ML components         |
| Asynchronous request handling                          | Strong                       | Supported, depending on components used        | Strong                                                       |
| API documentation                                      | Automatic OpenAPI generation | Requires configuration or additional libraries | Supported through Swagger integration                        |
| Built-in administration                                | No built-in admin interface  | Strong built-in Django administration          | No built-in admin interface                                  |
| Suitability for small independent services             | Strong                       | Good                                           | Strong                                                       |
| Integration with sentence embeddings and LLM libraries | Direct Python integration    | Direct Python integration                      | Usually requires an additional Python service or integration |

**Selected technology: Python 3.12 with FastAPI.**

FastAPI is selected because it supports API development, asynchronous operations, request validation, and automatic OpenAPI documentation. Python also provides the ecosystem required for sentence embeddings, AI-assisted matching, and recommendation evaluation.

SQLAlchemy 2 will be used for database access, Alembic for schema migrations, Pydantic for data validation, and pytest for automated testing. Internal gRPC endpoints will be implemented using the Python gRPC libraries and Protocol Buffers where synchronous inter-service communication is required.

Django REST Framework remains a reasonable alternative, particularly if the project requires a built-in administration interface. NestJS is also suitable for microservices, but using Python for the backend keeps the matching logic and the rest of the services within the same primary language.

## 4. Database and Vector Search Comparison

Three storage approaches were considered: PostgreSQL with pgvector, MySQL, and MongoDB.

| Criteria                                                    | PostgreSQL + pgvector      | MySQL                                                             | MongoDB                                                        |
| ----------------------------------------------------------- | -------------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------- |
| Structured relational data                                  | Strong                     | Strong                                                            | Requires a document-oriented data model                        |
| Transactions and referential integrity                      | Strong                     | Strong                                                            | Supported, with different modeling considerations              |
| Complex joins and reporting                                 | Strong                     | Strong                                                            | Often requires additional aggregation or application logic     |
| Vector similarity search                                    | Supported through pgvector | Depends on available vector-search capabilities and configuration | Depends on the selected edition and vector-search capabilities |
| Flexible profile attributes                                 | JSONB support              | JSON support                                                      | Flexible document structure                                    |
| Suitability for mentoring relationships and meeting records | Strong                     | Strong                                                            | Possible, with different relationship modeling                 |
| One storage platform for relational data and embeddings     | Yes                        | Depends on the selected configuration                             | Depends on the selected configuration                          |

**Selected technology: PostgreSQL with pgvector.**

PostgreSQL is suitable for storing accounts, profiles, mentoring relationships, meetings, goals, and progress records. These entities have structured relationships and require consistent updates.

The pgvector extension supports storing embeddings and performing vector similarity searches alongside relational data. This is useful for comparing mentee goals with mentor experience without introducing a separate vector database in the initial implementation.

Each microservice will own its data and use separate database credentials. During development, the service databases can run on one PostgreSQL server through Docker Compose, while remaining logically separated. Services must not directly read or modify another service's database.

MinIO will be used for documents and attachments rather than storing file contents in relational tables. Redis is optional and will only be added if performance testing demonstrates a need for caching or coordinating WebSocket connections.

## 5. Component Communication Comparison

Three communication approaches were considered: REST-only communication, gRPC-based communication, and a hybrid architecture using REST, gRPC, RabbitMQ, and WebSockets.

| Criteria                                  | REST Only                               | gRPC for Internal Calls                                                  | Hybrid Communication                                    |
| ----------------------------------------- | --------------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------- |
| Browser compatibility                     | Excellent                               | Requires gRPC-Web or an additional gateway configuration for browser use | REST is used for browser requests                       |
| Typed service contracts                   | OpenAPI schemas                         | Protocol Buffers and generated clients                                   | OpenAPI and Protocol Buffers                            |
| Synchronous service calls                 | Supported                               | Supported                                                                | gRPC for selected internal calls                        |
| Asynchronous domain events                | Requires additional technology          | Requires additional technology                                           | RabbitMQ                                                |
| Real-time browser messaging               | Requires WebSockets for persistent chat | Does not replace WebSockets for browser chat                             | WebSockets                                              |
| Implementation complexity                 | Low                                     | Medium                                                                   | Higher                                                  |
| Suitability for the proposed architecture | Good                                    | Good for selected internal calls                                         | Strong, with greater setup and maintenance requirements |

**Selected approach: Hybrid communication.**

The platform will use different communication methods for different purposes.

- **REST over HTTPS with JSON:** frontend-to-backend requests through Traefik, including login, profile management, coordinator dashboards, and match approval.
- **gRPC with Protocol Buffers:** synchronous communication between internal Python services where a typed service contract is useful.
- **RabbitMQ:** asynchronous domain events, such as notifying participants after a match is approved or alerting a coordinator after a complaint is submitted.
- **WebSockets:** real-time chat between authorized participants.

For example, the AI Matching Service can use gRPC to request the eligible, approved mentor data it needs from the Profile & Core Management Service. The Mentoring & Progress Service can publish an event after a coordinator approves a match, allowing the Communication & Signaling Service to send notifications asynchronously.

The AI Matching Service will only generate recommendations. It will not create or approve mentoring pairs. The Mentoring & Progress Service remains responsible for recording approved matches.

All direct service calls must use appropriate authentication, authorization, timeouts, and error handling. RabbitMQ consumers must handle duplicate event delivery safely. The need for gRPC will be evaluated through implementation and testing, but it is part of the proposed initial architecture.

## 6. Deployment and API Gateway Comparison

Three deployment approaches were considered: Docker Compose with Traefik, Kubernetes, and managed application hosting.

| Criteria                           | Docker Compose + Traefik          | Kubernetes                                | Managed Application Platform          |
| ---------------------------------- | --------------------------------- | ----------------------------------------- | ------------------------------------- |
| Local development                  | Simple, repeatable environment    | Requires additional cluster setup         | Depends on the provider               |
| Microservice deployment            | Separate containers               | Independent deployments and orchestration | Depends on the provider               |
| API routing                        | Traefik reverse proxy and routing | Ingress or gateway configuration          | Usually provider-dependent            |
| Network configuration              | Docker networks                   | Cluster networking and network policies   | Depends on available controls         |
| Operational complexity             | Low to medium                     | High                                      | Low to medium                         |
| Suitability for a university pilot | Strong                            | Potentially excessive                     | Depends on pricing and service limits |

**Selected approach: Docker Compose with Traefik.**

Docker Compose will provide a repeatable environment for running the frontend, microservices, PostgreSQL, RabbitMQ, and supporting infrastructure. Traefik will act as the API Gateway, routing external requests to the appropriate backend endpoints.

Only intended public entry points will be exposed. Internal service endpoints and supporting infrastructure should remain on appropriately restricted Docker networks. TLS, access controls, and rate limits will be configured according to the deployment environment.

Kubernetes may be considered in a future deployment if the system's operational needs justify its additional complexity.

## 7. Frontend Framework Comparison

Three frontend frameworks were considered: React, Vue, and Angular.

| Criteria                                     | React                       | Vue                    | Angular                                     |
| -------------------------------------------- | --------------------------- | ---------------------- | ------------------------------------------- |
| Component-based interface development        | Strong                      | Strong                 | Strong                                      |
| TypeScript support                           | Strong                      | Strong                 | Strong                                      |
| Suitability for a responsive web application | Strong                      | Strong                 | Strong                                      |
| Ecosystem and community resources            | Extensive                   | Extensive              | Extensive                                   |
| Integration with generated API clients       | Supported                   | Supported              | Supported                                   |
| Project implementation complexity            | Depends on chosen libraries | Generally approachable | More structured but comparatively extensive |

**Selected technology: React with TypeScript and Vite.**

React is selected for building the responsive web interface for mentees, mentors, coordinators, and administrators. TypeScript provides static type checking, while Vite provides the development and build tooling.

The frontend will communicate with backend services through the API Gateway rather than accessing individual service databases or internal endpoints.

## 8. Security and Maintainability

The platform handles personal information about minors and vulnerable young people. Security and access control are therefore core architectural requirements.

The proposed design includes:

- Authentication and role-based authorization.
- Verification of mentors before they can be recommended or matched.
- Coordinator approval of all final mentor–mentee matches.
- Restricted access to sensitive information and service-owned databases.
- Pseudonymisation of matching inputs and exclusion of unnecessary identifying information from AI requests.
- Secure storage of uploaded documents and attachments.
- Audit records for sensitive administrative and moderation actions.
- Timeouts, error handling, and failure-isolation measures for inter-service communication.
- Automated unit, integration, contract, and end-to-end testing.

Each service will validate permissions for its own operations. The API Gateway provides a common entry point but does not replace service-level authorization.

The AI Matching Service will not have credentials to create or approve pairs. A coordinator will retain the final decision-making authority, and recommendation scores will be treated as indicators of compatibility rather than guarantees of a successful mentoring relationship.

## 9. Final Technology Selection

| Layer                                        | Selected technology                                         |
| -------------------------------------------- | ----------------------------------------------------------- |
| Architecture                                 | Five-microservice architecture                              |
| Frontend                                     | React, TypeScript, and Vite                                 |
| Backend                                      | Python 3.12 and FastAPI                                     |
| Internal synchronous communication           | gRPC with Protocol Buffers for selected service calls       |
| Frontend-to-backend communication            | REST over HTTPS with JSON                                   |
| Asynchronous communication                   | RabbitMQ                                                    |
| Real-time chat                               | WebSockets                                                  |
| Data storage                                 | PostgreSQL with pgvector                                    |
| Database access and migrations               | SQLAlchemy 2 and Alembic                                    |
| API Gateway                                  | Traefik                                                     |
| Containerization and local orchestration     | Docker Compose                                              |
| File and attachment storage                  | MinIO                                                       |
| Optional caching and connection coordination | Redis, only if needed                                       |
| Automated testing                            | pytest, HTTPX, service contract tests, and end-to-end tests |

This stack is intended to support independent service development, AI-assisted matching, structured data management, and secure coordination of mentoring relationships.

## 10. Verification Plan

The selected technologies and architectural decisions will be checked through implementation and testing rather than assumed to satisfy the requirements automatically.

| Decision                      | Verification                                                                                                                                              |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Microservices architecture    | Demonstrate that individual services can be started, tested, and redeployed independently.                                                                |
| FastAPI and service contracts | Test API validation, generated OpenAPI documentation, gRPC contracts, and error handling.                                                                 |
| gRPC communication            | Test successful requests, timeouts, authentication, and behavior when a dependent service is unavailable.                                                 |
| RabbitMQ                      | Test event delivery, retry behavior, and duplicate-event handling.                                                                                        |
| PostgreSQL and pgvector       | Test relational integrity, vector similarity searches, data isolation, and database backup and restoration.                                               |
| Traefik and Docker Compose    | Verify that the platform can be started using documented instructions and that only intended endpoints are publicly accessible.                           |
| Security and privacy          | Test role-based permissions, cross-user access restrictions, mentor-approval rules, and protection of sensitive information.                              |
| Performance                   | Use representative test data and load testing to measure response times and determine whether the matching service satisfies defined performance targets. |

Any numerical performance targets will be taken from the project requirements and verified through testing.

## 11. Conclusion

The proposed technology stack combines a microservices architecture with FastAPI, PostgreSQL and pgvector, gRPC, REST APIs, RabbitMQ, WebSockets, Traefik, and Docker Compose. These choices provide a basis for separating business responsibilities, implementing AI-assisted mentor recommendations, maintaining structured data, and supporting communication between platform participants.

The approach introduces additional operational and testing complexity compared with a monolithic application. The team will manage this complexity through limited service boundaries, clear data ownership, documented communication contracts, and progressive verification.

The final architecture and technology choices will be refined according to implementation results, measurable requirements, and supervisor feedback.
