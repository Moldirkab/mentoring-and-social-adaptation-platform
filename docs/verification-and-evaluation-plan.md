# Verification and Evaluation Plan

## 1. Purpose

This document defines how the Mentoring and Social Adaptation Platform will be tested and evaluated to demonstrate that it meets its functional and non-functional requirements and achieves its project objectives.

The evaluation covers functional correctness, security and privacy, performance, usability, and the effectiveness of the proposed mentor-matching approach. Each test will have defined conditions, measurable criteria, and recorded results.

The project will be considered successful when all mandatory requirements are verified, critical security and safeguarding tests pass, representative users can complete the main workflows, and the matching approach is evaluated against a documented baseline.

## 2. Evaluation Strategy

The platform will be evaluated using five complementary methods:

1. **Functional testing:** automated unit, API integration, and end-to-end tests.
2. **Security and privacy testing:** access-control tests, negative tests, and inspection of data handling.
3. **Performance testing:** response-time and reliability measurements under a defined test load.
4. **Usability evaluation:** task-based testing with adult participants using a prototype or implemented system.
5. **Matching evaluation:** comparison of the proposed AI-assisted matching method with a rule-based baseline using the same test dataset.

Testing will use synthetic profiles and non-sensitive test data wherever possible. No real children's personal information will be required for the technical evaluation.

## 3. Functional Verification

Functional tests will verify the requirements specified in `functional-non-functional-requirements.md`. Each test case will record its requirement ID, preconditions, test inputs, expected result, actual result, and pass/fail status.

| Test area                      | Requirements covered                                  | Test method                                | Acceptance criteria                                                                                                                                        |
| ------------------------------ | ----------------------------------------------------- | ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentication and accounts    | FR-01, FR-02, FR-13, FR-14, FR-15                     | Unit and API tests                         | Valid users can sign in; invalid credentials are rejected; minors cannot self-register; required consent is enforced; profile permissions are respected.   |
| Roles and permissions          | FR-17, FR-18, FR-19                                   | Automated authorization and negative tests | All tested API operations comply with the permission matrix; cross-organisation and unauthorized access attempts are denied.                               |
| Mentor screening               | FR-03, FR-04                                          | API integration tests                      | Applications follow the required review workflow; unapproved mentors cannot be matched.                                                                    |
| Mentor discovery and matching  | FR-05, FR-21, FR-23, FR-24                            | Unit, integration, and ranking tests       | Hard eligibility filters are enforced; the reference dataset produces the expected baseline ranking; scores and criterion-level contributions are correct. |
| Pair management                | FR-06                                                 | API and end-to-end tests                   | Only a coordinator can create, pause, or end a pair; pair status controls access to communication.                                                         |
| Communication and safeguarding | FR-07, FR-08, FR-25, FR-26                            | API, integration, and negative tests       | Messages are restricted to active pairs; reports reach the appropriate coordinator; moderation actions are logged.                                         |
| Meetings and records           | FR-09, FR-29, FR-30                                   | Integration and scheduler tests            | Meeting statuses, reminders, notes, and visibility permissions behave as specified.                                                                        |
| Goals and monitoring           | FR-10, FR-11                                          | API and end-to-end tests                   | Progress calculations are correct; inactive pairs are flagged at the specified 14-day threshold.                                                           |
| Notifications                  | FR-04, FR-09 and applicable notification requirements | Integration tests                          | Required notifications are generated for the corresponding events and delivered through the configured channels.                                           |

### 3.1 Test execution and completion criteria

Automated tests will be implemented with the backend testing framework selected for the project, using `pytest` if FastAPI is selected. API and end-to-end testing tools will be chosen according to the final implementation stack.

The following completion criteria will be used:

- 100% of mandatory requirements have at least one documented verification test.
- 100% of executed mandatory acceptance tests pass before the final release.
- All identified critical and high-severity defects are resolved before release.
- Failed tests are investigated, corrected where necessary, and rerun.
- Test results are linked to their corresponding requirement IDs.

Optional features will be evaluated according to their implementation status and priority. Features not implemented will be reported as limitations rather than counted as passed tests.

## 4. Non-Functional Verification

