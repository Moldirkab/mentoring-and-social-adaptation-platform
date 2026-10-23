# Project Management and Risk Management

## Project Information

| Item                    | Details                                                                                                                  |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Project title           | Development of a Mentoring and Social Adaptation Platform for Children from Orphanages and Graduates of Boarding Schools |
| GitHub repository       | https://github.com/Moldirkab/mentoring-and-social-adaptation-platform                                                    |
| Project management tool | YouTrack                                                                                                                 |
| Development methodology | Scrum with milestone-based planning                                                                                      |
| Team                    | Assem Kadulbekova, Moldir Kabdykarim, Anel Kashym                                                                        |
| Supervisor              | Salkenov Aldiyar                                                                                                         |
| Current milestone       | Pre-defense 1 — October 24, 2026                                                                                         |
| Last updated            | October 23, 2026                                                                                                         |

## 1. Project Management Methodology

The team will use **Scrum with milestone-based planning** to manage the diploma project throughout the academic year.

Scrum supports iterative development through short development cycles, allowing the team to implement functionality incrementally, evaluate completed work, and adjust priorities when requirements or technical constraints change. Milestone-based planning complements this approach by aligning development with academic deadlines.

The team will apply the following principles:

- **Iterative development:** Divide the project into manageable increments.
- **Sprint planning:** Select tasks and define a goal for each sprint.
- **Prioritized backlog:** Organize work according to importance, dependencies, risks, and academic requirements.
- **Clear responsibilities:** Assign one primary person to each task, with other members contributing when needed.
- **Continuous testing:** Verify functionality throughout development.
- **Regular reviews:** Evaluate completed work and identify improvements.
- **Milestone-based planning:** Align sprint goals with pre-defense and final-defense requirements.

The planned sprint duration is two weeks. The team will review progress weekly and adjust the schedule if necessary.

### 1.1 Scrum Roles and Team Responsibilities

| Role or area                          | Team member       | Responsibilities                                                                                                      |
| ------------------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| Product Owner responsibilities        | Moldir Kabdykarim | Prioritize requirements, maintain the product backlog, and ensure the platform addresses user needs                   |
| Scrum Master responsibilities         | Anel Kashym       | Facilitate sprint planning and reviews, identify blockers, and support the team's Scrum process                       |
| Backend, database, and DevOps         | Assem Kadulbekova | Design backend architecture and database, implement APIs and server-side logic, and manage development infrastructure |
| AI matching, research, and evaluation | Moldir Kabdykarim | Prepare matching data, develop and evaluate AI-assisted matching, and maintain research and evaluation documentation  |
| Frontend and UX/UI                    | Anel Kashym       | Design user workflows, develop interfaces, and integrate frontend components with backend APIs                        |

As this is a three-person student team, members may contribute outside their primary areas when necessary. Each task will nevertheless have one primary assignee in YouTrack to maintain accountability.

### 1.2 Scrum Activities

| Activity             | Frequency                | Purpose                                                          |
| -------------------- | ------------------------ | ---------------------------------------------------------------- |
| Sprint planning      | Beginning of each sprint | Select tasks and establish a sprint goal                         |
| Progress check-in    | Weekly                   | Review progress and resolve blockers                             |
| Sprint review        | End of each sprint       | Demonstrate and evaluate completed work                          |
| Sprint retrospective | End of each sprint       | Identify improvements to the team's process                      |
| Backlog refinement   | As needed                | Clarify tasks, priorities, dependencies, and acceptance criteria |
| Risk review          | At least once per sprint | Reassess risks and mitigation actions                            |

The team will use weekly check-ins rather than requiring daily meetings. Scrum activities will be documented as they are performed.

## 2. Project Management Tools

| Tool                     | Purpose                                                                    |
| ------------------------ | -------------------------------------------------------------------------- |
| GitHub                   | Store source code, project documentation, diagrams, and version history    |
| YouTrack                 | Manage tasks, assignees, priorities, deadlines, dependencies, and progress |
| Markdown                 | Maintain version-controlled project documentation                          |
| Git branches and commits | Track changes and link implementation work to YouTrack tasks               |
| Pull requests            | Review changes before merging into the main branch                         |

### 2.1 YouTrack Task Management

Each task should have a unique issue ID, a clear title, one primary assignee, a priority, and acceptance criteria.

Deadlines will be set according to sprint goals and academic milestones. Dependencies will be recorded when one task relies on another deliverable.

Tasks will be selected for each sprint based on priority, available time, and dependencies. Work required for an imminent academic deadline will receive particular attention.

