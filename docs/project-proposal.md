# Development of a Mentoring and Social Adaptation Platform for Children from Orphanages and Graduates of Boarding Schools

**Institution:** Astana IT University  
**School:** School of Software Engineering  
**Team Members:** Assem Kadulbekova, Moldir Kabdykarim, Anel Kashym  
**Supervisor:** Salkenov Aldiyar

## 1. Project Proposal

### 1.1. Problem Statement

Graduates of orphanages and boarding schools may face challenges when transitioning to independent adult life, including developing daily-living skills, maintaining supportive relationships, continuing education, and finding employment [1].

Research conducted in Kazakhstan highlights the importance of socialisation and support for young people who have lived in orphanages [2].

Mentoring programmes can help young people develop social connections and receive guidance as they work toward personal goals [1]. Digital mentoring research also identifies security, privacy, and communication as important considerations when designing platforms for young people and their mentors [3].

This project addresses three main problems:

1. **Limited scalability of mentoring coordination.** Managing participant information, selecting compatible mentor–mentee pairs, and following up on activities manually may increase the workload of coordinators. Research on two-sided matching demonstrates that allocating mentors and mentees can involve multiple preferences and matching constraints [4].

2. **Communication and safeguarding risks.** Communication between adult mentors and underage mentees through uncontrolled channels can make it more difficult to establish appropriate safeguarding procedures and oversee reported concerns. Research on digital mentoring highlights the importance of security and control in platform design [3].

3. **Limited progress monitoring.** Without structured records of meetings, goals, and completed activities, organizations may find it difficult to track participation and evaluate mentoring outcomes. Research on care leavers identifies the importance of support during the transition to independent living [1].

The proposed platform will centralize participant information, support mentor–mentee matching, facilitate communication, and provide coordinators with tools for managing mentoring relationships and monitoring activities. Its design will incorporate requirements identified in digital mentoring research [3]. Computational matching methods will inform the development of the recommendation component [5].

The extent of these problems and the specific needs of the intended users will be investigated through literature review, existing-system analysis, and stakeholder research. Claims about current organizational practices will be verified where possible rather than treated as established findings without evidence.

### 1.2. Target Users

The platform is intended for the following user groups:

- **Mentees:** Young people aged 14–18 living in orphanages and graduates of boarding schools aged 18–23 who need guidance and support in preparing for independent life.
- **Mentors:** Screened adult volunteers who provide guidance, share practical experience, and support mentees in pursuing personal and educational goals.
- **Coordinators:** NGO representatives or institutional staff responsible for reviewing mentor applications, managing mentoring pairs, monitoring activities, and addressing reported concerns.
- **Platform administrators:** Authorized users responsible for technical administration, user-role management, and platform configuration.

Participation by minors will require appropriate institutional authorization, consent arrangements, and safeguarding procedures. The platform will apply role-based access and appropriate restrictions to sensitive participant information. The emphasis on security and control is consistent with needs identified in digital mentoring research [3].

### 1.3. Project Aim

The aim of this project is to design and develop a responsive web platform that supports the mentoring cycle, facilitates safe mentor–mentee communication, and enables coordinators to manage mentoring relationships and monitor participant activities. The platform's focus on social adaptation is informed by research on young people transitioning from institutional care [2].

### 1.4. Project Objectives

The project will pursue the following objectives:

1. Investigate the needs of mentees, mentors, and coordinators through stakeholder research, including three to five interviews where access and authorization permit.
2. Review scientific literature on the social adaptation of care leavers, youth mentoring, and digital mentoring platforms.
3. Analyze existing mentoring systems and identify functional gaps relevant to the target users.
4. Define functional and non-functional requirements with measurable acceptance criteria.
5. Design the system architecture, database model, API structure, and user interface for the key user scenarios.
6. Implement the core platform functionality, including authentication, role-based access, mentor applications, matching recommendations, meeting management, messaging, goal tracking, and a coordinator dashboard, prioritizing a feasible minimum viable product.
7. Investigate and evaluate a machine-learning-based matching approach against an appropriate baseline, subject to suitable data availability.
8. Verify the implementation through automated tests and usability testing, and evaluate selected workflows against a documented baseline where a fair comparison is feasible.

### 1.5. Expected Outcomes

The expected outcome is a working responsive web application deployed in a test environment, accompanied by technical documentation and evaluation results.

The planned deliverables include:

- A documented analysis of the problem, target users, literature, and existing systems.
- A requirements specification with functional and non-functional requirements and acceptance criteria.
- System architecture, database design, API documentation, and user-interface prototypes.
- A web application supporting the agreed core mentoring workflows.
- A mentor–mentee matching component with documented matching criteria.
- An automated test suite and instructions for configuring, running, and verifying the application.
- An evaluation report containing appropriate technical and usability measurements.

Evaluation may include the System Usability Scale (SUS), task completion rate, and coordinator time required to complete a matching workflow compared with a documented manual baseline. These measurements will be collected only if suitable participants, permissions, and testing conditions are available. Any limitations will be reported transparently.

The project will not claim demonstrated improvements in long-term social adaptation unless supported by appropriate empirical evidence.

