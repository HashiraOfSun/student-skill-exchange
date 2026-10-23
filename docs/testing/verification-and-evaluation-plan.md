# Verification and Evaluation Plan

**Project:** Development of a Peer-to-Peer Skill Exchange Platform for University Students  
**Task:** SSE-9  
**Status:** Planned; no tests in this document have been executed  
**Owner:** Nursultan Makhmutov  
**Required reviewer:** Tamir Burlibaev

## 1. Purpose

This document defines how the Student Skill Exchange MVP will be verified against its mandatory requirements and how the team will evaluate whether reciprocal matching helps university students find a suitable learning partner.

The plan is based on the [initial platform requirements](../requirements.md) and the [system architecture](../architecture/system-architecture.md). It covers the first-version journey from registration to recorded exchange details. Built-in chat, video calls, payments, native mobile applications, machine-learning recommendations, certificates, and formal skill assessment remain outside scope.

## 2. Test status and evidence policy

Everything described here is **planned**. No pass, fail, performance, accessibility, compatibility, or usability result is claimed yet.

During implementation and evaluation, each execution record shall contain:

- test-case ID and requirement ID;
- application version or commit SHA;
- date, tester, environment, browser, and viewport where relevant;
- test data used;
- expected and actual result;
- pass, fail, blocked, or not-run status;
- defect link and retest evidence when applicable.

Automated reports, screenshots, compatibility matrices, usability notes, and defect links will be stored under `docs/testing/evidence/` or linked from the final report. Personal participant data shall not be committed.

## 3. Verification strategy

| Level | Purpose | Planned evidence |
|---|---|---|
| Unit tests | Verify matching rules, validation, and request-state rules in isolation | Test-run report with commit SHA |
| API integration tests | Verify database behaviour, authorization, transactions, and HTTP responses | API test report and seeded database version |
| Contract tests | Verify implementation against OpenAPI schemas, authentication rules, and error codes | OpenAPI validation and contract-test report |
| End-to-end tests | Verify successful and unsuccessful user journeys through the browser | Browser test report, screenshots for failures |
| Security review | Verify password handling, input validation, access control, secrets, and transport settings | Security checklist and automated test output |
| Performance tests | Verify API response targets with the required concurrency and dataset | Repeatable load-test script, configuration, and report |
| Accessibility and UI review | Verify keyboard access, labels, focus, contrast, responsive layout, and feedback states | Automated scan plus manual checklists |
| Compatibility tests | Verify the main scenario in the required browser/version combinations | Compatibility matrix |
| Usability evaluation | Measure task completion, assistance, time, errors, comprehension, and participant feedback | Anonymised observation sheet and summary |

## 4. Environments and test data

### 4.1 Environments

| Environment | Use | Required configuration |
|---|---|---|
| Local automated test | Unit, integration, and contract tests | Isolated PostgreSQL test database; fixed clock where needed; test-only secrets |
| Staging | End-to-end, accessibility, responsive, compatibility, and usability tests | Production-like build over HTTPS; no production credentials or personal data |
| Load-test environment | Performance verification | Documented CPU, memory, database version, API version, and network location; no other workloads |

The exact versions of Node.js, PostgreSQL, browsers, test libraries, and operating systems shall be recorded when the tests are run.

### 4.2 Seeded data

The functional dataset shall include at least:

- six active student accounts and one unauthenticated visitor;
- one account with an incomplete skill profile;
- one completed profile with no reciprocal matches;
- one reciprocal pair with exactly one skill in each direction;
- one profile with multiple offered and wanted skills;
- skill categories and enough catalogue entries to test search filters;
- pending, accepted, declined, and cancelled requests;
- one accepted request with agreement details;
- attempted duplicate, self-directed, and unauthorized operations.

The load-test dataset shall contain at least 1,000 synthetic users and 10,000 active user-skill relationships. Synthetic accounts shall use non-routable addresses such as `example.test`; no real student records are required.

### 4.3 Data reset and repeatability

Automated suites shall create or restore a known database state before execution. Test cases must not depend on execution order unless the sequence is explicitly part of a state-transition test. Failed runs must retain enough logs to reproduce the failure without retaining passwords, session tokens, or private participant information.

## 5. Functional test catalogue

All cases in this section are planned.

