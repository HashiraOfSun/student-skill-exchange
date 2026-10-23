# Project Proposal

## Project title

Development of a Peer-to-Peer Skill Exchange Platform for University Students.

## Team and supervisor

- **Nursultan Makhmutov**, SE-2413 — backend development.
- **Tamir Burlibaev**, SE-2413 — frontend development.
- **Supervisor:** Konstantin Latuta.
- **University:** Astana IT University.

## Problem statement

Students have different practical skills and learning interests.
A student who can help with programming may need help practising
English, while another student may have the opposite strengths.

Our starting assumption is that finding a suitable exchange partner
through general student chats can take time. Information about what
people can teach and what they want to learn may be scattered across
messages, making reciprocal matches difficult to identify.

We will investigate this assumption through discussions with 3–5
potential users. At this stage, we have not yet established how
common this problem is or whether students would regularly use
a dedicated platform.

## Target users

The initial target users are university students who want to share
their knowledge and learn practical skills from other students.

We will initially focus our user research on students at Astana IT
University. The first version will support individual exchanges
between two participants.

## Project aim

To develop and evaluate a web platform that helps university students
find partners with complementary skills and arrange peer-to-peer
learning exchanges.

## Objectives

1. Investigate students' current learning support practices,
   difficulties, and expectations.
2. Review relevant research and compare existing platforms.
3. Define functional and non-functional requirements with
   verifiable acceptance criteria.
4. Compare technology options and design the system architecture.
5. Develop user accounts, profiles, and skill management.
6. Implement search and reciprocal partner matching.
7. Implement exchange requests and agreement on exchange details.
8. Integrate the frontend and backend.
9. Test the main scenarios and evaluate the matching approach
   against a defined baseline.
10. Prepare technical documentation and user instructions.

## Proposed solution

The platform will allow each student to list skills they can offer
and skills they want to learn. Students will be able to search for
participants and view suggested exchange partners.

The initial matching approach will look for reciprocal matches:
student A offers a skill wanted by student B, and student B offers
a skill wanted by student A. Recommendations will show the skills
that produced the match.

A student can send an exchange request to another participant.
The recipient can accept or decline it, and requests can be
cancelled according to rules defined in the requirements.

Participants will be able to record the agreed topic, time,
and format of the exchange. The learning session itself will
take place outside the platform, either in person or through
an external communication service.

## Main user scenario

1. A student creates an account and signs in.
2. The student adds offered and desired skills to their profile.
3. The student searches for a partner or views recommendations.
4. The student opens a profile and sends an exchange request.
5. The recipient reviews and accepts or declines the request.
6. If accepted, the participants agree on the topic, time,
   and format of the exchange.
7. Both participants can view the recorded exchange details.

## Scope of the first version

The first version will include:

- Registration, login, and access control.
- User profiles and profile editing.
- Offered and desired skills.
- Search and filtering by skills and categories.
- Partner recommendations based on reciprocal skill matches.
- An explanation of matching skills.
- Incoming and outgoing exchange requests.
- Request statuses and status history.
- Recording agreed exchange details.
- A web interface adapted for desktop and mobile screens.

The first version will not include:

- Payments or paid tutoring.
- Built-in video calls.
- A real-time chat system.
- Native mobile applications.
- Machine-learning-based recommendations.
- Certificates or formal assessment of users' skills.
- Group classes or a course marketplace.

## Engineering challenges

The project requires consistent interaction between user profiles,
skill data, partner matching, and exchange requests.

The backend must prevent unauthorized changes to other users'
profiles and requests. Request status transitions must follow
defined rules, and both participants must see consistent information.

The matching logic must handle incomplete profiles, repeated skills,
and cases where no reciprocal partner is available. The frontend
must communicate these situations clearly.

## Responsibilities

### Nursultan Makhmutov

- Design the backend architecture and database.
- Develop the REST API.
- Implement authentication, validation, and access control.
- Implement profiles, skills, search, and partner matching.
- Implement exchange request processing and data storage.
- Test backend functionality and document the API.

### Tamir Burlibaev

- Design user flows, page structure, and interface mockups.
- Develop registration, login, and profile interfaces.
- Build search and recommendation screens.
- Develop exchange request and agreement interfaces.
- Integrate the frontend with the API.
- Handle validation messages, loading states, and errors.
- Check responsive layouts and navigation.

### Shared responsibilities

Both team members will contribute to research, requirements,
technology decisions, integration, testing, and reporting.
Individual tasks and contributions will be recorded in YouTrack
and GitHub. Changes will be reviewed by the other team member
before merging.

## Expected outcomes

By the end of the diploma project, we expect to deliver:

- A working web application demonstrating the main exchange scenario.
- A documented API and database structure.
- Test results for core functions and access restrictions.
- An evaluation of partner matching against a baseline approach.
- Technical documentation and user instructions.

The evaluation will examine whether the platform helps users find
suitable partners. We do not assume in advance that it will improve
learning outcomes or that reciprocal matches will always be available.

## Current stage

The project is in the analysis and planning stage. An initial README,
a GitHub repository, and a YouTrack board have been created.

User interviews, the literature review, comparisons, detailed
requirements, architectural diagrams, and the interface prototype
are planned work. Application development has not started.

## Project links

- [GitHub repository](https://github.com/HashiraOfSun/student-skill-exchange)
- [YouTrack board](https://student-skill-exchange.youtrack.cloud/agiles/204-1/current)
- [Proposal task SSE-1](https://student-skill-exchange.youtrack.cloud/issue/SSE-1)
