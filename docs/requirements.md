# Initial Platform Requirements

**Project:** Development of a Peer-to-Peer Skill Exchange Platform for University Students  
**Task:** SSE-6  
**Status:** Initial requirements for team review

## 1. Purpose and scope

This document defines the initial functional and non-functional requirements for the first version of Student Skill Exchange. The first version supports the journey from registration to an agreed peer-learning exchange between two university students.

Built-in chat, video calls, payments, native mobile applications, machine-learning recommendations, certificates, formal skill assessment, group classes, and a course marketplace are outside the first-version scope.

## 2. Sources and validation status

| Code | Source or status |
|---|---|
| **P1** | [Project proposal](project-proposal.md): approved scope, objectives, main scenario, and engineering constraints. |
| **R1** | [Literature review](research/literature-review.md): rationale for transparent matching, user control, trust, and usable peer-learning interactions. |
| **T1** | [Technology comparison](architecture/technology-comparison.md): selected web stack, REST API, PostgreSQL, and security baseline. |
| **Y1** | [YouTrack task SSE-6](https://student-skill-exchange.youtrack.cloud/issue/SSE-6): required coverage and acceptance criteria. |
| **A1** | **Assumption — pending validation through SSE-2:** students are willing to create profiles and use reciprocal skill matching. |
| **A2** | **Assumption — pending validation through SSE-2:** email and password are acceptable credentials for the first version. |
| **A3** | **Assumption — pending validation through SSE-2:** the proposed profile fields, filters, and exchange-detail fields are sufficient. |
| **A4** | **Assumption — pending validation through SSE-2 and usability testing:** the usability and performance targets below are appropriate for target users. |

Requirements marked **Scope-backed** come from the reviewed project scope. Requirements marked **Assumption** must be reviewed after SSE-2; they must not be presented as validated user findings.

Priorities follow MoSCoW:

- **Must:** required for the first-version main scenario.
- **Should:** valuable for the first version but not required to demonstrate the complete main scenario.
- **Could:** optional if time permits.

## 3. Functional requirements

### 3.1 Registration and authentication

#### FR-AUTH-01 — Register an account

- **Priority:** Must
- **Status:** Scope-backed; credential choice is an Assumption
- **Requirement:** A visitor shall be able to register using a unique email address, password, and display name.
- **Acceptance criteria:**
  1. Valid unique details create one account and start an authenticated session or direct the user to sign in.
  2. Missing or malformed fields are rejected with field-specific messages.
  3. An email already assigned to an account is rejected without creating another account.
- **Source/rationale:** P1 main scenario and first-version scope; A2 for email/password choice.

#### FR-AUTH-02 — Sign in

- **Priority:** Must
- **Status:** Scope-backed; credential choice is an Assumption
- **Requirement:** A registered user shall be able to sign in with their email address and password.
- **Acceptance criteria:**
  1. Correct credentials create an authenticated session and open the application.
  2. Incorrect credentials do not create a session and produce a generic error that does not reveal whether the email exists.
  3. An authenticated user can access protected functions until the session expires or is ended.
- **Source/rationale:** P1 main scenario and access-control scope; A2 for email/password choice.

#### FR-AUTH-03 — Sign out

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** An authenticated user shall be able to sign out.
- **Acceptance criteria:** Signing out invalidates the current session and protected pages or API operations require authentication again.
- **Source/rationale:** P1 requirement for authentication and access control.

#### FR-AUTH-04 — Recover access

- **Priority:** Could
- **Status:** Assumption
- **Requirement:** A user may request a time-limited password-reset link for their registered email address.
- **Source/rationale:** Common account-recovery need; excluded from the mandatory main scenario until validated and scheduled.

### 3.2 Profiles

#### FR-PRO-01 — View and edit own profile

- **Priority:** Must
- **Status:** Scope-backed; exact fields are an Assumption
- **Requirement:** An authenticated user shall be able to view and edit their display name, short biography, and optional contact or study information approved for the first version.
- **Acceptance criteria:**
  1. Saved valid changes appear when the profile is reopened.
  2. Invalid values are rejected with field-specific messages.
  3. A user cannot edit another user's profile through either the interface or direct API requests.
- **Source/rationale:** P1 profile scope and access-control challenge; A3 for exact fields.

#### FR-PRO-02 — View another student's exchange profile

- **Priority:** Must
- **Status:** Scope-backed; visible fields are an Assumption
- **Requirement:** An authenticated user shall be able to open another student's profile and see the information needed to assess a possible exchange, including offered and wanted skills.
- **Acceptance criteria:** The profile displays only fields designated as visible to other authenticated users and never exposes authentication data or private internal identifiers.
- **Source/rationale:** P1 search and partner-selection scenario; R1 rationale for informed and trustworthy partner selection; A3 for visible fields.

### 3.3 Skills

#### FR-SKL-01 — Manage offered skills

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** A user shall be able to add and remove skills they can offer.
- **Acceptance criteria:**
  1. Added skills appear on the user's profile and are available to search and matching.
  2. Removing a skill removes it from future search and matching results without changing historical exchange records.
  3. The same offered skill cannot be added twice to one profile.
- **Source/rationale:** P1 proposed solution and first-version scope.

#### FR-SKL-02 — Manage wanted skills

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** A user shall be able to add and remove skills they want to learn.
- **Acceptance criteria:**
  1. Added skills appear on the user's profile and are available to matching.
  2. Removing a skill removes it from future matching results without changing historical exchange records.
  3. The same wanted skill cannot be added twice to one profile.
- **Source/rationale:** P1 proposed solution and first-version scope.

#### FR-SKL-03 — Use a consistent skill catalogue

- **Priority:** Must
- **Status:** Scope-backed; catalogue contents are an Assumption
- **Requirement:** Offered and wanted skills shall reference a shared skill catalogue so that equivalent skills can be searched and matched consistently.
- **Acceptance criteria:** Selecting the same catalogue skill on two different profiles stores the same skill identifier, and unsupported duplicate catalogue entries cannot be created through the public API.
- **Source/rationale:** P1 requirement to handle repeated skills and match complementary profiles; A3 for initial catalogue contents.

### 3.4 Search

#### FR-SRCH-01 — Search and filter students

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** An authenticated user shall be able to search for other students by offered skill and filter results by skill category.
- **Acceptance criteria:**
  1. Results contain only profiles that offer the selected skill and satisfy the selected category filter.
  2. The current user's own profile is not returned as a potential partner.
  3. Clearing the query or filters returns the documented default result state.
- **Source/rationale:** P1 first-version scope and main scenario.

#### FR-SRCH-02 — Explain empty search results

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** When no profiles match a search, the system shall display an empty state and allow the user to change or clear the filters.
- **Acceptance criteria:** A zero-result query shows no profile cards, displays a clear message, and provides an action that returns to a broader search.
- **Source/rationale:** P1 engineering challenge requiring clear handling when no suitable partner exists.

### 3.5 Partner matching

#### FR-MAT-01 — Generate reciprocal partner suggestions

- **Priority:** Must
- **Status:** Scope-backed; user value is an Assumption
- **Requirement:** The system shall suggest another user when the current user offers at least one skill the other user wants and the other user offers at least one skill the current user wants.
- **Acceptance criteria:**
  1. Every suggested pair satisfies both directions of the reciprocal rule using active offered and wanted skills.
  2. The current user is never suggested to themselves.
  3. Removing one side of the only reciprocal skill pair removes that suggestion after matching is recalculated.
- **Source/rationale:** P1 proposed solution and objectives; A1 for whether students value reciprocal matching.

#### FR-MAT-02 — Explain each suggestion

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** Each suggested partner shall show the offered and wanted skills that caused the reciprocal match.
- **Acceptance criteria:** For every suggestion, the interface displays at least one skill in each matching direction, and both displayed skills correspond to current profile data.
- **Source/rationale:** P1 first-version scope; R1 rationale for transparent, user-controllable matching.

#### FR-MAT-03 — Handle incomplete profiles and no matches

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** The system shall provide clear guidance when matching cannot run because skills are missing or when no reciprocal match exists.
- **Acceptance criteria:**
  1. A user with no offered or no wanted skill is prompted to complete the missing profile section.
  2. A completed profile with no reciprocal matches receives a distinct no-matches message and can continue to manual search.
- **Source/rationale:** P1 engineering challenges.

### 3.6 Exchange requests

#### FR-REQ-01 — Send an exchange request

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** An authenticated user shall be able to send another student an exchange request containing the proposed offered skill, wanted skill, and an optional short note.
- **Acceptance criteria:**
  1. A valid request creates one record with status `Pending` and identifies the sender and recipient.
  2. A user cannot send a request to themselves.
  3. A request cannot use a skill not present in the relevant participant's active profile data.
  4. A duplicate pending request for the same participants and skill pair is rejected.
- **Source/rationale:** P1 main user scenario and exchange-request scope.

#### FR-REQ-02 — View incoming and outgoing requests

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** A user shall be able to view their incoming and outgoing requests with participant, skill pair, current status, and creation time.
- **Acceptance criteria:** The two lists show only requests in which the authenticated user is the recipient or sender respectively, and their displayed status matches stored data.
- **Source/rationale:** P1 first-version scope.

#### FR-REQ-03 — Accept or decline a request

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** The recipient of a pending request shall be able to accept or decline it.
- **Acceptance criteria:**
  1. Only the recipient can accept or decline the request.
  2. A pending request changes exactly once to `Accepted` or `Declined`.
  3. Repeating the operation or applying it to a non-pending request is rejected without changing stored data.
- **Source/rationale:** P1 proposed solution and request-state engineering challenge.

#### FR-REQ-04 — Cancel a pending request

- **Priority:** Must
- **Status:** Scope-backed; transition rule defined here
- **Requirement:** The sender shall be able to cancel their request while it is pending.
- **Acceptance criteria:**
  1. Only the sender can cancel a pending request.
  2. Cancellation changes the status to `Cancelled`.
  3. Accepted, declined, or already cancelled requests cannot be cancelled again.
- **Source/rationale:** P1 states that requests can be cancelled according to rules defined in the requirements.

#### FR-REQ-05 — Preserve request status history

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** The system shall record each request status change with the new status, responsible user, and timestamp.
- **Acceptance criteria:** Creating, accepting, declining, or cancelling a request creates a corresponding immutable history entry, and only the two participants can view that history.
- **Source/rationale:** P1 first-version scope and requirement for consistent request information.

### 3.7 Agreed exchange details

#### FR-AGR-01 — Record agreed details

- **Priority:** Must
- **Status:** Scope-backed; exact fields are an Assumption
- **Requirement:** After a request is accepted, either participant shall be able to record the agreed topic, date and time, and format (`In person` or `External online service`), with an optional location or meeting link as appropriate.
- **Acceptance criteria:**
  1. Details can be created only for an accepted request and by one of its participants.
  2. Topic, future date and time, and format are required.
  3. The location or meeting-link field is validated according to the selected format.
  4. Saved details are visible to both participants.
- **Source/rationale:** P1 proposed solution and main scenario; A3 for exact fields.

#### FR-AGR-02 — Update agreed details

- **Priority:** Must
- **Status:** Scope-backed; collaboration rule is an Assumption
- **Requirement:** Either participant shall be able to update the agreed details, and the system shall show when they were last updated and by whom.
- **Acceptance criteria:**
  1. Only the two participants can update the details.
  2. Valid changes are visible to both participants after saving.
  3. The last-updated timestamp and responsible participant change with every successful update.
- **Source/rationale:** P1 requirement that both participants see consistent agreed details; A3 for the update workflow.

#### FR-AGR-03 — Keep sessions outside the platform

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** The first version shall direct users to conduct the learning session in person or through an external service and shall not provide built-in chat or video calls.
- **Acceptance criteria:** No built-in chat or video-call function appears in the first-version navigation or API, while the agreed format and optional external meeting information can be recorded.
- **Source/rationale:** P1 explicit scope exclusions.

## 4. Non-functional requirements

### 4.1 Security and privacy

#### NFR-SEC-01 — Protect passwords

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** Passwords shall be processed only by the backend and stored using a maintained adaptive password-hashing algorithm with a unique salt.
- **Acceptance criteria:** Database inspection shows no plaintext or reversibly encrypted passwords; automated authentication tests confirm that password verification succeeds only for the correct password.
- **Source/rationale:** P1 authentication and access-control scope; T1 security baseline.

#### NFR-SEC-02 — Enforce authentication and object-level authorization

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** Every protected API operation shall verify authentication and permission for the specific profile, request, or agreement being accessed.
- **Acceptance criteria:** Automated tests cover every protected endpoint: unauthenticated access returns `401`, and authenticated cross-user access outside the permitted relationship returns `403` or a non-disclosing `404`.
- **Source/rationale:** P1 engineering challenges; T1 security baseline.

#### NFR-SEC-03 — Validate untrusted input

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** The backend shall validate all request parameters and bodies against defined schemas and use parameterised database access.
- **Acceptance criteria:** Invalid type, length, format, and unexpected-field tests are rejected with `4xx` responses; automated security tests confirm common SQL-injection strings are treated as data and do not alter query structure.
- **Source/rationale:** T1 selected REST/PostgreSQL security responsibilities.

#### NFR-SEC-04 — Protect transport and secrets

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** Non-local deployments shall use HTTPS, and credentials or signing secrets shall be supplied through protected environment configuration rather than committed files.
- **Acceptance criteria:** The deployed HTTP endpoint redirects to HTTPS or is unavailable; repository secret scanning finds no active credentials; production cookies, if used, have `Secure`, `HttpOnly`, and an explicit `SameSite` policy.
- **Source/rationale:** T1 security and deployment baseline.

#### NFR-SEC-05 — Limit authentication abuse

- **Priority:** Must
- **Status:** Assumption
- **Requirement:** Login attempts shall be rate-limited to no more than 10 failed attempts for the same account or client address within 15 minutes.
- **Acceptance criteria:** An automated test shows that attempts beyond the configured threshold receive `429 Too Many Requests` and that access becomes available after the limit window expires.
- **Source/rationale:** T1 Express security baseline; threshold requires review after testing.

#### NFR-SEC-06 — Minimise exposed personal data

- **Priority:** Must
- **Status:** Scope-backed; exact visible fields are an Assumption
- **Requirement:** API responses and screens shall expose only the profile fields required for finding and arranging an exchange.
- **Acceptance criteria:** Public profile responses exclude password hashes, session data, private configuration, and email unless the visibility decision explicitly permits it; API contract tests verify the approved response schema.
- **Source/rationale:** P1 target-user scenario; R1 trust rationale; A3 for final visible fields.

### 4.2 Usability and accessibility

#### NFR-USA-01 — Complete the main scenario

- **Priority:** Must
- **Status:** Assumption
- **Requirement:** At least 80% of five representative university-student test participants shall complete registration, skill setup, partner discovery, request submission, request acceptance, and recording agreed details without moderator assistance.
- **Acceptance criteria:** A documented usability test records at least four successful completions out of five participants and lists failures or required corrections.
- **Source/rationale:** P1 main scenario and evaluation objective; A4 target pending user research and evaluation planning.

#### NFR-USA-02 — Provide clear system feedback

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** Forms and asynchronous actions shall show validation errors, loading state, success confirmation, and recoverable error guidance where applicable.
- **Acceptance criteria:** A UI review of registration, login, profile, search, request, and agreement screens confirms that each applicable state is represented and that errors identify the affected action or field.
- **Source/rationale:** P1 frontend responsibilities and requirement to communicate incomplete/no-match cases clearly.

#### NFR-USA-03 — Support keyboard use and readable labels

- **Priority:** Must
- **Status:** Assumption
- **Requirement:** Core screens shall support keyboard navigation, visible focus, programmatic form labels, and text/background contrast conforming to WCAG 2.2 Level AA for the tested components.
- **Acceptance criteria:** Automated accessibility checks report no critical violations on core screens, and a manual keyboard test completes the main scenario without a mouse.
- **Source/rationale:** A4 usability assumption; inclusive access for the target student population.

### 4.3 Performance

#### NFR-PERF-01 — API response time

- **Priority:** Must
- **Status:** Assumption
- **Requirement:** Under 20 concurrent simulated users with a seeded dataset of at least 1,000 users and 10,000 user-skill relationships, the 95th-percentile response time shall be at most 500 ms for profile and request operations and at most 1,000 ms for search and reciprocal matching.
- **Acceptance criteria:** A repeatable load-test report from the documented test environment meets both 95th-percentile targets with an API error rate below 1%.
- **Source/rationale:** A4 initial measurable target; P1 requires usable search and matching.

#### NFR-PERF-02 — Core page loading

- **Priority:** Should
- **Status:** Assumption
- **Requirement:** On the agreed staging environment, each core page should achieve a Largest Contentful Paint of at most 2.5 seconds in a documented Lighthouse mobile test.
- **Source/rationale:** A4 initial usability/performance target; selected static frontend in T1.

### 4.4 Compatibility and responsive design

#### NFR-COM-01 — Browser compatibility

- **Priority:** Must
- **Status:** Assumption
- **Requirement:** The main scenario shall work in the latest two stable major versions available at test time of Chrome, Firefox, Edge, and Safari.
- **Acceptance criteria:** A compatibility matrix records a passing main-scenario test for every listed browser/version combination, or records and resolves any blocking difference before release.
- **Source/rationale:** A4 compatibility target for a browser-based university platform.

#### NFR-COM-02 — Responsive web interface

- **Priority:** Must
- **Status:** Scope-backed; dimensions are an Assumption
- **Requirement:** Core screens shall remain usable at viewport widths from 360 px to 1440 px without unintended horizontal scrolling or hidden primary actions.
- **Acceptance criteria:** Registration, login, profile, search, recommendations, requests, and agreement screens pass manual checks at 360, 768, 1024, and 1440 px widths.
- **Source/rationale:** P1 requires a web interface adapted for desktop and mobile screens; A4 for chosen test widths.

### 4.5 Reliability and maintainability

#### NFR-REL-01 — Preserve request consistency

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** Exchange-request status changes and their history entries shall be committed atomically.
- **Acceptance criteria:** Integration tests show that an induced failure cannot leave a changed request status without its history entry, or a history entry without the corresponding status change.
- **Source/rationale:** P1 consistency challenge; PostgreSQL transaction decision in T1.

#### NFR-MNT-01 — Maintain the API contract

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** The implemented HTTP API shall have a versioned OpenAPI document consistent with its request schemas, responses, authentication rules, and error codes.
- **Acceptance criteria:** The OpenAPI document passes schema validation, and automated contract tests fail when the implementation no longer matches the documented endpoints used by the main scenario.
- **Source/rationale:** P1 expected API documentation; T1 selected OpenAPI contract.

#### NFR-MNT-02 — Verify mandatory requirements

- **Priority:** Must
- **Status:** Scope-backed
- **Requirement:** Every Must requirement in this document shall be traceable to at least one automated test, manual test case, or review record before the first-version evaluation.
- **Acceptance criteria:** A traceability table lists every Must requirement ID with evidence and contains no empty evidence field at release review.
- **Source/rationale:** Y1 requires clear, verifiable acceptance criteria; P1 includes testing and evaluation objectives.

## 5. Business rules and state model

### 5.1 Exchange-request states

| Current state | Allowed action | Actor | New state |
|---|---|---|---|
| No request | Send valid request | Sender | Pending |
| Pending | Accept | Recipient | Accepted |
| Pending | Decline | Recipient | Declined |
| Pending | Cancel | Sender | Cancelled |
| Accepted | Record or update agreement | Either participant | Accepted |
| Declined | None | — | Declined |
| Cancelled | None | — | Cancelled |

Terminal requests are retained for history. A new request for the same users and skill pair may be considered only after the previous request is no longer pending; whether a waiting period is needed remains an assumption for later validation.

### 5.2 Matching rule

For current user `A`, user `B` is a reciprocal match when:

1. `A` and `B` are different active users;
2. at least one active skill offered by `A` is wanted by `B`; and
3. at least one active skill offered by `B` is wanted by `A`.

The interface must show the skills satisfying conditions 2 and 3. Ranking beyond the existence of a reciprocal match is outside the mandatory first-version requirement and may be defined after user research.

## 6. Traceability summary

| Required area from SSE-6 | Requirement IDs |
|---|---|
| Registration and authentication | FR-AUTH-01–04 |
| Profiles | FR-PRO-01–02 |
| Skills | FR-SKL-01–03 |
| Search | FR-SRCH-01–02 |
| Partner matching | FR-MAT-01–03 |
| Exchange requests | FR-REQ-01–05 |
| Agreed exchange details | FR-AGR-01–03 |
| Security | NFR-SEC-01–06 |
| Usability | NFR-USA-01–03 |
| Performance | NFR-PERF-01–02 |
| Compatibility | NFR-COM-01–02 |
| Reliability and maintainability | NFR-REL-01, NFR-MNT-01–02 |

## 7. Assumption review after SSE-2

After the student research task is completed, the team shall review A1–A4 and record one of the following for every affected requirement:

- **Validated:** supported by collected evidence;
- **Revised:** changed to reflect collected evidence; or
- **Rejected:** removed from the planned scope with a recorded reason.

The review should specifically check credential preferences, profile information, skill terminology, useful search filters, willingness to use reciprocal matching, exchange-request expectations, agreement fields, and the practicality of the usability targets.

## 8. Team agreement

Agreement will be recorded through review and approval of the pull request for SSE-6.

- [ ] Nursultan Makhmutov confirms that the requirements fit the first-version scope.
- [ ] Tamir Burlibaev confirms that the requirements fit the first-version scope.

The approved pull request URL will be added to [SSE-6](https://student-skill-exchange.youtrack.cloud/issue/SSE-6).