| Test ID | Scenario and method | Expected result |
|---|---|---|
| **TC-AUTH-01** | Register with a unique email, valid password, and display name through the UI and API. | One account is created and the user is authenticated or directed to sign in. |
| **TC-AUTH-02** | Submit missing fields, malformed email, weak or invalid values, unexpected fields, and an already registered email. | Field-specific `4xx` errors are shown; no duplicate account is created. |
| **TC-AUTH-03** | Sign in with correct credentials, incorrect password, and an unknown email. | Correct credentials create a session; both invalid cases show the same non-disclosing error. |
| **TC-AUTH-04** | Sign out, then revisit a protected page and repeat a protected API request. | The session is invalidated and protected access requires authentication again. |
| **TC-PRO-01** | Edit the current user's profile with valid and invalid values, reopen it, then attempt to edit another profile through the API. | Valid values persist; invalid values are rejected; cross-user modification is denied. |
| **TC-PRO-02** | Open another student's profile and inspect the UI and API payload. | Only approved visible profile fields and current offered/wanted skills appear; private fields are absent. |
| **TC-SKL-01** | Add and remove an offered skill, attempt a duplicate, and inspect search/matching plus historical requests. | Active results change, duplicates are rejected, and historical records remain intact. |
| **TC-SKL-02** | Add and remove a wanted skill, attempt a duplicate, and inspect matching plus historical requests. | Active matches change, duplicates are rejected, and historical records remain intact. |
| **TC-SKL-03** | Select the same catalogue skill for two profiles and attempt to create an unsupported duplicate through the public API. | Both relationships use the same skill ID and catalogue duplication is denied. |
| **TC-SRCH-01** | Search by offered skill, apply a category filter, clear both, and inspect returned profile IDs. | Only eligible profiles appear, the current user is excluded, and clearing restores the documented default state. |
| **TC-SRCH-02** | Run a zero-result query and use the recovery action. | No profile cards appear; a clear empty state and an action to broaden the search are available. |
| **TC-MAT-01** | Seed reciprocal, one-directional, self, and unrelated profiles; request suggestions; remove one side of the only reciprocal pair and recalculate. | Only reciprocal users are suggested; self is excluded; removing either direction removes the suggestion. |
| **TC-MAT-02** | Inspect every returned suggestion and compare its explanation with active profile data. | At least one current skill in each direction explains every suggestion. |
| **TC-MAT-03** | Open matching with no offered skill, no wanted skill, and a complete profile with no reciprocal match. | Missing-profile guidance is distinct from the no-match state; manual search remains available. |
| **TC-REQ-01** | Send a valid request, then attempt a self-request, inactive skill pair, and duplicate pending request. | One valid `Pending` request and history entry are created; invalid requests are rejected without extra records. |
| **TC-REQ-02** | View incoming and outgoing lists as both participants and as an unrelated user. | Each list contains only the authenticated user's requests with correct participant, skills, status, and creation time. |
| **TC-REQ-03** | As recipient, accept one pending request and decline another; repeat each action and try as sender or unrelated user. | Only the recipient can make one valid transition; repeated and unauthorized changes are rejected. |
| **TC-REQ-04** | As sender, cancel a pending request; repeat cancellation and try to cancel accepted, declined, and another user's request. | Only the sender can cancel once from `Pending`; all forbidden transitions are rejected. |
| **TC-REQ-05** | Create and transition requests, then inspect history as both participants and an unrelated user; attempt history modification. | Every change has an immutable actor, status, and timestamp record visible only to participants. |
| **TC-AGR-01** | For an accepted request, record topic, future date/time, each format, and appropriate location/link; repeat for non-accepted and unrelated requests and invalid fields. | Valid details are visible to both participants; status, ownership, required-field, and format-specific rules are enforced. |
| **TC-AGR-02** | Update an agreement as each participant and as an unrelated user. | Participant changes persist for both users and update actor/time; unrelated access is denied. |
| **TC-AGR-03** | Inspect navigation, UI, and OpenAPI operations for chat/video; record an in-person location and external meeting information. | No built-in chat or video feature exists; supported external/in-person details can be recorded. |

## 6. Non-functional test catalogue

All cases in this section are planned.