## 2. Project Scope

### 2.1. In Scope

The following functionality is planned for the project. The team will prioritize the core workflows for the minimum viable product (MVP).

| ID       | Feature                         | Description                                                                                                                    |
| -------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| SCOPE-01 | Registration and authentication | Allow users to sign in and access functionality according to their assigned roles.                                             |
| SCOPE-02 | Role-based access control       | Distinguish mentees, mentors, coordinators, and platform administrators.                                                       |
| SCOPE-03 | Mentor applications             | Allow prospective mentors to submit applications and authorized coordinators to review them and record decisions.              |
| SCOPE-04 | Participant profiles            | Store relevant information, including interests, goals, availability, and areas of support.                                    |
| SCOPE-05 | Mentor–mentee matching          | Generate recommendations based on relevant attributes, such as interests, location, and availability.                          |
| SCOPE-06 | Coordinator-controlled pairing  | Allow coordinators to review recommendations and make final pairing decisions.                                                 |
| SCOPE-07 | Messaging                       | Provide communication between approved participants, with disclosed coordinator oversight and appropriate access restrictions. |
| SCOPE-08 | Problem reporting               | Allow users to report concerns or inappropriate behavior for coordinator review.                                               |
| SCOPE-09 | Meeting management              | Support meeting scheduling and recording meeting notes, subject to role-based permissions.                                     |
| SCOPE-10 | Goals and learning tracks       | Support basic mentoring goals and selected practical-life skill development activities where feasible within the MVP.          |
| SCOPE-11 | Coordinator dashboard           | Display mentoring pairs, relevant activities, and indicators of potentially inactive pairs.                                    |
| SCOPE-12 | Notifications                   | Provide basic in-app notifications and email notifications for selected events, subject to implementation feasibility.         |
| SCOPE-13 | Matching evaluation             | Evaluate the matching approach against a documented baseline using an appropriate method and available data.                   |
| SCOPE-14 | Testing and documentation       | Provide automated tests, setup instructions, architecture documentation, and evaluation results.                               |

The MVP will prioritize authentication and authorization, participant profiles, mentor application review, matching recommendations, coordinator-controlled pairing, problem reporting, and essential communication. Meeting management, goals, learning tracks, and email notifications will be implemented according to the team's available time and the agreed acceptance criteria.

Machine-learning-based matching will be investigated as a technical component. A transparent rule-based or weighted-scoring baseline will be established first. A machine-learning model will be evaluated if suitable data are available. Previous research has explored computational methods for mentor–mentee matching [4]. Hybrid machine-learning approaches have also been proposed for this task [5]. Synthetic data, if used, will be clearly identified and will not be presented as evidence of real-world matching effectiveness.

### 2.2. Out of Scope

The following features are excluded from the planned MVP:

| ID     | Excluded feature                                              | Reason                                                                                                           |
| ------ | ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| OUT-01 | Native Android and iOS applications                           | The project will deliver a responsive web application rather than separate native mobile applications.           |
| OUT-02 | Integration with government systems                           | Such integration requires external authorization, access to appropriate interfaces, and additional coordination. |
| OUT-03 | Donations and payment processing                              | Financial transactions are not required for the core mentoring workflow.                                         |
| OUT-04 | Psychological diagnosis or automated mental-health assessment | These functions require specialized expertise, validation, and safeguards beyond the project's scope.            |
| OUT-05 | Automatic mentor approval or final pairing                    | Mentor approval and final matching decisions will remain under authorized coordinator control.                   |

Features excluded from the MVP may be considered in future development, but they will not be treated as required deliverables for the initial implementation.

## References

[1] A. E. Thompson and J. K. P. Greeson, “Prosocial activities and natural mentoring among youth at risk of aging out of foster care,” _Journal of the Society for Social Work and Research_, vol. 8, no. 3, pp. 421–440, 2017, doi: 10.1086/693119.

[2] A. Sadyrova and Z. Simtikov, “Socialisation and experience of living in orphanages during childhood,” _International Journal of Child Care and Education Policy_, vol. 19, Art. no. 2, 2025, doi: 10.1186/s40723-025-00142-5.

[3] R. L. Radlick, J. Mirkovic, S. Przedpelska, E. H. Brendmo, and D. Gammon, “Experiences and needs of multicultural youth and their mentors, and implications for digital mentoring platforms: Qualitative exploratory study,” _JMIR Formative Research_, vol. 4, no. 2, Art. no. e15500, 2020, doi: 10.2196/15500.

[4] C. Haas, M. Hall, and S. L. Vlasnik, “Finding optimal mentor-mentee matches: A case study in applied two-sided matching,” _Heliyon_, vol. 4, no. 6, Art. no. e00634, 2018, doi: 10.1016/j.heliyon.2018.e00634.

[5] J. Varghese and M. Mohaghegh, “Personality-based hybrid machine learning model for mentor-mentee matching using collaborative and content filtering methods,” in _Proc. 2023 7th International Symposium on Multidisciplinary Studies and Innovative Technologies (ISMSIT)_, 2023, pp. 1–6, doi: 10.1109/ISMSIT58785.2023.10304908.
