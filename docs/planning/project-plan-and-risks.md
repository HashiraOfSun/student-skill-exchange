Project Plan and Risk Register
Project: Development of a Peer-to-Peer Skill Exchange Platform for University Students  
Team: Nursultan Makhmutov and Tamir Burlibaev, SE-2413, Astana IT University  
Supervisor: Konstantin Latuta  
Document owner / SSE-10 assignee: Tamir Burlibaev  
Required reviewer: Nursultan Makhmutov  
Updated: 23 October 2026  
Status: Ready for pull-request review; review and merge evidence remain to be recorded.  
Time zone: Astana, UTC+5, for all deadlines and targets.
1. Purpose, scope, and project links
This plan assigns responsibilities, sequences the work, defines milestone exits, and records risks and controls. It covers both the first assessment checkpoint and subsequent application development.
Resource	Link or repository path
GitHub repository	HashiraOfSun/student-skill-exchange
YouTrack board	Student Skill Exchange Kanban
Planning task	SSE-10 — Document project milestones, responsibilities, and risks
This deliverable	`docs/planning/project-plan-and-risks.md`
Scope	Project proposal
Requirements	Initial Platform Requirements supplied for SSE-6
User evidence	Survey report, SSE-2
Existing systems	Comparison, SSE-4
Interface	Prototype walkthrough, SSE-8
The first version includes accounts, editable profiles, offered and wanted skills from a shared catalogue, skill/category search, explained reciprocal recommendations, exchange requests and status history, and recording a shared topic, future time, and meeting format. Sessions take place in person or through an external service.
Request states are Pending, Accepted, Declined, and Cancelled. A pending request can be accepted or declined by its recipient or cancelled by its sender. Participants can edit an accepted exchange's shared plan without changing that status. The UI, API, persistence, and tests must implement the same rules.
Payments, built-in chat/video, native mobile applications, machine-learning recommendations, certificates, formal skill assessment, and group classes are outside this version.
2. Responsibilities and actual task allocation
Team responsibilities
Area	Responsible member	Required contribution and handoff
Backend and data	Nursultan Makhmutov	Architecture, schema/migrations, REST API, authentication, authorization, validation, matching, request processing/history, agreement storage, and backend documentation
Frontend and UI/UX	Tamir Burlibaev	User flows, prototype, responsive screens, forms, search/match explanations, request and agreement interfaces, loading/empty/error states, accessibility, and API integration
Research and requirements	Both, according to the task register	Nursultan leads literature, technical choices, and requirements; Tamir leads student research and system comparison; each reviews the other's conclusions
Integration and verification	Nursultan: API/security/data; Tamir: client/usability	Agree the contract, integrate increments, test core and negative scenarios, and link results to requirement IDs
Planning and reporting	Tamir coordinates planning and user documentation; Nursultan coordinates technical evidence and assessment assembly	Maintain risks, contribution evidence, setup/API/database documentation, report, and demonstration materials
Each work item has one assignee and the other member as peer reviewer. Supervisor feedback is recorded separately from peer approval.
Task register — supplied YouTrack snapshot, 23 October 2026
The displayed assignees and priorities below are transcribed from the supplied task list. Normal corresponds to “Обычная”; Major corresponds to “Серьезная”. For the technical workstream, this plan assigns person-level delivery responsibility to Nursultan while preserving the displayed account label `admin`. The screenshot does not establish that account's personal identity; record its owner in the contributor information before attributing contributions to an individual.
Task	Title	Displayed assignee	Priority	Delivery responsibility under this plan
SSE-1	Prepare the project proposal and define its scope	`admin`	Normal	Nursultan
SSE-2	Interview students about skill exchange	Tamir Burlibaev	Normal	Tamir
SSE-3	Review literature on peer learning and skill matching	`admin`	Normal	Nursultan
SSE-4	Compare existing skill exchange and peer learning platforms	Tamir Burlibaev	Normal	Tamir
SSE-5	Compare technology options and justify the selected stack	`admin`	Normal	Nursultan
SSE-6	Define functional and non-functional requirements	`admin`	Major	Nursultan
SSE-7	Design the system architecture and create diagrams	`admin`	Normal	Nursultan
SSE-8	Create a UI prototype for the main user scenarios	Tamir Burlibaev	Normal	Tamir
SSE-9	Prepare the verification and evaluation plan	`admin`	Normal	Nursultan
SSE-10	Document project milestones, responsibilities, and risks	Tamir Burlibaev	Normal	Tamir
SSE-11	Obtain supervisor feedback and document revisions	`admin`	Major	Nursultan; Tamir addresses comments in his areas
SSE-12	Prepare and submit the assessment materials	`admin`	Major	Nursultan coordinates; both verify their deliverables
Priority does not replace dependency order or a confirmed deadline. SSE-6, SSE-11, and SSE-12 need particular attention because they connect the evidence, decisions, and submission package. Task completion must be verified through deliverables and PRs; the screenshot alone is not review or merge evidence.
3. Current baseline and confirmed deadlines
The proposal and detailed initial requirements have been supplied. A six-response survey report, existing-system comparison, and standalone clickable prototype with a walkthrough are prepared for review. Architecture, technology, verification, supervision, and submission evidence must be checked in their respective tickets before the assessment package is declared complete.
The prototype demonstrates local interactions with sample data. Backend, database, integration, security, and multi-user readiness require separate implementation evidence.
Item	Confirmed deadline	Source / qualification
SSE-2	23 October 2026, 16:00	Supplied research task description
SSE-4	23 October 2026, 20:00	Supplied comparison task description
SSE-10	23 October 2026, 21:00	Current planning task description
SSE-8	24 October 2026, 10:00	Supplied prototype task description
First assessment checkpoint	24 October 2026; exact submission hour not established	Supplied assessment instructions; confirm the cutoff through the assessment channel
Other tasks and later academic submissions/defence	Not established by the supplied evidence	Preserve any deadlines already recorded in live tickets; add missing dates with their source
A prepared file is not evidence that its task met its deadline. Use actual acceptance, review, merge, and submission timestamps. If a deadline passes with work outstanding, record the remaining work and revised decision while retaining the original date.
First-checkpoint exit gate
The checkpoint requires analysis, initial design, planning, supervision, and traceable contributions; a complete application is not required. SSE-12 can proceed when the following are checked:
Proposal, scope, project README, links, roles, and access for the team, supervisor, and committee.
Actual relevance evidence, with findings separated from assumptions. Record acceptance of the six-response questionnaire alternative to SSE-2's original 3–5-discussion brief.
Literature review with at least 12 meaningfully used sources, including eight scientific publications; comparison of 3–5 systems using 6–10 consistent criteria; at least three technology decisions with 2–3 alternatives each.
Prioritized requirements and verifiable criteria; consistent context, use-case, and draft component diagrams with editable sources.
Accessible prototype and walkthrough; verification/evaluation plan with metrics, conditions, and a baseline; this plan and risk register.
Substantive supervisor feedback, revision decisions, reviewed changes, and individual task/commit/PR evidence.
4. Proposed development milestones
The table is a proposed sequence after the first checkpoint, not an official calendar. Week 1 means the first agreed development week after the checkpoint; subsequent weeks are relative to that start. Calendar dates and available hours must be agreed once later academic deadlines are known. No weekly-hour commitment or December submission date is assumed.
M1–M7 are milestone identifiers, not YouTrack task IDs. Create real implementation tickets with owners, estimates, and reviewed targets before starting their work.
Milestone	Proposed window	Lead	Prerequisites	Exit criteria
M1 — Research and requirements refinement	Week 1	Tamir: evidence; Nursultan: requirements	Checkpoint materials and feedback; SSE-2/3/4/6	Method decision and limitations recorded; findings reflected in priorities; remaining assumptions have owners and validation actions
M2 — Design and API agreement	Week 2	Nursultan: architecture/API; Tamir: UI	M1; SSE-5/7/8/9	Data model, diagrams, user flow, request rules, versioned OpenAPI contract, examples, errors, and timezone handling reviewed together
M3 — First connected implementation	Week 3	Both, by component	M2 contract and setup	Registration/sign-in and profile editing work through the actual frontend, API, and database; persisted changes survive reload; basic ownership/error paths checked
M4 — Core feature implementation	Weeks 4–5	Both, by component	M3 and feature acceptance criteria	Skills, search, explained reciprocal matching, requests/history, and accepted-plan recording delivered in reviewed increments with negative-case checks
M5 — Full integration candidate	Week 6	Nursultan coordinates; Tamir integrates client	Reviewed M4 increments, migrations, configuration	Complete main journey works for two users; persistence and contract checks pass; setup and candidate version are reproducible
M6 — Testing and evaluation	Week 7	Nursultan: API/security/matching; Tamir: UI/usability	M5 and reviewed SSE-9 protocol	Every Must requirement has evidence; permission/state/transaction checks pass; responsive/browser checks, user results, matching-baseline comparison, and limitations recorded
M7 — Final documentation and demonstration	Week 8	Tamir coordinates; Nursultan supplies technical sections	M6 results and reviewed corrections	Report, diagrams, API/database/setup/test/user guides, contribution evidence, and demo script match the selected version
Contingency	Proposed reserve after M7, sized during scheduling	Both	Outstanding defects or evaluation gaps	Resolve blockers and repeat affected checks; prepare a new reviewed candidate where needed
Tests, integration, and documentation accompany each increment. M5–M7 consolidate evidence. Review capacity weekly, keep one primary active task per member, reserve time for review and corrections, and reduce optional scope before compromising mandatory checks.
Immediate checkpoint sequence
Tamir opens the SSE-10 PR; Nursultan reviews; Tamir addresses comments, obtains approval, merges, and links the PR to SSE-10. Keep the 21:00 deadline visible. In parallel, verify remaining checkpoint evidence, resolve SSE-11 feedback, and assemble SSE-12. If a required review or deliverable remains unavailable, record the blocker and actual readiness rather than treating the plan as completion of that work.
5. Dependencies and handoffs
Dependency	Required handoff / reason
SSE-1 → SSE-2/3/4/5	Scope, target users, exclusions, and investigation questions guide research and alternatives
SSE-2/3/4 + SSE-5 → SSE-6 refinement	Evidence, limitations, and technical decisions inform requirements; unresolved assumptions remain labelled
SSE-6 → SSE-7/8/9	Architecture, UI, and verification use the same requirement IDs, scenarios, states, and acceptance criteria; these tasks may run in parallel
Data model + API contract → parallel frontend/backend work	Agree skill IDs, schemas, permissions, errors, statuses, and timestamps before dependent integration
Authentication/profiles → skills and exchange ownership	Requests require real identities, persisted profiles, and server-side access rules
Offered/wanted skills → search → reciprocal matching	Discovery uses canonical active skills; recommendations require both overlap directions and self exclusion
Identity + skills + state rules → requests/history	Validate participants, skill pair, duplicates, and atomic state/history updates
Accepted request → shared plan	Only accepted participants can record/edit a topic, future time, and format
Reviewed increments → M5 → M6 → M7	Evaluation requires a connected, reproducible candidate; final claims require measured results and recorded limitations
Initial deliverables + SSE-10 + SSE-11 revisions → SSE-12	Submission needs reviewed materials, feedback decisions, access, contribution links, and the exact version
Supervisor feedback can start on ready materials. Frontend fixtures can support parallel work, but mock-only functionality does not close integration tasks. Record blockers in YouTrack with the prerequisite issue, missing handoff, owner, and next action.
The checkpoint readiness path is requirements consistency, architecture/prototype/verification evidence, feedback and revisions, reviewed package, and tagged submission. Planning runs alongside research and design rather than blocking their start.
6. YouTrack, branches, review, and completion
Task and board rules
Every task records its actual YouTrack ID, one assignee, reviewer, output, acceptance criteria, priority, dependencies, and a confirmed deadline or proposed target. Milestone/risk labels in this document do not substitute for issue IDs.
Use the project's board stages as applicable:
Stage	Meaning
Очередь — Queue	Scoped and assigned, awaiting work
Разработка — Development	Active research, documentation, design, or implementation
Ревью — Review	PR opened, author checks recorded, peer review requested
Тест — Test	Applicable verification and acceptance checks being completed
На тестовом окружении — Test environment	Applicable runnable changes checked in the integration/staging environment
Готово — Done	Acceptance, required review, checks, merge, and task links complete
Documentation-only tasks require content and consistency checks; they do not require application deployment. Record the applicable verification in the PR. A blocked task names the dependency and next action and stays visibly incomplete.
Required development workflow
Start from the reviewed `main` baseline. Use a task branch, for example `SSE-10-project-plan-and-risks`.
Make coherent commits using an identifiable contributor account. For this change use `SSE-10: document milestones, responsibilities, and risks`. Record research/design/documentation progressively as well as code.
Open a PR into `main`, for example `SSE-10: add project plan and risk register`. Link SSE-10, summarize the change, explain verification, and disclose gaps. Add the PR link to the task.
Nursultan reviews this document's allocation, timing, dependencies, risks, and completion rules. Tamir reviews Nursultan-authored changes. Resolve substantive comments in the branch and request re-review after material revisions.
Obtain approval of the final content, pass applicable repository checks, and merge using the configured method. Preserve the relationship between the PR and resulting commit.
Add the merge commit or permanent merged-file link and verification summary to YouTrack. Check any automatic integration before relying on it to close the issue.
Definition of done: the required deliverable exists at the correct path; acceptance criteria have evidence; the required peer review covers the final changes; applicable checks pass; changes are merged into `main`; and the PR/commit evidence is linked to the task. Mandatory defects remain blockers. Code additionally requires relevant component, contract, integration, and negative-case checks plus updated setup/documentation. Research documents require source, date, consistency, and evidence/assumption checks.
Submission version and access
The supplied first-submission form requires `prob-period-1`. Tag the exact reviewed commit and provide its direct GitHub tag link. The general instructions also list pre-defence tags; follow each submission's specific naming requirement. If two names are required for the same package, point both to the same commit and record the relationship.
Check that attachments and prototype materials match that version and that the team, supervisor, and committee can access them. Keep submitted tags fixed; record later corrections through the required procedure and a new reviewed version. The standalone prototype remains usable offline after download.
7. Risk register
Likelihood and impact are qualitative planning judgments. Low likelihood: possible without a specific warning; Medium: plausible and requiring monitoring; High: current conditions make disruption especially likely. Low impact: local correction; Medium: rework within a milestone; High: a confirmed deadline, mandatory outcome, data protection, or core flow is threatened.
Each risk has one accountable owner. R01–R15 are local risk IDs; controls are planned until their execution is evidenced in the relevant task.
ID	Risk and trigger	Likelihood	Impact	Mitigation and response	Responsible person
R01	Checkpoint work or review misses a confirmed deadline; required evidence remains missing at the final check	High	High	Inventory evidence, finish focused PRs, and prioritize review/corrections. Record outstanding work and a revised decision without replacing the original deadline	Tamir Burlibaev
R02	Unknown official dates conflict with the proposed sequence; an announced cutoff precedes planned readiness	Medium	High	Confirm the assessment hour and later dates; anchor milestone dates to available capacity and official cutoffs; record impacts and re-plan	Tamir Burlibaev
R03	The survey alternative is not accepted or findings are overstated; six questionnaire records differ from the discussion brief	Medium	High	Record the method/sample decision, preserve all six responses and limitations, and arrange permitted follow-up evidence if required; retain the distinction from interviews	Tamir Burlibaev
R04	Reciprocal matching yields too few partners despite complete profiles	Medium	High	Measure coverage on a defined dataset; retain manual search and clear no-match guidance; report sparse-match cases and review any proposed model change	Tamir Burlibaev
R05	Optional requests displace mandatory functionality	Medium	High	Maintain explicit exclusions and priorities; estimate changes and dependencies; defer optional scope or obtain a reviewed scope/date decision	Tamir Burlibaev
R06	API/client drift produces incompatible fields, skill IDs, errors, or request states	Medium	High	Review the versioned contract and fixtures together; integrate at M3 and after increments; update both components and affected checks before incompatible changes merge	Nursultan Makhmutov
R07	A user accesses or changes another user's protected record	Medium	High	Enforce backend object permissions, credential protection, and input validation; test unauthenticated/cross-user access; block release on exposure or unauthorized writes	Nursultan Makhmutov
R08	Repeated/concurrent actions create conflicting outcomes or separate status and history updates	Medium	High	Guard transitions and use atomic writes; test duplicates, simultaneous actions, and induced failures; correct inconsistencies and retest before release	Nursultan Makhmutov
R09	Mobile, keyboard, or error handling prevents completion	Medium	High	Check 360/768/1024/1440 px, focus/labels/keyboard use, state handling, and the agreed browser matrix; fix main-flow blockers and repeat affected checks	Tamir Burlibaev
R10	Participants see different meeting instants or can save past/ambiguous times	Medium	High	Agree UTC storage and explicit display timezone; validate future times consistently; test different browser timezones and date boundaries	Tamir Burlibaev
R11	Absence, coursework, or an unfamiliar tool causes repeated estimate overruns	Medium	High	Review capacity weekly, keep tasks small, time-box investigation, document handoffs, and reserve review/fix time; reassign feasible work and defer optional scope	Tamir Burlibaev
R12	Hosting, migration, configuration, or data loss prevents reproducible execution	Low	High	Maintain a local run path, example configuration, reviewed migrations, and a checked backup/restore procedure; verify both environments and retain a local demo fallback	Nursultan Makhmutov
R13	Evaluation lacks participants, comparable baseline conditions, or a recorded tested version	Medium	High	Agree SSE-9's protocol early, arrange participants, freeze version/data, and record failures and conditions; report evidence gaps and seek a revised evaluation decision	Tamir Burlibaev
R14	Sources or comparison claims do not support requirements or conclusions	Medium	Medium	Verify original/official sources and access dates, mark unverified features Unknown, and separate interpretation; revise unsupported claims before reuse	Nursultan Makhmutov
R15	Account identity, missing review links, access, or mixed/tagged versions prevent contribution and submission traceability	Medium	High	Identify contributor accounts, retain task/PR/revision evidence, check access and package consistency, and keep submitted tags fixed	Nursultan Makhmutov
Review R01–R03 and R15 during each remaining checkpoint work session; review all risks weekly and at milestone exits. When a trigger occurs, create or update the actual YouTrack issue with the risk ID, owner, impact, next action, and response target. Escalate threats to a deadline, data protection, or core flow to the other member the same day; involve the supervisor for academic scope/date/evidence decisions.
8. Progress, evaluation, and change control
At an agreed weekly review, confirm capacity, inspect completed evidence and blockers, update risks, and select the next small tasks. Track accepted outputs, Must requirements with evidence, unresolved core-flow defects, and dependency/risk actions. Commit count alone is not a progress measure.
Changes to scope, the API, estimates, or proposed dates record their reason, affected requirement/task IDs, dependency impact, owner, reviewer, and decision. Only official instructions or an authorized recorded decision change an academic deadline.
SSE-9 defines environment, data, metrics, and baseline before evaluation. The initial SSE-6 usability target is four unaided successful completions among five representative students; it remains a target requiring review, not a result. A proposed matching baseline is one-direction skill search with the same users/catalogue; confirm it in SSE-9 and record reciprocal validity, coverage, and applicable discovery measures. Do not infer learning improvement from partner discovery alone.
Maintain requirements, diagrams, API documentation, and checks during development. Link every Must requirement to test/review evidence at release review. Prototype checks do not establish backend security, performance, transactions, or multi-browser implementation readiness.
9. SSE-10 acceptance and review record
The content covers assigned responsibilities, all required milestone stages, confirmed/proposed timing, dependencies, risk likelihood/impact/mitigation/ownership, project links, and the development workflow.
Remaining acceptance step	Required evidence
Nursultan reviews the document	Actual PR review, resolved comments, revision commits, and approval of the final content
Changes are merged into `main`	Actual merge commit and permanent merged-file link
PR is linked to SSE-10	Actual PR URL and verification summary in the task before Done
These external steps are not yet recorded in this document. The planning PR and SSE-10 retain the authoritative completion evidence.