| Test ID | Method and conditions | Target / expected result |
|---|---|---|
| **TC-SEC-01** | Register a known password, inspect stored credential data, and verify correct/incorrect passwords through automated tests. | No plaintext or reversible password is stored; an adaptive salted hash is used; only the correct password verifies. |
| **TC-SEC-02** | Build an endpoint authorization matrix covering anonymous, owner/participant, authenticated non-participant, and wrong-role access for every protected operation. | Anonymous access returns `401`; unauthorized object access returns `403` or non-disclosing `404`; permitted access succeeds. |
| **TC-SEC-03** | Submit invalid types, lengths, formats, extra fields, path/query values, and common SQL-injection strings to every write/search endpoint. | Requests receive safe `4xx` responses; injection strings are treated as data; database structure and unrelated rows do not change. |
| **TC-SEC-04** | Inspect staging HTTP/HTTPS behaviour, production cookie attributes, repository history, and secret-scanning output. | HTTP redirects or is unavailable; cookies use `Secure`, `HttpOnly`, and explicit `SameSite`; no active secret is committed. |
| **TC-SEC-05** | Make 10 failed logins and then an additional attempt for the same account or client; repeat after the 15-minute window. | Attempts above the configured threshold return `429`; access becomes available after the window expires. |
| **TC-SEC-06** | Compare profile/account API responses with approved schemas and inspect logs/errors for private fields. | Password hashes, sessions, secrets, internal configuration, and non-approved email data are absent. |
| **TC-USA-01** | Five representative students independently perform the full main scenario on staging using the protocol in Section 9. | At least 4 of 5 complete the scenario without moderator assistance. |
| **TC-USA-02** | Review registration, login, profile, search, matching, request, and agreement screens under normal, loading, success, validation, empty, and recoverable-error states. | Every applicable state provides visible and action-specific feedback; field errors identify the affected field. |
| **TC-USA-03** | Run automated WCAG checks on core screens; manually complete the main scenario by keyboard and inspect focus, labels, and contrast. | No critical automated violation; keyboard completion succeeds without a mouse; tested components meet WCAG 2.2 AA contrast. |
| **TC-PERF-01** | After warm-up, run three 10-minute tests with 20 concurrent simulated users against 1,000 users and 10,000 relationships; report the median run and every run. | In every run, p95 is at most 500 ms for profile/request operations and 1,000 ms for search/matching; API error rate is below 1%. |
| **TC-COM-01** | Execute the main scenario in the latest two stable major versions available at test time of Chrome, Firefox, Edge, and Safari; record exact versions. | Every browser/version combination passes or any blocking difference is fixed and retested before release. |
| **TC-COM-02** | Manually check all core screens at 360, 768, 1024, and 1440 px widths. | No unintended horizontal scrolling, clipped content, or hidden primary action. |
| **TC-REL-01** | Induce a failure between request-status update and history insertion in an integration test, then repeat without failure. | Failure rolls back both changes; success commits both atomically. |
| **TC-MNT-01** | Validate the versioned OpenAPI file and run contract tests for every main-scenario endpoint. | The document is valid and implemented schemas, authentication, responses, and error codes match it. |
| **TC-MNT-02** | Review the release traceability table and attached evidence. | Every Must requirement has at least one completed evidence record and no evidence field is empty. |

`NFR-PERF-02` is a **Should** requirement. If the staging UI is available, Lighthouse mobile tests will also measure Largest Contentful Paint on every core page, with a target of at most 2.5 seconds. This optional check does not replace `TC-PERF-01`.

## 7. Mandatory-requirement traceability

The following table covers every requirement marked **Must** in SSE-6. Evidence links are intentionally recorded as planned test IDs until execution; they shall be replaced or supplemented with report links at release review.

