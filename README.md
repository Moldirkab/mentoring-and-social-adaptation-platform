# Mentoring and Social Adaptation Platform

A web-based platform designed to connect young people from residential care with screened mentors and support their transition to independent living.

**Academic institution:** Astana IT University (AITU)  
**Project supervisor:** Salkenov Aldiyar

## GitHub Repository

**Repository:** https://github.com/Moldirkab/mentoring-and-social-adaptation-platform

**YouTrack Project:** [https://mentorship-platform.youtrack.cloud](https://mentorship-platform.youtrack.cloud/)

## Project Overview

Young people living in residential care and graduates transitioning to independent living may face challenges related to social integration, education, employment, housing, and access to reliable guidance.

The Mentoring and Social Adaptation Platform aims to provide an integrated digital environment for mentor applications, coordinator-supervised matching, communication, meetings, life-skills goals, and progress monitoring.

## Problem Statement

Access to consistent mentorship and practical social adaptation support can be difficult to coordinate. Organisations need ways to manage mentor applications, identify suitable matches, monitor mentoring relationships, and respond to reported problems.

The project addresses these needs through a web-based platform that brings mentoring workflows and social adaptation resources together.

## Project Aim

To develop a web-based mentoring and social adaptation platform that facilitates mentor–mentee connections and supports young people transitioning toward independent living.

## Target Users

- **Mentees:** Young people aged 14–17 living in residential care and graduates aged 18–23 transitioning to independent living.
- **Mentors:** Screened adult volunteers aged 18 or older who provide guidance and support.
- **Coordinators:** NGO or residential-care staff who verify mentors, approve matches, handle complaints, and monitor progress.
- **Administrators:** Users responsible for managing platform accounts, organisations, roles, and settings.

Accounts for minors must be created by a coordinator after the required consent is recorded. Mentors must be approved before they can be matched.

## Planned Features

- User authentication and role-based access control.
- Mentor applications, document verification, and coordinator approval.
- AI-assisted mentor recommendations based on compatibility criteria.
- Coordinator-controlled mentor–mentee matching.
- Supervised communication and problem reporting.
- Meeting scheduling, meeting notes, and feedback.
- Personalized life-skills goals and progress tracking.
- Notifications and coordinator monitoring, including inactivity alerts.

**Human oversight:** AI recommendations are advisory only. Coordinators retain final authority over mentor–mentee matching decisions.

## Planned Architecture

The production system is planned as five independently deployable microservices.

| Microservice | Responsibilities |
|---|---|
| **Identity & Access** | Authentication, roles, permissions, and consent management |
| **Profile & Core Management** | Mentor and mentee profiles, applications, and mentor verification |
| **AI Matching** | Eligibility filtering, sentence embeddings, weighted compatibility scoring, and recommendations |
| **Mentoring & Progress** | Approved matches, meetings, goals, skill tracks, and coordinator monitoring |
| **Communication & Safety** | Messaging, notifications, complaints, and moderation |

### Inter-Service Communication

- **REST over HTTPS:** Frontend-to-backend requests through the API Gateway.
- **gRPC with Protocol Buffers:** Synchronous communication between internal services.
- **RabbitMQ:** Asynchronous events and background processing.
- **WebSockets:** Real-time chat.

## Technology Stack

| Component | Planned technology |
|---|---|
| Architecture | Microservices |
| Backend | Python and FastAPI |
| Frontend | React, TypeScript, and Vite |
| Database and vector search | PostgreSQL with pgvector |
| ORM and migrations | SQLAlchemy 2 and Alembic |
| API Gateway | Traefik |
| Asynchronous messaging | RabbitMQ |
| Real-time communication | WebSockets |
| File storage | MinIO |
| Containerization | Docker and Docker Compose |
| Testing | pytest and frontend testing tools |
| Version control | Git and GitHub |

These technologies describe the planned production architecture. Final implementation and testing will determine whether adjustments are needed.

## Project Documentation

- [Project Proposal and Scope](docs/proposal.md)
- [Requirements Specification](docs/requirements.md)
- [Technology Comparison](docs/technology-comparison.md)
- [Architecture Diagrams](diagrams/)

Additional documentation will be added as the project progresses.

## Repository Structure

```text
mentoring-and-social-adaptation-platform/
├── backend/                 # Backend services
├── frontend/                # Web client
├── docs/                    # Project documentation
├── diagrams/                # Architecture and design diagrams
├── tests/                   # Automated and supporting tests
├── prototype/               #Prototype
├── .gitignore
└── README.md
```

The structure will evolve as development progresses. Individual components will be added and documented as they are implemented.

## Development Workflow

The team uses GitHub for version control and YouTrack for task management.

- Work is organized into task-specific branches.
- Commits and pull requests reference their corresponding YouTrack task IDs.
- Changes are submitted through pull requests.
- Another team member reviews changes before they are merged into `main`.
- Requirements, design decisions, and implementation progress are documented throughout development.

## Team Members

- Assem Kadulbekova
- Moldir Kabdykarim
- Anel Kashym

**Project supervisor:** Salkenov Aldiyar

## Project Status

The project is in the requirements, architecture, and design stage. The proposed architecture, technology choices, functional requirements, and system diagrams are being documented before full implementation.

## License

This project is being developed for academic purposes as part of a diploma project at Astana IT University.
