# Student Skill Exchange

A diploma project at Astana IT University.

Student Skill Exchange is a web platform where university students can teach skills they know and find peers who can teach skills they want to learn. The MVP focuses on profiles, offered and desired skills, partner discovery, reciprocal matching, and exchange requests.

**Diploma topic:** Development of a Peer-to-Peer Skill Exchange Platform for University Students.

## Project scope

The MVP is designed to let students:

- create an account and maintain a profile;
- list skills they can teach and skills they want to learn;
- search for students by skill;
- receive reciprocal partner suggestions;
- send, accept, decline, cancel, and complete exchange requests;
- agree on the topic, time, and format of an exchange.

Built-in video calls, payments, a mobile application, and machine-learning recommendations are outside the MVP scope.

## Team

The team consists of two Software Engineering students from group SE-2413:

- **Makhmutov Nursultan** — backend, database, API, authentication, and partner matching;
- **Burlibaev Tamir** — user flows, interface design, frontend, and API integration.

Research, requirements, testing, project planning, and the final report are shared responsibilities.

**Supervisor:** Latuta Konstantin

## Technology stack

- **Frontend:** React, TypeScript, and Vite
- **Backend:** Node.js, Express, and TypeScript
- **Database:** PostgreSQL
- **Interface:** REST-style JSON API over HTTPS
- **API contract:** OpenAPI

The rationale, alternatives, trade-offs, and decision triggers are documented in the [technology comparison](docs/architecture/technology-comparison.md).

## Project documentation

### Proposal and research

- [Project proposal](docs/project-proposal.md)
- [Student interviews and survey findings](docs/research/user-interviews.md)
- [Literature review](docs/research/literature-review.md)
- [Existing systems comparison](docs/research/existing-systems-comparison.md)

### Requirements, architecture, and prototype

- [Functional and non-functional requirements](docs/requirements.md)
- [Technology comparison](docs/architecture/technology-comparison.md)
- [System architecture](docs/architecture/system-architecture.md)
- [System context diagram](docs/diagrams/system-context.png)
- [Use-case diagram](docs/diagrams/use-case.png)
- [Component diagram](docs/diagrams/component-diagram.png)
- [UI prototype package](SSE-8_UI_Prototype.zip)

Editable Draw.io sources are stored in [`docs/diagrams`](docs/diagrams/).

### Verification, planning, and supervision

- [Verification and evaluation plan](docs/testing/verification-and-evaluation-plan.md)
- [Project plan, responsibilities, and risks](docs/planning/project-plan-and-risks.md)
- [Supervisor feedback and revisions](docs/supervision/supervisor-feedback.md)

### Pre-defense materials

- [Pre-defense report](docs/submission/student-skill-exchange-pre-defense-report.pdf)
- [YouTrack board and task screenshots](docs/submission/youtrack-board-and-tasks.pdf)
- [Submission checklist and form data](docs/submission/submission-checklist.md)

## Project tracking

- [YouTrack task board](https://student-skill-exchange.youtrack.cloud/agiles/204-1/current)
- [GitHub repository](https://github.com/HashiraOfSun/student-skill-exchange)

## Current status and limitations

The proposal, research, requirements, architecture, UI prototype, verification plan, project plan, risk register, and supervisor feedback record are complete. The current repository contains documentation and prototype materials.

A runnable web application has not been implemented yet. The tests in the verification plan are planned tests, and no implementation test results are claimed. Submission of the university form, storage of its confirmation, and creation of the `pre-defense-1` repository tag must be completed as final administrative steps.