| Requirement | Planned verification evidence |
|---|---|
| FR-AUTH-01 | TC-AUTH-01, TC-AUTH-02 |
| FR-AUTH-02 | TC-AUTH-03 |
| FR-AUTH-03 | TC-AUTH-04 |
| FR-PRO-01 | TC-PRO-01, TC-SEC-02 |
| FR-PRO-02 | TC-PRO-02, TC-SEC-06 |
| FR-SKL-01 | TC-SKL-01 |
| FR-SKL-02 | TC-SKL-02 |
| FR-SKL-03 | TC-SKL-03 |
| FR-SRCH-01 | TC-SRCH-01 |
| FR-SRCH-02 | TC-SRCH-02, TC-USA-02 |
| FR-MAT-01 | TC-MAT-01 |
| FR-MAT-02 | TC-MAT-02 |
| FR-MAT-03 | TC-MAT-03, TC-USA-02 |
| FR-REQ-01 | TC-REQ-01 |
| FR-REQ-02 | TC-REQ-02, TC-SEC-02 |
| FR-REQ-03 | TC-REQ-03 |
| FR-REQ-04 | TC-REQ-04 |
| FR-REQ-05 | TC-REQ-05, TC-REL-01 |
| FR-AGR-01 | TC-AGR-01 |
| FR-AGR-02 | TC-AGR-02 |
| FR-AGR-03 | TC-AGR-03 |
| NFR-SEC-01 | TC-SEC-01 |
| NFR-SEC-02 | TC-SEC-02 |
| NFR-SEC-03 | TC-SEC-03 |
| NFR-SEC-04 | TC-SEC-04 |
| NFR-SEC-05 | TC-SEC-05 |
| NFR-SEC-06 | TC-SEC-06 |
| NFR-USA-01 | TC-USA-01 |
| NFR-USA-02 | TC-USA-02 |
| NFR-USA-03 | TC-USA-03 |
| NFR-PERF-01 | TC-PERF-01 |
| NFR-COM-01 | TC-COM-01 |
| NFR-COM-02 | TC-COM-02 |
| NFR-REL-01 | TC-REL-01 |
| NFR-MNT-01 | TC-MNT-01 |
| NFR-MNT-02 | TC-MNT-02 |

## 8. Request-state verification matrix

| Initial state | Actor and action | Expected state/result | Test case |
|---|---|---|---|
| No request | User sends a valid request to another user | `Pending`; initial history entry created | TC-REQ-01 |
| No request | User sends request to self or with invalid skill pair | Rejected; no request/history created | TC-REQ-01 |
| Pending | Recipient accepts | `Accepted`; one history entry created | TC-REQ-03, TC-REQ-05 |
| Pending | Recipient declines | `Declined`; one history entry created | TC-REQ-03, TC-REQ-05 |
| Pending | Sender cancels | `Cancelled`; one history entry created | TC-REQ-04, TC-REQ-05 |
| Pending | Wrong actor accepts, declines, or cancels | Rejected; no data change | TC-REQ-03, TC-REQ-04 |
| Accepted | Either participant records/updates agreement | Status remains `Accepted`; agreement is stored | TC-AGR-01, TC-AGR-02 |
| Accepted, Declined, or Cancelled | Actor attempts a terminal transition | Rejected; no data change | TC-REQ-03, TC-REQ-04 |

## 9. Evaluation of project aim

### 9.1 Evaluation questions

The evaluation will answer:

1. Can representative students complete the full journey without moderator assistance?
2. Does reciprocal matching help students identify a suitable partner more efficiently than basic desired-skill search?
3. Do students understand why a suggested partner matches them?
4. Do users consider the proposed request and agreement workflow clear enough to use?

### 9.2 Participants and ethics

Recruit five university students who were not involved in implementing the tested screens. Participation shall be voluntary. Before testing, explain the purpose, activities, duration, data recorded, withdrawal option, and anonymisation approach. Use participant codes `P01`–`P05`; do not collect passwords, private messages, or unnecessary identifying data in repository evidence.

### 9.3 Main-scenario usability test

Each participant will use a fresh test account and receive a short goal without step-by-step interface instructions:

> Create an account, add the skills you can offer and want to learn, find a suitable partner, send an exchange request, respond as the second participant, and record the agreed topic, time, and format.

The moderator may clarify the task goal but shall not identify controls or give navigation instructions. Assistance requested or provided is recorded. A scenario counts as successful only when all required records are stored correctly and the participant completes it without moderator assistance.

### 9.4 Matching-versus-baseline comparison

The baseline is **manual search by desired skill without reciprocal-match suggestions**. The comparison condition uses reciprocal suggestions with an explanation of the skill match.

Each participant completes two equivalent partner-finding tasks on the same staging build and equally sized synthetic datasets:

- **Baseline condition:** search for profiles offering the desired skill, inspect profiles, and select a partner manually.
- **Matching condition:** inspect reciprocal suggestions and select a partner using the displayed match explanation.

Task order is counterbalanced: three participants start with the baseline and two start with matching. The datasets use different names but equivalent numbers of profiles, relevant offers, distractors, and one clearly suitable reciprocal partner. No participant sees the same dataset twice.

### 9.5 Metrics and targets