### 2.2 GitHub Workflow and Traceability

The team will follow this workflow:

1. Select a task from YouTrack.
2. Create a branch using the task ID and a short description, such as `MSAP-14-project-repository-structure`.
3. Implement the change and use the issue ID in commit messages, such as `MSAP-14 Create initial project repository structure`.
4. Push the branch to GitHub.
5. Review the changes and merge them into `main` when ready.
6. Update the YouTrack task and verify that the relevant code or documentation is available.

The team will use the `MSAP-*` identifier convention for branches and commits. The GitHub–YouTrack integration will be checked to ensure that relevant branches and commits are linked to their tasks.

## 3. Team Responsibilities and Current Tasks

The following table reflects the current YouTrack task list as of October 23, 2026. Priorities are written in English for this document: **Серьезная = Major**, **Неотложная = Urgent**, **Критическая = Critical**, and **Обычная = Normal**.

| Task ID | Task                                       | Assignee(s)       | Priority |
| ------- | ------------------------------------------ | ----------------- | -------- |
| MSAP-2  | Evidence of Relevance                      | Anel Kashym       | Normal   |
| MSAP-3  | Literature Review                          | Moldir Kabdykarim | Major    |
| MSAP-5  | Existing System Comparison                 | Moldir Kabdykarim | Major    |
| MSAP-6  | Technology Comparison and Selection        | Assem Kadulbekova | Major    |
| MSAP-7  | Functional and Non-Functional Requirements | Anel Kashym       | Major    |
| MSAP-8  | System Context Diagram                     | Moldir Kabdykarim | Normal   |
| MSAP-9  | Use Case Diagram                           | Anel Kashym       | Normal   |
| MSAP-10 | Component Diagram and Initial Architecture | Assem Kadulbekova | Normal   |
| MSAP-11 | UX/UI Prototype                            | Anel Kashym       | Major    |
| MSAP-12 | Verification and Evaluation Plan           | Moldir Kabdykarim | Normal   |
| MSAP-13 | Project Management and Risks               | Moldir Kabdykarim | Major    |
| MSAP-14 | Project Repository Structure               | Moldir Kabdykarim | Major    |
| MSAP-15 | Supervisor Feedback and Revisions          | All team members  | Normal   |

_For MSAP-14 and MSAP-15, “All team members” indicates the proposed shared responsibility for the project plan. These tasks are currently unassigned in YouTrack and must be assigned or configured accordingly in the actual system._

### 3.1 Individual Responsibilities

**Assem Kadulbekova — Backend, Database, and DevOps**

- Compare and select backend and infrastructure technologies.
- Design the system architecture and database.
- Implement backend APIs and business logic.
- Configure development and deployment infrastructure.
- Support integration and technical testing.

**Moldir Kabdykarim — AI Matching, Research, and Evaluation**

- Conduct the literature review and existing-system comparison.
- Prepare project management and evaluation documentation.
- Investigate suitable data sources for matching.
- Develop and evaluate AI-assisted matching.
- Compare the AI-assisted approach with a rule-based baseline.

**Anel Kashym — Frontend, UX/UI, and Requirements**

- Organize functional and non-functional requirements.
- Design user workflows and the interface prototype.
- Implement frontend components and integrate them with backend APIs.
- Support usability testing and interface validation.
- Prepare requirements and design documentation.

**Shared responsibilities**

All team members will contribute to the initial repository structure, review supervisor feedback, discuss revisions, and help ensure that project deliverables are ready for academic milestones.

## 4. Project Repository Structure

The initial repository will separate the backend, frontend, testing, documentation, and diagrams.

```text
mentoring-and-social-adaptation-platform/
├── backend/
├── frontend/
├── tests/
├── docs/
├── diagrams/
├── README.md
└── .gitignore
```

The `backend/`, `frontend/`, and `tests/` directories will initially be placeholders and expanded during implementation. The existing `docs/` and `diagrams/` directories will be preserved.

Because Git does not track empty directories, placeholder files such as `.gitkeep` will be added where necessary.

The `backend/` directory will contain the Python server-side application, APIs, database access, authentication, and matching logic. The `frontend/` directory will contain the user interface and client-side code. The `tests/` directory will contain shared or end-to-end tests, while component-specific tests may also be located within the backend or frontend directories.

The initial structure will be committed to GitHub under MSAP-14.

## 5. Project Milestones and Timeline

The project will be organized around academic milestones and implemented through two-week sprints.

