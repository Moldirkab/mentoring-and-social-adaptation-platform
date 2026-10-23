# Project Management and Risk Management

## Project Information

| Item                    | Details                                                                                                                  |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Project title           | Development of a Mentoring and Social Adaptation Platform for Children from Orphanages and Graduates of Boarding Schools |
| Project repository      | [GitHub Repository](https://github.com/Moldirkab/mentoring-and-social-adaptation-platform)                               |
| Project management tool | YouTrack                                                                                                                 |
| Development methodology | Scrum with milestone-based planning                                                                                      |
| Team                    | Assem Kadulbekova, Moldir Kabdykarim, Anel Kashym                                                                        |
| Supervisor              | Salkenov Aldiyar                                                                                                         |
| Current milestone       | Pre-defense 1 — October 24, 2026                                                                                         |
| Document status         | Initial project management plan                                                                                          |
| Last updated            | October 23, 2026                                                                                                         |

## 1. Project Management Methodology

The team will use **Scrum with milestone-based planning** to manage the development of the mentoring and social adaptation platform throughout the diploma project.

Scrum is an iterative and incremental development framework. It allows the team to divide a large project into smaller development cycles, deliver functionality progressively, evaluate completed work, and adjust priorities when requirements or technical constraints change.

Milestone-based planning complements Scrum by establishing fixed academic deadlines. This is important because the project must satisfy the requirements of Pre-defense 1, subsequent academic reviews, and the final diploma defense.

The team will apply the following principles:

- **Iterative development:** The platform will be developed in small increments instead of implementing all features at once.
- **Prioritized backlog:** Tasks will be ordered according to their importance, dependencies, technical risk, and academic requirements.
- **Defined responsibilities:** Every task will have one primary assignee responsible for completing it.
- **Continuous testing:** Completed functionality will be tested throughout development rather than only at the end.
- **Regular review:** The team will evaluate completed work, discuss difficulties, and update priorities.
- **Deadline awareness:** Sprint goals and task priorities will be aligned with academic milestones.

The planned sprint duration is **two weeks**. The team may adjust this duration if the academic schedule or workload requires it. The actual sprint schedule and completed sprint activities will be documented as development progresses.

### 1.1 Scrum Roles

The project team consists of three students. Responsibilities will be distributed according to their main areas of work.

| Scrum role or responsibility                                 | Assigned member   | Main responsibilities                                                                                                                       |
| ------------------------------------------------------------ | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Product Owner responsibilities                               | Moldir Kabdykarim | Prioritize the product backlog, clarify requirements, and ensure that development addresses the needs of mentees, mentors, and coordinators |
| Scrum Master responsibilities                                | Anel Kashym       | Facilitate sprint planning and reviews, help identify blockers, and support the team's use of Scrum practices                               |
| Development responsibilities — backend, database, and DevOps | Assem Kadulbekova | Design backend architecture and database, implement server-side functionality, and manage deployment and development infrastructure         |
| Development responsibilities — AI and research               | Moldir Kabdykarim | Prepare matching data, develop and evaluate AI-assisted matching, and maintain research and evaluation documentation                        |
| Development responsibilities — frontend and UX/UI            | Anel Kashym       | Design user workflows and interfaces and implement frontend functionality                                                                   |

Because this is a small student team, Scrum responsibilities and development work may overlap. The role allocation identifies primary responsibilities rather than preventing team members from helping with other tasks.

### 1.2 Scrum Activities

The team will use the following activities throughout the project.

| Activity             | Frequency                                            | Purpose                                                                                       |
| -------------------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| Sprint planning      | At the beginning of each sprint                      | Select prioritized tasks and define a realistic sprint goal                                   |
| Progress check-in    | Weekly                                               | Review progress, identify blockers, and coordinate work                                       |
| Sprint review        | At the end of each sprint                            | Demonstrate completed functionality or documentation and check it against acceptance criteria |
| Sprint retrospective | At the end of each sprint                            | Identify what worked well, what caused difficulties, and what should improve                  |
| Backlog refinement   | During the sprint as needed                          | Clarify requirements, dependencies, acceptance criteria, and task priorities                  |
| Risk review          | At least once per sprint and when major issues arise | Reassess risks and update mitigation actions                                                  |

Formal daily Scrum meetings are not required for this small student team. A weekly check-in will be used as a practical coordination mechanism.

## 2. Project Management Tools

The project will use GitHub and YouTrack for version control, task management, and progress tracking.

| Tool                     | Purpose                                                                                                              |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| GitHub                   | Store source code, diagrams, technical documentation, and project deliverables                                       |
| YouTrack                 | Manage the product backlog, assign tasks, track statuses, record priorities, and document dependencies and deadlines |
| Markdown                 | Maintain readable, version-controlled project documentation                                                          |
| Git branches and commits | Isolate changes and associate development work with YouTrack tasks                                                   |
| Pull requests            | Review changes before merging them into the main branch                                                              |

### 2.1 YouTrack Task Management

Each task should include:

- A unique issue ID, such as `MSAP-13`.
- A descriptive title and clear scope.
- One primary assignee.
- A priority and status.
- A deadline when required by a milestone or sprint.
- Acceptance criteria describing the expected result.
- Dependencies on other tasks, where applicable.

The product backlog will contain requirements, research activities, design deliverables, implementation tasks, testing activities, and documentation.

Tasks will be selected for each sprint according to priority, available time, and dependencies. Tasks required for an imminent academic deadline will receive particular attention.

### 2.2 GitHub Workflow and Traceability

The team will use the following workflow:

1. Select a task from YouTrack.
2. Create a branch named using the task ID and a short description, for example `MSAP-13-project-management`.
3. Implement the change and commit the work using the corresponding issue ID, for example `MSAP-13 Add project management and risk documentation`.
4. Push the branch to GitHub.
5. Review the changes and merge them into `main` when they are ready.
6. Update the YouTrack task status and verify that the relevant documentation or code is available in the repository.

The team will use the `MSAP-*` identifier convention because it matches the current YouTrack project.

The team will verify that the GitHub–YouTrack integration correctly links branches and commits to their corresponding issues. A task will not be considered fully documented merely because a branch exists; its expected deliverable must also be available and reviewed.

## 3. Team Responsibilities and Current Tasks

The following table summarizes the current project tasks in YouTrack, their assigned team members, and priorities as of October 23, 2026.

| Task ID | Task                                       | Assignee          | Priority |
| ------- | ------------------------------------------ | ----------------- | -------- |
| MSAP-2  | Evidence of Relevance                      | Anel Kashym       | Normal   |
| MSAP-3  | Literature Review                          | Moldir Kabdykarim | Major    |
| MSAP-5  | Existing System Comparison                 | Moldir Kabdykarim | Major    |
| MSAP-6  | Technology Comparison and Selection        | Assem Kadulbekova | Major    |
| MSAP-7  | Functional and Non-Functional Requirements | Anel Kashym       | Major    |
| MSAP-8  | System Context Diagram                     | Moldir Kabdykarim | Normal   |
| MSAP-9  | Use Case Diagram                           | Anel Kashym       | Normal   |
| MSAP-10 | Component Diagram and Initial Architecture | Assem Kadulbekova | Normal   |
| MSAP-11 | UX/UI Prototype                            | Anel Kashym       | Normal   |
| MSAP-12 | Verification and Evaluation Plan           | Moldir Kabdykarim | Normal   |
| MSAP-13 | Project Management and Risks               | Moldir Kabdykarim | Major    |
| MSAP-14 | Supervisor Feedback and Revisions          | Unassigned        | Major    |

_Task assignments and priorities should be updated in YouTrack whenever responsibilities or project requirements change. MSAP-14 requires an assigned owner before work begins._

### 3.1 Responsibility Boundaries

**Assem Kadulbekova — Backend, Database, and DevOps**

- Compare and select backend and infrastructure technologies.
- Design the initial system architecture and database.
- Implement backend APIs and core business logic.
- Configure development, testing, and deployment infrastructure.
- Support integration and technical testing.

**Moldir Kabdykarim — AI Matching, Research, and Evaluation**

- Conduct the literature review and existing-system comparison.
- Prepare project management, evaluation, and research documentation.
- Investigate data sources and prepare appropriate matching data.
- Develop and evaluate the AI-assisted matching component.
- Compare AI-assisted matching with a transparent rule-based baseline.

**Anel Kashym — Frontend, UX/UI, and Requirements**

- Organize functional and non-functional requirements.
- Design user workflows and the interface prototype.
- Implement frontend components and integrate them with backend APIs.
- Support usability testing and interface validation.
- Prepare relevant requirements and design documentation.

Responsibilities may be adjusted if workload, technical dependencies, or supervisor feedback require changes. Each YouTrack task will retain one primary assignee to ensure accountability.

## 4. Project Milestones and Timeline

The project will be organized around academic milestones and implemented through two-week sprints. The dates below distinguish the confirmed immediate deadline from provisional future planning periods.

| Milestone                                   | Target period                                       | Main deliverables                                                                                                                                                                           | Status         |
| ------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| Pre-defense 1                               | October 24, 2026                                    | Project proposal, evidence of relevance, literature review, existing-system comparison, requirements, initial diagrams, technology selection, evaluation plan, project management and risks | In preparation |
| Architecture and design completion          | November–December 2026, provisional                 | Refined architecture, database design, UX/UI prototype, clarified requirements, and implementation backlog                                                                                  | Planned        |
| Core platform implementation                | January–February 2027, provisional                  | Authentication, role-based access, user profiles, mentor application and coordinator approval workflows                                                                                     | Planned        |
| Matching and mentoring workflows            | February–March 2027, provisional                    | Matching recommendations, coordinator-controlled pairing, meeting scheduling, goals, and relevant safety workflows                                                                          | Planned        |
| Integration and evaluation                  | March–April 2027, provisional                       | Integrated platform, automated tests, AI-matching evaluation, usability feedback, and improvements                                                                                          | Planned        |
| Final documentation and defense preparation | April–May 2027 or the confirmed university schedule | Final report, results, limitations, demonstration, presentation, and defense preparation                                                                                                    | Planned        |

The provisional periods must be updated once the university confirms the dates for subsequent pre-defenses and the final defense. The team will maintain more precise dates for tasks and sprints in YouTrack.

### 4.1 Immediate Milestone: Pre-defense 1

The first priority is to prepare the required planning and design deliverables before October 24, 2026.

The team will prioritize:

1. Completing the literature review and evidence of relevance.
2. Finalizing functional and non-functional requirements.
3. Completing the system context and use case diagrams.
4. Completing the initial component architecture and technology selection.
5. Preparing the existing-system comparison and UX/UI prototype.
6. Finalizing the verification and evaluation plan.
7. Reviewing the project management and risk document.
8. Collecting supervisor feedback and recording required revisions.

Where a deliverable cannot be fully completed before the deadline, the team will identify the remaining work explicitly, document the limitation, and agree on the next action rather than presenting incomplete work as finished.

## 5. Product Backlog and Sprint Planning

The product backlog will contain all known work required to develop and evaluate the platform. Items will be prioritized according to their value, academic importance, risk, and technical dependencies.

The initial backlog will be divided into the following areas:

| Backlog area                 | Examples of work                                                                                          |
| ---------------------------- | --------------------------------------------------------------------------------------------------------- |
| Research and requirements    | Literature review, evidence of relevance, existing-system comparison, functional requirements             |
| Architecture and design      | Technology selection, system context, use cases, component architecture, database design, UX/UI prototype |
| Core platform                | Authentication, roles, profiles, mentor screening, coordinator workflows                                  |
| Matching                     | Hard eligibility filters, rule-based baseline, AI-assisted ranking, recommendation explanations           |
| Mentoring workflows          | Pair management, meeting scheduling, goals, progress records, notifications                               |
| Safeguarding                 | Consent and approval workflows, access restrictions, coordinator visibility, problem reporting            |
| Testing and evaluation       | Unit and integration tests, security checks, usability feedback, matching evaluation                      |
| Deployment and documentation | Containerization, deployment configuration, user instructions, final report                               |

### 5.1 Sprint Planning Procedure

At the beginning of each sprint, the team will:

1. Review the current backlog and academic milestones.
2. Identify unfinished work and dependencies.
3. Select a realistic set of tasks based on team capacity.
4. Agree on a sprint goal.
5. Ensure selected tasks have clear acceptance criteria.
6. Assign one primary assignee to each task.
7. Set task deadlines consistent with the sprint and milestone.

During the sprint, the team will track progress in YouTrack and record changes when new information affects the plan.

### 5.2 Definition of Done

A task may be considered complete when its applicable conditions are satisfied:

- The requested functionality or deliverable is implemented.
- The result meets the task's acceptance criteria.
- Relevant tests have passed, where applicable.
- Documentation has been updated.
- Changes have been committed to GitHub and reviewed before merging when a review is required.
- The corresponding YouTrack task status and links have been updated.
- No known critical issue remains unresolved for the scope being marked complete.

For research and documentation tasks, the definition of done also includes checking factual accuracy, references, consistency, and alignment with the project requirements.

## 6. Project Risks

Risk management will be integrated into sprint planning and project reviews. The team will identify risks, estimate their likelihood and impact, assign an owner, and define mitigation actions.

### 6.1 Risk Assessment Method

Each risk will be rated on a scale from 1 to 5 for likelihood and impact.

**Risk score = Likelihood × Impact**

| Score | Level    | Response                                          |
| ----- | -------- | ------------------------------------------------- |
| 1–4   | Low      | Monitor during normal project work                |
| 5–9   | Moderate | Apply preventive measures and review periodically |
| 10–16 | High     | Prioritize mitigation and monitor closely         |
| 17–25 | Critical | Take immediate action and escalate if necessary   |

The scores are initial estimates and should be reassessed as more information becomes available.

### 6.2 Risk Register

| ID  | Risk                                                                                       | Likelihood | Impact | Score | Mitigation strategy                                                                                                                                            | Owner            |
| --- | ------------------------------------------------------------------------------------------ | ---------: | -----: | ----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| R1  | Insufficient suitable data for developing and evaluating the matching component            |          4 |      5 |    20 | Investigate public datasets and synthetic data; document data limitations; avoid claiming real-world effectiveness without appropriate evidence                | Moldir           |
| R2  | AI-assisted matching performs no better than the rule-based baseline                       |          3 |      4 |    12 | Establish baseline metrics early; compare models fairly; retain the baseline if the AI approach does not demonstrate improvement                               | Moldir           |
| R3  | Sensitive information about minors is exposed or accessed without authorization            |          3 |      5 |    15 | Minimize collected data, enforce role-based access, protect sensitive records, define consent and coordinator-approval workflows, and test authorization rules | Assem            |
| R4  | Backend and frontend integration takes longer than expected                                |          3 |      4 |    12 | Define API contracts early, integrate incrementally, and test endpoints before dependent features are completed                                                | Assem            |
| R5  | Research and planning deliverables are incomplete by academic deadlines                    |          4 |      4 |    16 | Prioritize milestone-critical tasks, track deadlines in YouTrack, and review unfinished work weekly                                                            | Moldir           |
| R6  | The project scope becomes too large for the available time                                 |          4 |      4 |    16 | Protect the core MVP, defer optional features, and obtain team agreement before expanding scope                                                                | All team members |
| R7  | External services or hosting introduce unexpected costs or technical limitations           |          3 |      3 |     9 | Prefer free or low-cost development tools, estimate API and hosting costs, and prepare local or open-source alternatives                                       | Assem            |
| R8  | User needs are insufficiently validated because access to intended participants is limited |          4 |      3 |    12 | Review published research, consult the supervisor or relevant specialists where possible, and conduct usability checks with appropriate adult participants     | Anel             |
| R9  | A team member becomes unavailable or falls behind on assigned tasks                        |          3 |      4 |    12 | Maintain documentation, communicate blockers early, and redistribute work by agreement while preserving one assignee per task                                  | All team members |
| R10 | GitHub branches or commits fail to link to the corresponding YouTrack issues               |          3 |      3 |     9 | Use consistent MSAP issue IDs, verify integration settings, and manually update issue links when automatic linking fails                                       | Assem            |
| R11 | Supervisor feedback requires substantial revisions close to a milestone                    |          3 |      4 |    12 | Request feedback early, maintain a revision buffer, and record requested changes as prioritized YouTrack tasks                                                 | Moldir           |

### 6.3 Risk Monitoring

Risks will be reviewed at the end of each sprint and whenever a significant issue arises.

For each high or critical risk, the team will verify whether the mitigation action has been completed, whether the score has changed, and whether additional action is necessary. Risks that materialize will be converted into actionable tasks or documented issues in YouTrack.

The risk register will be updated as the architecture, data availability, matching approach, and deployment requirements become clearer.

## 7. Task Dependencies

Tasks will be linked in YouTrack when one deliverable must be completed before another can proceed reliably.

### 7.1 Planning and Design Dependencies

| Task                                               | Depends on                                                              | Reason                                                                            |
| -------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| MSAP-5 Existing System Comparison                  | MSAP-2 Evidence of Relevance and relevant research                      | Existing systems should be selected based on the problem and project scope        |
| MSAP-7 Functional and Non-Functional Requirements  | MSAP-2 Evidence of Relevance and initial research                       | Requirements must reflect the identified user needs and project constraints       |
| MSAP-9 Use Case Diagram                            | MSAP-7 Functional and Non-Functional Requirements                       | Use cases should represent the agreed system functionality and actors             |
| MSAP-10 Component Diagram and Initial Architecture | MSAP-6 Technology Comparison and Selection and MSAP-7 Requirements      | Architecture should reflect the selected technologies and system requirements     |
| MSAP-11 UX/UI Prototype                            | MSAP-7 Functional and Non-Functional Requirements                       | Interface workflows should reflect the intended user tasks                        |
| MSAP-12 Verification and Evaluation Plan           | MSAP-7 Requirements and the proposed matching approach                  | Evaluation criteria should be linked to requirements and project objectives       |
| MSAP-13 Project Management and Risks               | Initial task backlog, team responsibilities, and milestone requirements | The plan must reflect the real project scope, owners, deadlines, and dependencies |

These dependencies indicate logical relationships, not a requirement to delay all work until every prerequisite is fully finished. Tasks may proceed in parallel when enough information is available.

### 7.2 Implementation Dependencies

The following implementation dependencies are expected to guide later sprints:

1. Finalize the core requirements and architecture before implementing dependent components.
2. Define database entities and API contracts before integrating dependent frontend workflows.
3. Implement authentication and authorization before exposing protected mentor, mentee, or coordinator functions.
4. Implement the eligibility filters and rule-based matching baseline before evaluating AI-assisted ranking.
5. Prepare and validate matching data before drawing conclusions about model performance.
6. Integrate the main workflows before end-to-end testing.
7. Complete testing and evaluation before finalizing claims about system quality and matching effectiveness.

Dependencies will be refined in YouTrack as the architecture and backlog become more detailed.

## 8. Quality Assurance and Evaluation

Quality assurance will be performed throughout development. The team will evaluate both software functionality and the quality of the matching component.

### 8.1 Software Quality

The team will plan and perform:

- Unit testing for individual functions and business rules.
- Integration testing for backend endpoints, database operations, and frontend–backend communication.
- Authorization testing to verify that each role can access only permitted functionality.
- Validation testing for registration, profiles, pairing workflows, meetings, and problem reporting.
- Usability checks for the clarity and accessibility of the user interface.
- Regression testing after changes to core workflows.

### 8.2 Matching Component Evaluation

The matching component will be evaluated against a transparent rule-based baseline. Depending on the available and appropriate data, evaluation may include ranking quality, recommendation coverage, and violations of eligibility constraints.

The team will define the metrics, data preparation process, and evaluation limitations in the verification and evaluation plan. The evaluation must distinguish between technical matching performance and actual long-term mentoring outcomes, which cannot be established solely through a prototype or offline experiment.

### 8.3 Safeguarding and Privacy

The platform is intended to support minors and young adults who may require additional safeguarding. Therefore, safety and privacy requirements are treated as core system requirements rather than optional enhancements.

The design will include appropriate consent and approval workflows, restricted access to sensitive records, coordinator oversight of relevant communication, and a way to report problems. The team will document the limitations of its prototype and will not claim that the system is ready for real-world deployment with minors without appropriate review and safeguards.

## 9. Communication and Collaboration

The team will use YouTrack for task ownership and progress, GitHub for version-controlled work, and agreed team communication channels for coordination.

The following practices will be used:

- Each team member will update their assigned tasks when progress or blockers change.
- Blockers that may affect a sprint goal or academic deadline will be communicated promptly.
- Important decisions about scope, architecture, and responsibilities will be documented.
- Supervisor feedback will be recorded as revisions or new YouTrack tasks.
- Work will be integrated regularly to reduce last-minute merge and integration problems.
- The team will review upcoming deadlines during weekly check-ins.

If a task becomes blocked, the assignee will explain the blocker, identify what is needed to proceed, and agree with the team on a next action.

## 10. Traceability and Progress Reporting

The team will maintain traceability between project requirements, YouTrack tasks, implementation changes, and evaluation evidence.

The intended traceability chain is:

**Requirement → YouTrack task → GitHub branch/commit or documentation → verification evidence → milestone deliverable**

For example, a requirement concerning mentor approval should be represented by an appropriate task, implemented in the backend and relevant interface, verified through authorization and workflow tests, and included in the relevant project demonstration or report.

Progress will be assessed using:

- The status of milestone-critical YouTrack tasks.
- Completion of sprint goals and acceptance criteria.
- The number and severity of unresolved blockers.
- Test results and unresolved defects.
- Completion of documentation and evaluation deliverables.
- The status of high-priority risks and mitigation actions.

Task completion alone will not be treated as evidence that the overall project is successful. The final evaluation must also demonstrate that the delivered system meets the defined requirements.

## 11. Next Steps

### 11.1 Before Pre-defense 1 — October 24, 2026

The immediate priorities are:

1. Review and finalize the project management and risk documentation under MSAP-13.
2. Complete or clearly document the outstanding planning and design deliverables.
3. Review the literature review, evidence of relevance, requirements, diagrams, and technology selection for consistency.
4. Confirm that each active task has one primary assignee.
5. Assign an owner to MSAP-14 before starting supervisor-feedback revisions.
6. Verify that the repository contains the latest reviewed documentation.
7. Check that GitHub branches and commits use the correct MSAP identifiers.
8. Record any remaining gaps and agree on corrective actions with the supervisor.

### 11.2 After Pre-defense 1

After the first pre-defense, the team will:

1. Record supervisor and committee feedback.
2. Convert requested changes into prioritized YouTrack tasks.
3. Confirm the dates and expected deliverables for subsequent academic milestones.
4. Refine the product backlog and create the next sprint goal.
5. Finalize the architecture and database design.
6. Begin implementation of the core platform.
7. Reassess risks, data availability, and the feasibility of the matching evaluation.
8. Continue sprint reviews, testing, and documentation throughout development.

## 12. Success Criteria for Project Management

The project management approach will be considered effective if:

- Academic deliverables are planned against explicit milestones.
- Every active task has one primary assignee and clear acceptance criteria.
- Sprint goals are defined and reviewed regularly.
- Dependencies and blockers are visible in YouTrack.
- Source code and documentation are version-controlled in GitHub.
- Requirements can be traced to implementation tasks and verification evidence.
- Major risks have owners and practical mitigation actions.
- Supervisor feedback is recorded and addressed.
- The final project is evaluated against its requirements, with limitations documented honestly.

## Conclusion

Scrum with milestone-based planning provides a structured approach for managing this year-long diploma project. Short development cycles support incremental implementation and continuous feedback, while academic milestones keep the team aligned with university deadlines.

YouTrack will provide visibility into responsibilities, priorities, deadlines, and dependencies. GitHub will maintain the history of project documentation and implementation. Regular sprint reviews, risk assessments, and testing will help the team identify problems early and deliver a platform that can be evaluated against its stated requirements.

The plan will be updated throughout the academic year as the team receives feedback, confirms milestone dates, and learns more about the project's technical and data constraints.