| Metric | Measurement | Target |
|---|---|---|
| Full-scenario completion | Participants completing all main-scenario steps without moderator assistance | At least 4 of 5 (80%) |
| Partner-selection success | Participant selects the profile satisfying both directions of the assigned skill need | At least 4 of 5 in the matching condition |
| Matching explanation comprehension | Participant correctly states what each person can teach the other after selection | At least 4 of 5 |
| Discovery time | Time from presentation of the partner-finding task to selection | Matching-condition median no longer than baseline median; a 20% reduction is the desired improvement |
| Discovery effort | Number of result/profile views before selection | Matching-condition median no higher than baseline median |
| Critical errors | Actions that prevent completion or create an invalid request/agreement | Zero unresolved critical errors at release |
| Task ease | One 1–7 rating after each major task, where 7 is very easy | Median at least 5 for the main scenario |
| Overall usefulness | 1–5 agreement with “This platform would help me arrange a skill exchange” | Median at least 4 |
| Matching usefulness | 1–5 agreement with “The suggestions helped me find a suitable partner” | Median at least 4 |

The 20% discovery-time reduction is a desired result, not a release gate. With five participants, results will be reported descriptively using counts, medians, ranges, and anonymised observations; no population-wide statistical claim will be made.

### 9.6 Feedback collection

The moderator records task completion, time, assistance, errors, route taken, and short think-aloud observations. After each major task, the participant gives the 1–7 ease rating. After both discovery conditions and the complete scenario, ask:

- What made it easy or difficult to find a partner?
- Did the match explanation make sense? What was unclear?
- Which profile or search information was missing?
- Was sending and responding to the request clear?
- Were the agreed topic, time, and format fields sufficient?
- What would prevent you from using this platform?

Closed ratings and open comments shall be reported separately. Negative and contradictory feedback must be retained in the summary rather than removed as outliers.

## 10. Entry, suspension, and exit criteria

### 10.1 Entry criteria

- SSE-6 requirements and SSE-7 architecture are merged into `main`.
- The tested feature has acceptance criteria implemented and code-reviewed.
- Automated unit/integration checks for the feature pass.
- Staging is reachable over HTTPS and uses the documented test dataset.
- OpenAPI reflects the tested endpoints.
- Usability participants have received the consent information and test accounts.

### 10.2 Suspension criteria

Testing pauses when the environment loses data integrity, the build cannot complete the main scenario, a security issue could expose participant data, or a blocking defect makes subsequent results invalid. The reason and affected cases shall be recorded before rescheduling.

### 10.3 Release exit criteria

- every Must requirement has completed evidence in the traceability table;
- no unresolved critical or high-severity defect blocks the main scenario, authorization, privacy, or data consistency;
- security, performance, compatibility, responsive, accessibility, and OpenAPI checks meet their mandatory targets or have an explicitly approved corrective plan;
- at least 4 of 5 participants complete the full scenario without assistance;
- failed cases are fixed and retested, or formally recorded as accepted limitations by both team members and the supervisor;
- the final evaluation report separates measured results from interpretation.

## 11. Responsibilities and planned outputs

| Activity | Responsible | Reviewer / participant | Output |
|---|---|---|---|
| Maintain requirement traceability and API/security tests | Nursultan Makhmutov | Tamir Burlibaev | Automated reports and traceability updates |
| Maintain UI, accessibility, responsive, and browser checks | Tamir Burlibaev | Nursultan Makhmutov | UI checklists and compatibility matrix |
| Prepare staging data and load-test dataset | Nursultan Makhmutov | Tamir Burlibaev | Seed version and environment record |
| Moderate usability sessions | One team member | Other team member observes and records | Anonymised observation sheets |
| Analyse results and agree corrective actions | Both team members | Supervisor where needed | Evaluation summary and issue links |

## 12. Review and delivery checklist

- [x] Every Must requirement is linked to at least one planned test or review.
- [x] Successful flows, invalid input, access permissions, and request status changes are covered.
- [x] Metrics, targets, measurement conditions, and required data are defined.
- [x] A manual-search baseline is defined for comparison with reciprocal matching.
- [x] User feedback and task completion assessment are defined.
- [x] Planned tests are distinguished from completed tests.
- [ ] Tamir has reviewed this plan through a pull request.
- [ ] Review comments have been resolved and the changes merged into `main`.
- [ ] The pull request is linked to [SSE-9](https://student-skill-exchange.youtrack.cloud/issue/SSE-9).

Suggested branch: `SSE-9-verification-evaluation-plan`.