| Milestone                                   | Target period                                | Main deliverables                                                                                                                                                               |
| ------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Pre-defense 1                               | October 24, 2026                             | Proposal, relevance evidence, literature review, system comparison, requirements, initial diagrams, technology selection, evaluation plan, and project management documentation |
| Architecture and design completion          | November–December 2026, provisional          | Refined architecture, database design, UX/UI prototype, and implementation backlog                                                                                              |
| Core platform implementation                | January–February 2027, provisional           | Authentication, roles, profiles, mentor application, and coordinator approval workflows                                                                                         |
| Matching and mentoring workflows            | February–March 2027, provisional             | Matching recommendations, coordinator-controlled pairing, meeting scheduling, and goals                                                                                         |
| Integration and evaluation                  | March–April 2027, provisional                | Integrated platform, automated tests, AI-matching evaluation, usability feedback, and improvements                                                                              |
| Final documentation and defense preparation | According to the confirmed academic schedule | Final report, evaluation results, limitations, demonstration, and presentation                                                                                                  |

Dates after Pre-defense 1 are provisional and will be updated when the university confirms subsequent deadlines.

### 5.1 Immediate Priorities for Pre-defense 1

The team will prioritize:

1. Completing the literature review and evidence of relevance.
2. Finalizing functional and non-functional requirements.
3. Completing the system context, use case, and initial architecture diagrams.
4. Completing the existing-system and technology comparisons.
5. Preparing the UX/UI prototype and evaluation plan.
6. Finalizing project management and risk documentation.
7. Creating the initial repository structure.
8. Recording supervisor feedback and identifying revisions.

Incomplete work will be documented transparently, with remaining actions identified rather than presented as completed.

## 6. Product Backlog and Sprint Planning

The product backlog will include research, requirements, design, implementation, testing, deployment, and documentation.

| Backlog area                 | Examples                                                                                                  |
| ---------------------------- | --------------------------------------------------------------------------------------------------------- |
| Research and requirements    | Literature review, relevance evidence, existing-system comparison, functional requirements                |
| Architecture and design      | Technology selection, system context, use cases, component architecture, database design, UX/UI prototype |
| Core platform                | Authentication, roles, profiles, mentor screening, coordinator workflows                                  |
| Matching                     | Eligibility filters, rule-based baseline, AI-assisted ranking, recommendation explanations                |
| Mentoring workflows          | Pair management, meeting scheduling, goals, progress records, notifications                               |
| Safeguarding                 | Consent and approval workflows, access restrictions, coordinator oversight, problem reporting             |
| Testing and evaluation       | Unit and integration tests, security checks, usability feedback, matching evaluation                      |
| Deployment and documentation | Development infrastructure, deployment configuration, user instructions, final report                     |

### 6.1 Sprint Planning Procedure

At the beginning of each sprint, the team will:

1. Review the prioritized backlog and upcoming milestones.
2. Identify unfinished work and dependencies.
3. Select a realistic set of tasks based on team capacity.
4. Define a sprint goal.
5. Confirm acceptance criteria for selected tasks.
6. Assign one primary assignee to each task.
7. Set deadlines consistent with the sprint and academic schedule.

During the sprint, the team will track progress in YouTrack and update the plan when new information affects priorities or feasibility.

### 6.2 Definition of Done

A task may be considered complete when:

- Its acceptance criteria are satisfied.
- The requested functionality or deliverable is implemented.
- Relevant tests pass, where applicable.
- Documentation is updated.
- Changes are committed to GitHub and reviewed when required.
- The YouTrack task is updated with relevant links.
- No known critical issue remains unresolved within the task's scope.

For research and documentation tasks, the team will also check factual accuracy, references, consistency, and alignment with project requirements.

## 7. Risk Management

The team will identify risks, estimate their likelihood and impact, assign owners, and define mitigation actions. Risks will be reviewed at least once per sprint and whenever significant issues arise.

### 7.1 Risk Assessment Method

Each risk will be rated from 1 to 5 for likelihood and impact.

**Risk score = Likelihood × Impact**

| Score | Level    | Response                                          |
| ----- | -------- | ------------------------------------------------- |
| 1–4   | Low      | Monitor during normal work                        |
| 5–9   | Moderate | Apply preventive measures and review periodically |
| 10–16 | High     | Prioritize mitigation and monitor closely         |
| 17–25 | Critical | Take immediate action and escalate if necessary   |

### 7.2 Risk Register

