# Requirements Specification

## 1. Purpose and scope

This document defines what the mentoring and social adaptation platform must do (functional requirements) and how well it must do it (non-functional requirements). It covers user accounts, roles and permissions, mentor discovery and matching, communication, mentoring sessions, notifications and the planned AI functionality.


### 1.1 How to read a requirement

| Field | Meaning |
|---|---|
| **ID** | Unique and stable. `FR-xx` is functional, `NFR-xx` is non-functional. An ID is never reused for a different requirement. |
| **Priority** | MoSCoW. **M** (must) is mandatory for the diploma release. **S** (should) is important but the release is acceptable without it. **C** (could) is desirable if time allows. **W** (won't) is out of scope for this release and listed so the boundary is explicit. |
| **Acceptance criterion** | A condition that is either met or not met. Written as *Given / When / Then* or as a numeric threshold. |
| **Verify** | How fulfilment is checked: **T** automated test (unit, API or end-to-end), **L** load or performance test, **S** security scan or security test, **I** inspection of code, configuration or logs, **U** usability test with participants. |

A mandatory (M) requirement counts as fulfilled only when every part of its acceptance criterion passes. Every M requirement has at least one automated check (T, L or S) unless the Verify column says otherwise.

### 1.2 Roles

| Role | Who | Key constraint |
|---|---|---|
| **Mentee (minor)** | Orphanage resident or boarding school graduate aged 14–17 | Account is created only by a coordinator, after guardian or institution consent is recorded |
| **Mentee (adult)** | Graduate aged 18–23 | May self-register; activated by a coordinator of their organisation |
| **Mentor** | Adult volunteer (18+) | States: `applicant` → `under_review` → `approved` / `rejected` / `suspended`. Only `approved` mentors can be matched or contacted |
| **Coordinator** | Staff of a partner NGO or orphanage | Sees only the data of their own organisation; makes every pairing decision |
| **Administrator** | Technical administrator of the platform | Manages organisations, accounts and settings; does not read chat content |

Each user has exactly one role. A user belongs to exactly one organisation, except the administrator.

## 2. Functional requirements

### 2.1 User accounts

| ID | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|
| FR-01 | Users can register and sign in with email and password. Each account has exactly one role: mentee, mentor, coordinator or administrator. | M | Given a registered user of each role, when they sign in with valid credentials, then they receive a session and see only the navigation sections of their role (one automated test per role). Invalid credentials return a generic error that does not reveal whether the email exists. | T |
| FR-02 | A mentee under 18 can be registered only by a coordinator. | M | Given the self-registration form, when a birth date under 18 is entered, then registration is rejected with an explanation and no account is created. Given a coordinator, when they register a 15-year-old mentee, then the account is created in the coordinator's organisation. | T |
| FR-13 | For a mentee under 18, consent from the legal guardian or the institution is recorded before the account is activated. | M | Given a minor's account without a consent record, when anyone tries to activate it or add it to a pair, then the action is rejected. Given a consent record (who gave it, date, scanned document or reference number), activation succeeds. | T |
| FR-14 | Email verification and password reset by a one-time link. | M | A new self-registered account cannot sign in until the email is verified. A reset link works once and expires after 60 minutes; a second use or a late use is rejected. | T |
| FR-15 | Users can view and edit their own profile (name, city, interests, availability, preferred language, "about me"). Birth date and role can be changed only by a coordinator or administrator. | M | Given a mentee, when they change their interests, then the change is saved and used by the next matching run. When they try to change their birth date or role through the API, then the request is rejected with 403. | T |
| FR-16 | A coordinator can deactivate an account; the user can request deletion of their data. | S | Given a deactivated account, sign-in fails and the user disappears from matching results. A deletion request appears in the coordinator's queue and, once confirmed, personal fields are anonymised within 30 days (see NFR-11). | T |

### 2.2 Roles and permissions

| ID | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|
| FR-17 | Every API operation checks the user's role on the server according to the permission matrix in section 2.2.1. | M | For every endpoint, an automated test calls it as each of the five roles (minor mentee, adult mentee, mentor, coordinator, administrator) and as an unauthenticated client; 100% of the results match the matrix. | T, S |
| FR-18 | Data is isolated by organisation and by pair: a coordinator sees only their organisation; a mentor sees a mentee only while they share an active pair. | M | Given coordinator A of organisation 1, when they request a pair, profile or chat of organisation 2 (including by changing an ID in the URL), then the response is 403 or 404 and no data is returned. Given a mentor whose pair has ended, when they open the mentee's profile, then access is denied. | T, S |
| FR-19 | The administrator manages organisations, coordinator accounts and role assignments. | M | Given an administrator, when they create an organisation and a coordinator for it, then the coordinator can sign in and sees an empty organisation. Every role change is written to the audit log with author, old role, new role and time. | T |
| FR-20 | Coordinators can enable a second sign-in factor (one-time code); the administrator can make it mandatory for coordinators. | C | When the setting is on, a coordinator who enters only a password cannot reach any coordinator page. | T |

#### 2.2.1 Permission matrix

R = read, W = create or change, own = only own records, pair = only within own active pair, org = only within own organisation, — = no access.

| Resource | Mentee | Mentor | Coordinator | Administrator |
|---|---|---|---|---|
| Own profile | R W | R W | R W | R W |
| Mentee profiles | own | pair (R) | org (R W) | — (account fields only) |
| Mentor application and documents | — | own (R W) | org (R, decision) | — |
| Matching recommendations | — | — | org | — |
| Pairs | own (R) | own (R) | org (R W) | — |
| Chat messages | pair (R W) | pair (R W) | org (R, moderate) | — |
| Meetings and notes | pair (R W); notes R only if shared | pair (R W) | org (R) | — |
| Goals and skill tracks | own (R W) | pair (R) | org (R W) | — |
| Complaints | own (W, R own) | own (W, R own) | org (R W) | — |
| Audit log | — | — | org (R) | R |
| Organisations, roles, settings | — | — | — | R W |

### 2.3 Mentor discovery and matching

| ID | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|
| FR-03 | A mentor applicant fills in a questionnaire (motivation, experience, interests, city, format, availability) and uploads a criminal record certificate. The application has a visible review status. | M | Given an applicant, when they submit the form without the certificate, then submission is rejected. Given a submitted application, the applicant sees the status `under_review`. Given a mentor in any status other than `approved`, when a coordinator tries to put them in a pair, then the action is rejected. | T |
| FR-04 | The coordinator approves or rejects a mentor application with a comment. | M | When the coordinator approves or rejects, then a comment is required, the decision is stored with author and timestamp, and the applicant is notified (FR-12). A rejected mentor cannot be found in mentor search or recommendations. | T |
| FR-21 | The coordinator can browse and filter approved mentors of their organisation by city, meeting format (online, offline), interests, availability and free capacity. | M | Given a test set of 20 approved mentors, when the coordinator filters by city = Almaty and format = offline, then exactly the mentors that satisfy both filters are listed. Mentors in other statuses or organisations never appear. | T |
| FR-22 | A mentee can state matching preferences (interests, preferred format, preferred mentor gender, topics they need help with). Mentees do not browse or contact mentors directly. | S | Given a mentee with saved preferences, the next recommendation run uses them as filters or criteria (visible in the score breakdown). No API endpoint returns a list of mentors to a mentee. | T |
| FR-23 | Matching applies hard filters before scoring: mentor is `approved`, same organisation, same city or online format, at least one overlapping time slot, and number of active pairs below the mentor's limit (default 2). | M | Given a test dataset in which 5 mentors violate one filter each, when recommendations are requested, then none of those 5 mentors appears in the result. | T |
| FR-05 | For a selected mentee the coordinator receives the top 5 recommended mentors, ranked by a weighted score over interests, city, availability and preferences, with the score shown per criterion. | M | Given the reference test dataset (synthetic profiles with a precomputed expected ranking), when recommendations are requested, then the 5 mentors and their order match the reference and each result shows the per-criterion scores that sum to the total. | T |
| FR-24 | The coordinator can change the criterion weights for their organisation. | S | When the weight of "shared interests" is set to 0, then the ranking for the reference dataset changes to the reference ranking computed without that criterion. | T |
| FR-06 | The coordinator creates, pauses and ends a pair. The coordinator chooses the mentor; the system never creates a pair by itself. | M | When a pair is created, both participants are notified and the chat opens. When a pair is paused, messages cannot be sent. When a pair is ended, both participants lose chat access, and the reason is stored. There is no code path that creates a pair without a coordinator action (checked by test and code inspection). | T, I |

### 2.4 Communication

| ID | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|
| FR-07 | Mentor and mentee of an active pair exchange text messages in an in-platform chat. The coordinator of the organisation can view the chat, and both participants are told so before the first message. | M | Given an active pair, a message sent by one participant appears for the other (latency in NFR-12). Given a new pair, the chat shows a moderation notice that must be acknowledged before the first message can be sent. Given a coordinator of the organisation, they can open the chat history. | T |
| FR-25 | Users can message only the other member of their own active pair; there is no direct messaging between arbitrary users. | M | Given a mentor, when they try to send a message to a mentee who is not in their active pair (through the UI or API), then the request is rejected with 403 and nothing is stored. | T, S |
| FR-08 | A "Report a problem" button is available in the chat and in the profile. A report reaches the coordinator marked as urgent. | M | Given a mentee, when they submit a report (with or without text), then a complaint with status `new` and flag `urgent` is created, the coordinators receive a safety notification (section 2.6.1), and the reporter sees a confirmation. The reported user is not notified. | T |
| FR-26 | The coordinator can handle a complaint: change its status (`new`, `in_progress`, `resolved`), add notes, hide a message, and pause the pair. | M | When the coordinator hides a message, then neither participant sees it and the original stays available to the coordinator. Every status change is logged with author and time. | T |
| FR-27 | The chat warns users when a message contains a phone number, a messenger handle or an external link, and reminds them that communication should stay on the platform. | C | Given the message "write me on +7 701 123 4567", when it is sent, then the sender sees a warning and the message is flagged for the coordinator. | T |
| FR-28 | Participants can attach images or PDF files to chat messages. | C | Files over 10 MB or of other types are rejected; accepted files are stored privately (NFR-16). | T |

### 2.5 Mentoring sessions

| ID | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|
| FR-09 | A participant of an active pair schedules a meeting (date, time, duration, format, place or video link). The meeting appears for both participants and a reminder is sent 24 hours before. | M | Given a meeting scheduled for tomorrow at 15:00, then it appears in both participants' calendars, and reminder notifications are created between 14:55 and 15:05 today (scheduler test with a controlled clock). | T |
| FR-29 | A meeting has a status: `proposed`, `confirmed`, `held`, `cancelled`, `missed`. The other participant confirms or declines a proposed meeting. | M | Given a proposed meeting, when the mentee confirms, then the status becomes `confirmed` and the mentor is notified. A meeting whose end time has passed without a status update is shown to the mentor as "awaiting outcome". | T |
| FR-30 | After a meeting the mentor records a short note (topic, outcome, any concern). Notes are visible to the coordinator; a note is visible to the mentee only if the mentor marks it as shared. | M | Given a held meeting without a note 48 hours after its end, the mentor receives a reminder. A note with the "concern" flag creates a safety notification for the coordinator. A mentee cannot read an unshared note through the UI or API. | T |
| FR-31 | After a meeting the mentee can give optional feedback: a 1–5 rating and a comment. | S | Feedback is stored for the meeting and visible only to the coordinator. Submitting no feedback does not block any action. | T |
| FR-10 | The mentee has personal goals and skill tracks (finance, housing, documents, work) with progress. | S | Given a track with 4 lessons, when the mentee completes the second lesson, then progress shows 50%. The mentor of the active pair can see the progress but cannot change it. | T |
| FR-11 | The coordinator dashboard lists the organisation's pairs with the date of last contact (message or held meeting) and highlights pairs inactive for 14 days or more. | S | Given a test pair whose last message and last held meeting are 14 days old, it appears in the alert list; a pair with a message 13 days ago does not. | T |

### 2.6 Notifications

| ID | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|
| FR-12 | The platform sends in-app and email notifications for the events in section 2.6.1. Users can turn off email for non-safety events but cannot turn off safety notifications. | M | Given a user who turned off email, when a meeting reminder is triggered, then only the in-app notification is created. When a safety event is triggered for a coordinator, then both channels are used regardless of preferences. The settings page shows safety notifications as locked. | T |
| FR-32 | An in-app notification centre shows notifications with read/unread state, newest first. | M | Given 3 unread notifications, the counter shows 3; after opening one, it shows 2. | T |
| FR-33 | Urgent safety notifications (complaint, flagged note, flagged message) are escalated: if no coordinator acknowledges within 24 hours, the notification is sent to all coordinators of the organisation and to the administrator. | S | Given an urgent complaint not acknowledged for 24 hours (controlled clock), then escalation notifications are created for every coordinator of the organisation and the administrator. | T |
| FR-34 | Optional SMS or push channel for urgent safety notifications. | C | When the channel is configured, an urgent notification is passed to the gateway; when it is not configured, nothing fails and email is used. | T |

#### 2.6.1 Notification events

| Event | Recipients | Channels | Safety (cannot be turned off) |
|---|---|---|---|
| Mentor application approved or rejected (FR-04) | Applicant | In-app, email | No |
| Pair created, paused or ended (FR-06) | Mentor, mentee | In-app, email | No |
| New chat message (FR-07) | Other participant | In-app (email digest if unread for 12 h) | No |
| Meeting proposed, confirmed, cancelled (FR-29) | Other participant | In-app, email | No |
| Meeting reminder 24 h before (FR-09) | Both participants | In-app, email | No |
| Meeting note missing after 48 h (FR-30) | Mentor | In-app | No |
| Complaint submitted (FR-08) | Coordinators of the organisation | In-app, email, SMS/push if configured | **Yes** |
| Note or message flagged as a concern (FR-27, FR-30) | Coordinators of the organisation | In-app, email | **Yes** |
| Pair inactive for 14 days (FR-11) | Coordinator | In-app | No |
| Escalation of an unacknowledged urgent item (FR-33) | All coordinators, administrator | In-app, email | **Yes** |
| Password reset, email verification (FR-14) | User | Email | **Yes** |

### 2.7 Planned AI functionality

AI features extend the weighted matching in FR-05 and are planned after the baseline works. Their priority is S or C, but the safety constraints FR-37 to FR-40 are **mandatory whenever any AI feature is enabled**: an AI feature may not be switched on in a release where these constraints fail.

| ID | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|
| FR-35 | Semantic ranking: profile texts (interests, goals, "about me") are converted to embeddings, and candidates that pass the hard filters (FR-23) are re-ranked by a combination of the weighted score and cosine similarity. | S | Given the reference dataset with expected semantic matches (for example "wants to become a programmer" and "software developer"), the expected mentor is in the top 5 in at least 8 of 10 reference cases. | T |
| FR-36 | An LLM re-ranks the top candidates and writes a short justification (at most 300 characters) for each of the top 5, shown next to the per-criterion scores and labelled "AI suggestion". | C | Every recommendation produced with the LLM shows the label and a justification of at most 300 characters. A justification that mentions a fact not present in either profile counts as an error; on the reference dataset, at most 1 of 50 justifications is an error (manual review). | T, I |
| FR-37 | **Human decision.** AI output is advisory only. The coordinator chooses the mentor and confirms the pair; the system never creates, changes or ends a pair, approves a mentor or rejects a mentee based on AI output alone. | M (if AI enabled) | Given AI recommendations, no pair exists until the coordinator presses "Create pair". Code inspection shows that the matching module has no write access to pairs or applications. When the coordinator chooses a mentor outside the AI top 5, the action succeeds and an optional reason is stored. | T, I |
| FR-38 | **Data minimisation for external AI services.** Only pseudonymised interest and goal text is sent to an external LLM or embedding API. Names, contacts, birth dates, documents, chat messages and meeting notes are never sent. | M (if AI enabled) | An automated test captures all outgoing requests to the AI provider during a matching run and checks that none contains the test names, emails, phone numbers, birth dates or document identifiers. | T, I |
| FR-39 | **Minors.** No personal data of mentees under 18 is sent to an external LLM or embedding API. For them, matching uses the weighted baseline or a self-hosted embedding model. Sending minors' data to an external provider would require a separate, approved data protection plan and is out of scope for this release. | M (if AI enabled) | Given a 16-year-old mentee, when recommendations are requested, then zero requests are made to the external AI provider (checked with a mock that fails the test on any call) and the results are still returned. | T |
| FR-40 | **Fallback.** If the AI service is unavailable or does not answer within 5 seconds, the coordinator gets the weighted baseline result (FR-05) with a notice that AI ranking was not used. | M (if AI enabled) | Given a mocked AI provider that times out, when recommendations are requested, then the baseline top 5 is returned within the NFR-13 limit and the notice is shown. | T |
| FR-41 | **Evaluation log.** Each recommendation run stores the candidates, scores, whether AI was used, and which mentor the coordinator finally chose. | S | After 10 test runs, a report shows the share of pairs where the chosen mentor was in the top 5 (agreement rate), separately for AI and baseline runs. | T |
| FR-42 | The administrator can switch AI features on or off per organisation. | S | When AI is off, no request reaches the AI provider and the UI shows only baseline scores. | T |
| FR-43 | AI does not analyse chat messages, does not chat with mentees and does not make safeguarding decisions. | W | Out of scope for this release; listed to make the boundary explicit. | — |

### 2.8 Out of scope (won't have in this release)

- Native iOS and Android apps (the web client is responsive instead, NFR-04).
- Built-in video calls; the platform stores only a link to an external service (FR-09).
- Automatic pairing without a coordinator (excluded by FR-37).
- AI analysis of chat content or AI chat with mentees (FR-43).
- Payments or donations.

## 3. Non-functional requirements

| ID | Category | Requirement | Priority | Acceptance criterion | Verify |
|---|---|---|---|---|---|
| NFR-01 | Security | Passwords hashed with Argon2id (or bcrypt); HTTPS only; short-lived access tokens with refresh rotation; sign-in rate limited. | M | Inspection shows no plain or reversible passwords in the database. HTTP requests are redirected to HTTPS. Access tokens expire after at most 15 minutes. After 5 failed sign-ins in 15 minutes, further attempts are throttled. An OWASP ZAP baseline scan of the test deployment reports 0 high-severity findings. | I, S, T |
| NFR-02 | Privacy | Personal data is processed according to the applicable personal data law [jurisdiction to confirm]. Every view of a minor's profile and every change to sensitive data is written to an audit log. | M | Given a coordinator opening a 15-year-old's profile, an audit record with user, record, action and time is created. The audit log cannot be edited or deleted through the application (API test). | T, I |
| NFR-03 | Performance | API responses are fast under expected load. | S | A load test with 100 concurrent virtual users over 10 minutes on the reference environment shows p95 response time under 500 ms and an error rate under 1%. | L |
| NFR-04 | Responsiveness | Key scenarios work on screens from 360 px wide. | M | End-to-end tests for sign-in, chat, scheduling a meeting and reporting a problem pass at 360×640 and at 1280×800, with no horizontal scrolling. | T |
| NFR-05 | Usability | Mentees (18+) and coordinators find the platform easy to use. | S | In a usability test with at least 5 participants, the mean System Usability Scale score is at least 68 ([R13](REFERENCES.md#academic-and-domain-sources)) and at least 80% of the tasks are completed without help. | U |
| NFR-06 | Localisation | Russian is the first interface language; Kazakh and English can be added without code changes. | S | Inspection finds no hard-coded UI strings outside translation files. Switching the language setting changes all labels on the tested screens. | I, T |
| NFR-07 | Accessibility | Contrast, labels and keyboard navigation follow WCAG 2.1 AA ([T6](REFERENCES.md#technical-sources)). | C | Lighthouse accessibility score of at least 90 on the 5 key pages; all form fields have labels. | T |
| NFR-08 | Access control | Broken access control (changing IDs to reach other users' data) is prevented. | M | The access-control test suite (FR-17, FR-18) runs in CI on every merge and passes 100%; a manual test of 10 endpoints with changed IDs returns no foreign data. | T, S |
| NFR-09 | Availability | The pilot deployment is available during the evaluation period. | S | Uptime of at least 99% per month, measured by an external health check on `/health`. | I |
| NFR-10 | Backup and recovery | Data can be restored after a failure. | M | Automatic daily database backup (data loss at most 24 hours). A restore into an empty environment completes in under 4 hours and the restored data passes a consistency check. | T, I |
| NFR-11 | Data retention | Data of ended pairs and deleted accounts is not kept longer than needed. | S | A scheduled job anonymises or deletes messages, notes and documents of pairs ended more than N months ago [N to agree with partner organisations]; a test with a controlled clock shows the records are removed. | T |
| NFR-12 | Real-time chat | Chat messages are delivered quickly and reliably. | M | With 50 active pairs sending messages, the time from send to display for the other participant is under 2 s for 95% of messages. If the real-time connection drops, messages are delivered after reconnection without loss. | L, T |
| NFR-13 | Matching response time | Recommendations return in time for interactive use. | S | Baseline matching (FR-05) over 500 mentors returns in under 1 s (p95). With AI ranking (FR-35, FR-36), the result or the fallback (FR-40) returns in under 10 s (p95). | L |
| NFR-14 | Explainability | Every recommendation can be explained to the coordinator. | M | Every item in the top 5 shows the score for each criterion; AI-assisted items also show the label and justification (FR-36). No recommendation is shown without a breakdown (UI test). | T |
| NFR-15 | Logging | Application logs support troubleshooting without exposing personal data. | M | Inspection of the logs produced by the full test suite finds no passwords, tokens, message texts or document contents; every request log line has a request ID. | I, T |
| NFR-16 | File security | Uploaded documents are stored privately and checked on upload. | M | Only PDF, JPG and PNG up to 10 MB are accepted. The storage bucket is not publicly readable. Documents are served only through signed links that expire after at most 5 minutes, and only to coordinators of the organisation. | T, S |
| NFR-17 | Maintainability | The code is testable and documented. | S | Automated test coverage of the business-logic layer is at least 70%. The API is described by an OpenAPI specification generated from the code. A linter runs in CI with zero errors. | T, I |
| NFR-18 | Portability | The platform can be started in a new environment in a repeatable way. | S | A new developer starts the whole system with one documented command (for example `docker compose up`) and the end-to-end smoke test passes. Configuration comes from environment variables; no secrets are stored in the repository. | T, I |
| NFR-19 | Compatibility | The web client works in current browsers. | S | End-to-end tests pass in the latest versions of Chromium, Firefox and WebKit (Safari engine). | T |
| NFR-20 | Scalability | The design supports growth beyond the pilot. | C | A load test with 1,000 registered users across 10 organisations and 500 active pairs meets the NFR-03 and NFR-12 thresholds. | L |

## 4. Summary by priority

| Priority | Functional | Non-functional | Total |
|---|---|---|---|
| M (must) | 27 (4 of them apply when AI is enabled) | 9 | 36 |
| S (should) | 10 | 9 | 19 |
| C (could) | 5 | 2 | 7 |
| W (won't) | 1 | 0 | 1 |
| **Total** | **43** | **20** | **63** |

## 5. Security and Maintainability

### 5.1 Security Updates

**Aligned with NFR-01**

Passwords must be hashed using Argon2id or bcrypt. The platform must enforce HTTPS, use short-lived access tokens with refresh-token rotation, and implement sign-in rate limiting.

### 5.2 API Documentation and Maintainability

**Aligned with NFR-17**

The API must be documented using an OpenAPI specification generated directly from the code. Automated test coverage of the business-logic layer must reach at least 70%. A linter must run in the CI pipeline with zero errors.

### 5.3 Portability and Deployment

**Aligned with NFR-18**

The platform must support repeatable environment setup through containerization, for example, using `docker compose up`. Configuration must be managed through environment variables, and no secrets may be stored in the repository.

## 6. Final Technology Selection: AI Integration

### 6.1 AI and Embedding Support

**Aligned with FR-35, FR-38, and FR-39**

If AI features, such as semantic ranking or LLM-based justifications, are enabled, the technology stack must support integration with external or self-hosted embedding and large language model (LLM) APIs.

The implementation must enforce the data-minimisation requirements defined in the functional requirements:

- Personal data of mentees under 18 must not be sent to external AI providers.
- Names, contact details, birth dates, documents, chat messages, and meeting notes must not be sent to external AI services.
- Only permitted pseudonymised interest and goal text may be transmitted to an external provider.
- If external AI services are unavailable, the system must fall back to the weighted baseline matching approach, as specified in FR-40.


6. Final Technology Selection (AI Integration Additions)
AI and Embedding Support (Aligned with FR-35, FR-38, FR-39): If AI features (such as semantic ranking or LLM-based justifications) are enabled, the technology stack must support integration with external or self-hosted embedding/LLM APIs while strictly enforcing data minimization constraints (e.g., ensuring personal data of minors and sensitive profile details are not sent to external providers)