| Quality attribute           | Verification method                                   | Measurement conditions                                                                                       | Acceptance criteria                                                                                                        |
| --------------------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Security and access control | Automated authorization tests and security inspection | Authenticated users with different roles; attempts to access other organisations' records and inactive pairs | All defined authorization tests pass; no unauthorized access to protected records is observed.                             |
| Privacy and data protection | Code and configuration inspection; negative tests     | Test accounts, synthetic personal data, and simulated deletion requests                                      | Personal data is exposed only to authorized roles; deletion and anonymization behavior follows the specified requirements. |
| Performance                 | API load testing                                      | Controlled test environment, documented hardware, dataset size, and concurrent request count                 | The agreed response-time target is met for the specified workload, with no unexplained errors or data corruption.          |
| Reliability                 | Repeated workflow and integration tests               | Repeated account, matching, messaging, and meeting operations                                                | No unrecovered application errors or inconsistent records occur in the tested workflows.                                   |
| Usability                   | Task-based evaluation                                 | Participants complete predefined tasks using the same prototype version and instructions                     | At least 80% of participants complete each critical task without assistance; problems and completion times are documented. |
| Maintainability             | Code review and automated checks                      | Repository, test suite, dependency configuration, and CI pipeline                                            | Code follows the team's agreed conventions; tests run reproducibly; dependencies and setup instructions are documented.    |

Numeric performance targets must be finalized against the project's non-functional requirements before the performance test is executed. Response times will be reported as median and 95th-percentile latency, alongside error rates and the exact test conditions.

## 5. Usability Evaluation

### 5.1 Participants

The initial usability evaluation will recruit approximately 5–8 adult participants, such as university students or adults familiar with volunteering, mentoring, or digital services. If coordinators or NGO representatives are available, their feedback will be collected separately.

The initial evaluation will not require participation by minors. Testing with children would require appropriate institutional approval, informed consent and safeguarding arrangements.

### 5.2 Test tasks

Participants will be asked to complete representative tasks appropriate to their assigned role:

- **Mentor:** review a profile, complete an application, and identify its review status.
- **Mentee:** review their profile, access an assigned mentor relationship, and locate their goals or upcoming meetings.
- **Coordinator:** review a mentor application, examine matching recommendations, approve a pairing, and schedule a meeting.
- **Coordinator:** locate an inactive pair and respond to a simulated safety report.

Tasks will be demonstrated using the same test environment, without exposing participants to real children's data.

### 5.3 Usability metrics

| Metric                    | Measurement                                                        | Target                                                    |
| ------------------------- | ------------------------------------------------------------------ | --------------------------------------------------------- |
| Task completion rate      | Successfully completed tasks divided by attempted tasks            | At least 80% for each critical task                       |
| Task completion time      | Time from the start instruction to successful completion           | Record time for each task and calculate median            |
| Assistance rate           | Tasks requiring moderator help divided by attempted tasks          | Record and identify recurring difficulties                |
| User-reported ease        | Short questionnaire after each task or workflow                    | Collect a 1–5 rating and report the mean and distribution |
| Critical usability issues | Problems that prevent task completion or cause a safeguarding risk | No unresolved critical issues before release              |

Results will be reported descriptively because the initial sample is small. The evaluation will identify interface problems and opportunities for improvement; it will not be presented as a statistically representative study of all intended users.

## 6. AI-Assisted Mentor-Matching Evaluation

### 6.1 Objective

The objective is to determine whether AI-assisted matching improves the relevance of mentor recommendations compared with a simpler, transparent rule-based baseline.

AI recommendations will support coordinators rather than make autonomous pairing decisions. A coordinator will retain responsibility for approving or rejecting every proposed match.

### 6.2 Methods compared

**Baseline: weighted rule-based matching**

The baseline will apply eligibility filters and calculate a weighted score using structured profile fields such as shared interests, city, availability, and stated preferences. Eligible mentors will be ranked by their total score.

**Proposed approach: AI-assisted matching**

The proposed approach will use semantic similarity between mentee needs and mentor interests or experience, for example through text embeddings and cosine similarity. Structured compatibility criteria will also be considered. Hard eligibility and safeguarding filters will be applied before ranking.

The final AI method will depend on the data available and the implementation completed during the project. Any optional reranking or language-model explanations will be evaluated separately and will not be required for the core comparison.

### 6.3 Dataset and evaluation conditions

A synthetic dataset will be created containing mentee profiles, mentor profiles, availability, location or online-format preferences, interests, experience, and capacity constraints.

The dataset will include both eligible and ineligible mentor candidates. Expected eligibility decisions will be specified in advance. A separate set of relevance judgments will be created for eligible recommendations using predefined criteria and, where feasible, independent adult reviewers.

Both methods will use the same profiles, eligibility constraints, and evaluation cases. Test cases will be separated from any data used to tune the matching method to reduce evaluation bias.

No personally identifiable information from children will be used. Synthetic test results will be reported as prototype evidence, not as proof of real-world mentoring outcomes.