| ID  | Risk                                                                   | Likelihood | Impact | Score | Mitigation                                                                                | Owner            |
| --- | ---------------------------------------------------------------------- | ---------: | -----: | ----: | ----------------------------------------------------------------------------------------- | ---------------- |
| R1  | Insufficient suitable data for developing and evaluating matching      |          4 |      5 |    20 | Investigate suitable public data and synthetic data; document limitations                 | Moldir           |
| R2  | AI matching performs no better than the rule-based baseline            |          3 |      4 |    12 | Establish baseline metrics and retain the baseline if AI does not demonstrate improvement | Moldir           |
| R3  | Sensitive information about minors is exposed                          |          3 |      5 |    15 | Minimize data collection, enforce role-based access, and test authorization               | Assem            |
| R4  | Backend and frontend integration takes longer than expected            |          3 |      4 |    12 | Define API contracts early and integrate incrementally                                    | Assem            |
| R5  | Planning deliverables are incomplete by academic deadlines             |          4 |      4 |    16 | Prioritize milestone-critical work and review progress weekly                             | Moldir           |
| R6  | Scope exceeds the team's available time                                |          4 |      4 |    16 | Protect the MVP and defer optional features                                               | All team members |
| R7  | External services or hosting introduce unexpected costs                |          3 |      3 |     9 | Estimate costs and prepare local or open-source alternatives                              | Assem            |
| R8  | Intended-user needs are insufficiently validated                       |          4 |      3 |    12 | Review research and consult the supervisor or relevant specialists where possible         | Anel             |
| R9  | A team member becomes unavailable or falls behind                      |          3 |      4 |    12 | Document work, communicate blockers, and agree on redistribution of tasks                 | All team members |
| R10 | GitHub changes fail to link to YouTrack tasks                          |          3 |      3 |     9 | Use consistent MSAP IDs and verify integration settings                                   | Assem            |
| R11 | Supervisor feedback requires substantial revisions close to a deadline |          3 |      4 |    12 | Request feedback early and record revisions as prioritized tasks                          | All team members |

These scores are initial estimates and will be updated as the project progresses.

### 7.3 Risk Monitoring

For each high or critical risk, the team will review whether mitigation actions have been completed, whether the risk score has changed, and whether additional action is required. Risks that materialize will be documented and converted into actionable tasks when appropriate.

## 8. Task Dependencies

Tasks will be linked in YouTrack when one deliverable depends on another.

### 8.1 Planning and Design Dependencies

| Task                                               | Depends on                                                    | Reason                                                                      |
| -------------------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------- |
| MSAP-5 Existing System Comparison                  | MSAP-2 Evidence of Relevance and relevant research            | Existing systems should reflect the identified problem and project scope    |
| MSAP-7 Functional and Non-Functional Requirements  | MSAP-2 and initial research                                   | Requirements should reflect user needs and project constraints              |
| MSAP-9 Use Case Diagram                            | MSAP-7                                                        | Use cases should represent agreed requirements                              |
| MSAP-10 Component Diagram and Initial Architecture | MSAP-6 and MSAP-7                                             | Architecture should reflect selected technologies and requirements          |
| MSAP-11 UX/UI Prototype                            | MSAP-7                                                        | User workflows should reflect intended functionality                        |
| MSAP-12 Verification and Evaluation Plan           | MSAP-7 and the proposed matching approach                     | Evaluation criteria should be linked to requirements and objectives         |
| MSAP-13 Project Management and Risks               | Project backlog, responsibilities, and milestone requirements | The management plan should reflect actual scope and constraints             |
| MSAP-14 Project Repository Structure               | Existing repository and agreed project organization           | The structure should preserve existing documents and support implementation |
| MSAP-15 Supervisor Feedback and Revisions          | Available project deliverables and supervisor comments        | Revisions require material to review and feedback to record                 |

Tasks may proceed in parallel when enough information is available. These dependencies do not mean every prerequisite must be entirely finished before related work can begin.

### 8.2 Implementation Dependencies

1. Refine requirements and architecture before implementing dependent components.
2. Define database entities and API contracts before integrating dependent frontend workflows.
3. Implement authentication and authorization before exposing protected functionality.
4. Implement eligibility filters and a rule-based matching baseline before evaluating AI-assisted ranking.
5. Prepare and validate matching data before drawing conclusions about model performance.
6. Integrate the main workflows before end-to-end testing.
7. Complete testing and evaluation before finalizing claims about system quality.

Dependencies will be refined in YouTrack as the architecture and implementation backlog become more detailed.

## 9. Quality Assurance and Evaluation

Quality assurance will be integrated throughout development.

### 9.1 Software Quality

The team will plan and perform:

