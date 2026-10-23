# Student Skill Exchange

A diploma project at Astana IT University.

We are building a web platform where university students can learn from each other by exchanging skills. For example, someone who knows Python and wants to practise English could find a student who offers English practice and wants help with Python.

**Diploma topic:** Development of a Peer-to-Peer Skill Exchange Platform for University Students.

## Why we are building this

We want to explore whether students can find learning partners more easily when they can see what others know and what they want to learn.

Our starting assumption is that finding a suitable person through student chats can take time, especially when both people want something in return. We still need to check this through conversations with students before treating it as an established problem.

## Who it is for

University students who want to share what they know and learn something new from their peers.

## What we plan to build

The first version will let students:

- Create an account and fill out a profile.
- List skills they can teach and skills they want to learn.
- Search for other students by skill.
- See suggested partners with matching learning interests.
- Send and respond to exchange requests.
- Agree on the topic, time, and format of an exchange.

We will keep the first version focused on finding a partner and arranging an exchange. Built-in video calls, payments, a mobile app, and machine learning are outside its scope.

## Our goal

By the end of the project, we aim to have a working web application that supports the full journey from registration to an agreed exchange.

We will test the main user flows and evaluate how well the matching approach helps students find suitable partners. The project will also include API documentation and instructions for using the platform.

## Team

We are two Software Engineering students from group SE-2413:

- **Makhmutov Nursultan** — Backend, database, API, authentication, and partner matching.
- **Burlibaev Tamir** — User flows, interface design, frontend, and API integration.

We will work together on research, requirements, testing, and the final report. Tasks and repository history will show each person's contribution.

**Supervisor:** Latuta Konstantin

## Where we are now

We are at the beginning of the project. We have outlined the idea and our responsibilities; development has not started yet.

Our next steps are to talk to potential users, review relevant research and existing platforms, define the requirements, and prepare the architecture and interface prototype.

## Technology stack

The first version will use:

- **Frontend:** React with TypeScript and Vite.
- **Backend:** Node.js with Express and TypeScript.
- **Database:** PostgreSQL.
- **Frontend–backend communication:** a REST-style JSON API over HTTPS.
- **API contract and documentation:** OpenAPI.

This stack keeps the frontend and backend independently deployable, uses one language across the application, and provides relational constraints and transactions for users, skills, and exchange requests. Real-time communication is not included because chat is outside the first-version scope.

The alternatives, trade-offs, security responsibilities, and decision triggers are documented in the [technology comparison](docs/architecture/technology-comparison.md).

## Documentation and tasks

We will add research, requirements, diagrams, and prototype materials to this repository as they are prepared.

- [YouTrack task board](https://student-skill-exchange.youtrack.cloud/agiles/204-1/current)

## Running the project

There is no runnable application yet. Setup and testing instructions will be added when the first implementation is ready.