### 6.4 Metrics and baseline comparison

| Metric                     | Definition                                                                                                | Purpose                                                       |
| -------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Precision@5                | Relevant recommendations among the top five divided by the number of recommendations returned, up to five | Measures the relevance of the displayed shortlist             |
| Recall@5                   | Relevant eligible mentors in the top five divided by all relevant eligible mentors for a test case        | Measures how many relevant candidates appear in the shortlist |
| NDCG@5                     | Ranking-quality metric that gives greater weight to relevant candidates placed higher                     | Evaluates the ordering of recommendations                     |
| Eligibility violation rate | Ineligible recommendations divided by all recommendations                                                 | Checks whether hard constraints are respected                 |
| Recommendation coverage    | Test cases for which the method returns at least one eligible recommendation divided by all test cases    | Measures how often the system can produce a shortlist         |
| Coordinator decision time  | Time needed to review a shortlist and record a decision                                                   | Explores whether recommendations may reduce review effort     |

Precision@5, Recall@5, and NDCG@5 will be calculated on the same evaluation cases for both approaches. If relevance labels are unavailable for a case, it will be excluded from relevance-metric calculations and reported separately.

### 6.5 Acceptance criteria

The following criteria will be used to assess the matching prototype:

- Both methods must respect all hard eligibility and safeguarding constraints.
- The rule-based baseline must reproduce its expected rankings on the reference test dataset.
- AI-assisted matching must be evaluated using the same test cases and relevance labels as the baseline.
- All metrics and implementation settings must be documented and reproducible.
- Differences in Precision@5, Recall@5, and NDCG@5 must be reported, including cases where the AI method performs worse.
- The AI approach will be considered promising if it improves ranking relevance without increasing eligibility violations or compromising safeguarding requirements.

No numerical improvement in AI performance will be claimed before the experiments are conducted. If the AI approach does not outperform the baseline, the result will be reported and used to discuss the limitations of the method and dataset.

## 7. Measurement Conditions and Reproducibility

To make the evaluation reproducible, the project team will record:

- Application version, Git commit, and test execution date.
- Operating system, hardware, runtime, and database configuration.
- Dataset size, synthetic profile-generation method, and evaluation labels.
- Test tools, configuration, and exact workload for performance tests.
- Matching algorithm, feature weights, embedding model, and relevant parameters.
- Test cases, expected results, actual results, failures, and corrective actions.

For performance tests, the team will use a fixed workload and report the number of concurrent users or requests, duration, response-time distribution, and error rate. Performance measurements from a local development environment will not be presented as production cloud performance.

For AI tests, all compared methods will run against the same fixed evaluation dataset. Where random initialization or sampling is used, random seeds and configuration will be recorded.

## 8. Evaluation of Project Objectives

| Project objective                                            | Evidence of achievement                                                                                                      |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Provide structured mentor recruitment and screening          | Successful tests of application submission, review decisions, and mentor eligibility                                         |
| Support safer and more transparent mentor matching           | Correct application of hard constraints, explainable criterion scores, coordinator approval, and matching evaluation results |
| Enable communication and mentoring-session management        | Successful messaging, reporting, meeting scheduling, and record-visibility tests                                             |
| Support social adaptation and independent-living preparation | Demonstrated goal and skill-track workflows for housing, finance, documentation, and employment                              |
| Improve coordinator oversight                                | Correct inactivity alerts, complaint handling, and access to organization-specific records                                   |
| Protect users and their information                          | Passing authorization, privacy, and safeguarding tests                                                                       |
| Deliver a usable web platform                                | Task-completion rates, completion times, participant feedback, and resolution of critical usability issues                   |

The platform's immediate technical objectives will be assessed through testing of implemented features. Long-term social outcomes, such as improved independent-living skills, sustained mentoring relationships, employment, or housing stability, cannot be established through a short diploma prototype evaluation alone. They would require an appropriately designed longitudinal study with participating organizations.

## 9. Reporting and Final Acceptance

The final evaluation report will contain:

1. A requirement-to-test traceability matrix.
2. Functional and non-functional test results.
3. Security and privacy test findings.
4. Usability metrics and participant feedback.
5. A baseline-versus-AI matching comparison table.
6. Known limitations, unresolved non-critical defects, and recommendations for future work.

The project will be accepted for demonstration when mandatory acceptance tests pass, critical safeguarding and security issues are resolved, the implemented functionality matches its documented scope, and all evaluation results are reported transparently.

The results will distinguish between verified functionality, experimentally measured performance, and expected long-term benefits that remain outside the scope of the prototype evaluation.