- Unit tests for individual functions and business rules.
- Integration tests for APIs, database operations, and frontend–backend communication.
- Authorization tests for role-specific access.
- Workflow tests for registration, profiles, pairing, meetings, and problem reporting.
- Usability checks for interface clarity and accessibility.
- Regression tests after changes to core functionality.

### 9.2 Matching Component Evaluation

The AI-assisted matching component will be evaluated against a transparent rule-based baseline. Depending on available data, evaluation may include ranking quality, recommendation coverage, and eligibility-constraint violations.

The team will document the evaluation methodology, metrics, data limitations, and results. Technical matching performance will be distinguished from real-world long-term mentoring outcomes, which cannot be established solely through a prototype or offline experiment.

### 9.3 Safeguarding and Privacy

Because the platform is intended to support minors and young adults, safeguarding and privacy are core requirements. The design will include appropriate consent and approval workflows, restricted access to sensitive records, coordinator oversight of relevant communication, and a way to report problems.

The team will document the prototype's limitations and will not claim that it is ready for real-world deployment with minors without appropriate review and safeguards.

## 10. Communication and Collaboration

The team will use YouTrack to manage tasks and GitHub to maintain version-controlled work.

The team will:

- Update assigned tasks when progress or blockers change.
- Communicate blockers that may affect sprint goals or academic deadlines.
- Document important decisions about scope, architecture, and responsibilities.
- Record supervisor feedback as revision tasks.
- Integrate changes regularly to reduce last-minute conflicts.
- Review upcoming deadlines during weekly check-ins.

When a task is blocked, its primary assignee will identify the blocker and agree with the team on the next action.

## 11. Traceability and Progress Reporting

The team will maintain traceability between requirements, tasks, implementation changes, and evaluation evidence.

**Traceability chain:**

Requirement → YouTrack task → GitHub branch, commit, or document → Verification evidence → Milestone deliverable

For example, a mentor-approval requirement will be represented by a task, implemented in the backend and relevant interface, verified through workflow and authorization tests, and included in the project demonstration or report.

Progress will be assessed using:

- Completion of milestone-critical deliverables.
- Achievement of sprint goals and acceptance criteria.
- Outstanding blockers and defects.
- Test results.
- Completion of documentation and evaluation deliverables.
- Status of high-priority risks and mitigation actions.

Task completion alone will not be treated as proof of project success. The final system must also be evaluated against its stated requirements.

## 12. Next Steps

### 12.1 Before Pre-defense 1 — October 24, 2026

The immediate priorities are:

1. Finalize the project management and risk document under MSAP-13.
2. Complete or explicitly document remaining planning and design deliverables.
3. Review the literature review, evidence of relevance, requirements, diagrams, and technology selection for consistency.
4. Confirm one primary assignee for each task in YouTrack.
5. Create the initial repository structure under MSAP-14.
6. Record supervisor feedback and revision actions under MSAP-15.
7. Verify that the latest documentation is committed to GitHub.
8. Check that branch and commit names use the correct MSAP issue IDs.

### 12.2 After Pre-defense 1

After the first pre-defense, the team will:

1. Record supervisor and committee feedback.
2. Convert requested changes into prioritized YouTrack tasks.
3. Confirm subsequent academic milestone dates.
4. Refine the product backlog and plan the next sprint.
5. Finalize the architecture and database design.
6. Begin implementation of the core platform.
7. Reassess data availability, risks, and the feasibility of matching evaluation.
8. Continue sprint reviews, testing, and documentation throughout development.

## 13. Project Management Success Criteria

The project management approach will be considered effective if:

- Academic deliverables are planned against explicit milestones.
- Each task has one primary assignee and clear acceptance criteria.
- Sprint goals are defined and reviewed regularly.
- Dependencies and blockers are visible in YouTrack.
- Source code and documentation are version-controlled in GitHub.
- Requirements can be traced to tasks and verification evidence.
- Major risks have owners and mitigation actions.
- Supervisor feedback is recorded and addressed.
- The final project is evaluated against its requirements, with limitations documented honestly.

## Conclusion

Scrum with milestone-based planning provides a structured approach for managing the year-long diploma project. Short development cycles support incremental implementation and continuous feedback, while academic milestones keep the team aligned with university deadlines.

YouTrack will provide visibility into task ownership, priorities, deadlines, and dependencies. GitHub will maintain the history of project documentation and implementation. Regular reviews, risk assessments, and testing will help the team identify problems early and deliver a platform that can be evaluated against its stated requirements.

This plan will be updated as the team receives feedback, confirms milestone dates, and learns more about the project's technical and data constraints.
