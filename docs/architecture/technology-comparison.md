# Technology Comparison and Selected Stack

**Project:** Development of a Peer-to-Peer Skill Exchange Platform for University Students  
**Task:** SSE-5  
**Status:** Ready for team review

## 1. Decision context

The first version is a web application for two-sided skill exchange. It must support accounts, profiles, offered and wanted skills, search, reciprocal partner suggestions, exchange requests, and agreed exchange details. The project proposal excludes built-in chat, video calls, payments, native mobile applications, and machine-learning recommendations from the MVP.

The system will be developed by two students: one is responsible mainly for the backend and database, and the other for the frontend and API integration. The repository does not yet provide evidence that either team member has production experience with a specific framework. This comparison therefore does not claim undocumented expertise. Before implementation begins, both developers should complete a small setup exercise with the selected stack; if that reveals a serious skill gap, the decision should be reviewed.

The options are assessed against the same project needs:

- **Functional fit:** suitability for accounts, related skill data, search, matching, and request-state rules.
- **Maintainability:** clear structure, type safety, testability, documentation, and manageable dependencies.
- **Security:** support for authentication, authorization, validation, secure transport, and safe defaults.
- **Deployment:** ability to run locally and on common managed or container-based hosting.
- **Team fit:** learning burden, division between frontend and backend, and ease of collaboration.
- **MVP effort:** the amount of framework and infrastructure work required before product features can be implemented.

## 2. Frontend application

### Alternatives

| Option | Functional fit and maintainability | Security and deployment | Team fit and MVP effort | Main trade-off |
|---|---|---|---|---|
| **React + TypeScript + Vite** | React builds interfaces from reusable components. TypeScript can detect many type errors before execution. Vite provides a development server and produces static production assets. This is a direct fit for the planned profile, search, recommendation, and request screens. | The production output can be served as static files. Client-side code still requires safe token handling, output encoding, dependency updates, and server-side authorization; React alone is not a security boundary. | One frontend codebase and one language shared with the selected backend reduce context switching. The team still needs to learn routing, forms, API state, and testing. | The team must select and maintain supporting libraries because React is a UI library rather than a complete application framework. |
| **Next.js + TypeScript** | Next.js adds routing, server rendering, server components, and other full-stack features to React. It is useful when server rendering or a combined full-stack application is required. | It can run as a Node.js server, a container, or a static export, although static export has limited feature support. The larger execution model creates more deployment and security surface than this MVP needs. | Familiar React concepts can transfer, but the team must also understand server/client boundaries, caching, and framework conventions. | Its full-stack and rendering features overlap with the separately owned Express backend and add complexity without a current requirement for server-side rendering. |
| **Vue + TypeScript + Vite** | Vue is an approachable, component-based framework with an incrementally adoptable ecosystem. It can implement all planned MVP screens and can use the same Vite deployment model. | Like a React single-page application, it can be deployed as static assets and depends on backend authorization for protected operations. | Its template syntax may be approachable, but choosing it would create a separate learning path if the team is already using React-oriented materials or prototypes. No such experience is documented yet. | Technically suitable, but it offers no project-specific advantage strong enough to replace the selected React path. |

### Decision

Select **React with TypeScript and Vite**.

This option provides the component model needed for the planned interface while keeping deployment independent from the backend. TypeScript is selected for static checking at the frontend/backend contract boundary. Vite is selected because it provides a focused development server and a static production build without adding server-rendering features that the MVP does not require.

The trade-off is that routing, form validation, API-state handling, and testing are not supplied as one integrated framework. These libraries should be selected only when the relevant implementation task begins, rather than added speculatively.

Official documentation: [React: Describing the UI](https://react.dev/learn/describing-the-ui), [TypeScript: A Static Type Checker](https://www.typescriptlang.org/docs/handbook/typescript-from-scratch), [Vite: Getting Started](https://vite.dev/guide/), and [Vite: Building for Production](https://vite.dev/guide/build).

## 3. Backend platform

### Alternatives

| Option | Functional fit and maintainability | Security and deployment | Team fit and MVP effort | Main trade-off |
|---|---|---|---|---|
| **Node.js + Express + TypeScript** | Express supplies HTTP routing and middleware with a small core. TypeScript supports shared request and response types and catches many mistakes before execution. The modular approach fits a small REST API with explicit service and data-access layers. | Express documents production practices such as TLS, input validation, secure headers, dependency maintenance, and brute-force protection. These controls must be configured by the team. A Node process is straightforward to run locally or package in a container. | Sharing TypeScript with the frontend simplifies collaboration and API type definitions. Express has a small initial surface, but the team must establish its own project structure and choose validation, authentication, and database libraries. | Minimalism gives control but fewer secure defaults; inconsistent middleware or architecture is a risk unless conventions and tests are enforced. |
| **Django** | Django includes an ORM, authentication, forms, and administration features. Its integrated conventions can speed up data-oriented applications and reduce dependency selection. | Django documents built-in protection against several common web risks, including SQL injection, cross-site scripting, cross-site request forgery, and clickjacking when used correctly. It runs as a Python web application and typically needs an additional REST API layer. | It is productive when the backend developer already knows Python and Django, but that experience is not recorded. It would also introduce Python alongside the TypeScript frontend. | Strong built-in features, but some are unnecessary for a separate JSON API and the two-language stack adds context switching. |
| **Java + Spring Boot** | Spring Boot provides a structured ecosystem, dependency injection, validation, security integration, testing, and production features. It is well suited to large, long-lived services. | Official documentation covers executable applications, container images, external configuration, monitoring, and production deployment. Security is powerful but requires correct Spring Security configuration. | It is a strong option if the backend developer already has substantial Java/Spring experience. Without that evidence, configuration and framework concepts create the largest learning cost of the three options. | More structure and production facilities than the diploma MVP currently needs, with higher setup and learning overhead. |

### Decision

Select **Node.js with Express and TypeScript**.

The MVP is primarily an I/O-oriented HTTP service rather than a CPU-intensive system. Node.js uses an event loop to support non-blocking I/O, while Express supplies a small routing and middleware layer. Using TypeScript on both sides of the API reduces language switching and makes it possible to share or generate interface types.

This decision does not assume that Express is secure automatically. The backend must use supported releases, TLS in deployment, schema-based input validation, centralized error handling, secure response headers, rate limiting on authentication endpoints, password hashing, and authorization checks in the service layer. Protected operations must never rely on frontend checks.

The trade-off is that the team must define and enforce structure. The backend should therefore be organised into route, validation, controller, service, repository, and domain modules, with automated tests for authorization and request-state transitions.

Official documentation: [Node.js event loop](https://nodejs.org/en/learn/asynchronous-work/event-loop-timers-and-nexttick), [Express overview](https://expressjs.com/), [Express middleware](https://expressjs.com/en/guide/using-middleware.html), [Express security practices](https://expressjs.com/en/advanced/best-practice-security.html), and [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html).

## 4. Data storage

The core model contains strongly related records: users, skills, offered skills, wanted skills, reciprocal matches, exchange requests, status history, and agreed exchange details. Uniqueness, foreign-key relationships, and valid request-state changes matter more than flexible document shapes.

### Alternatives

| Option | Functional fit and maintainability | Security and deployment | Team fit and MVP effort | Main trade-off |
|---|---|---|---|---|
| **PostgreSQL** | Relational tables, primary keys, foreign keys, unique constraints, check constraints, transactions, and indexes match the connected domain model. Database constraints can protect invariants even when application code contains a defect. | A separate database server requires credentials, restricted network access, backups, and migrations. Managed PostgreSQL and containers are widely available deployment models. Application queries must still be parameterised and database roles must use least privilege. | SQL and explicit relations make the data model visible to both developers and suitable for architecture diagrams. Initial setup is greater than SQLite but appropriate for a multi-user web application. | Requires operating a database service and maintaining migrations. Schema changes are more deliberate than in a flexible document database. |
| **MongoDB** | Its flexible document model is useful when records vary significantly and data accessed together can be embedded. This project, however, has many cross-record relationships and lifecycle rules. MongoDB supports multi-document transactions, but its documentation notes additional cost and recommends effective schema design rather than using transactions as a substitute. | Managed and container deployment are available. Correct authorization, network restriction, indexes, validation, and backup configuration remain necessary. | JavaScript/TypeScript tooling is convenient, but the team would need to choose carefully between embedding and referencing for skills, requests, and users. | Flexibility can reduce early migration work, but denormalisation and cross-document consistency add avoidable design complexity for this relational domain. |
| **SQLite** | SQLite is a self-contained, serverless, transactional SQL database and is excellent for local prototypes and tests. It supports the necessary relational concepts. | Deployment is simple because data is stored in one local file. The official guidance notes that SQLite allows one writer at a time and recommends a client/server database when many concurrent writers or multiple application servers are required. | It has the lowest setup cost and is useful for isolated tests, but moving from a local file to production PostgreSQL creates environment differences. | Simple for a prototype, but less suitable as the main database for a deployed multi-user service and future horizontal scaling. |

### Decision

Select **PostgreSQL** as the application database.

The decisive factor is data integrity. A user can offer and request many skills, and an exchange request links two participants and moves through controlled statuses. PostgreSQL foreign keys, unique constraints, check constraints, and transactions support these rules directly. It also provides conventional indexes for search fields and relationship queries.

The trade-off is operational work: the team must manage migrations, environment-specific connection settings, backups for a deployed instance, and least-privilege credentials. SQLite may still be used for small isolated experiments only if the selected data-access library produces equivalent behaviour; integration tests should run against PostgreSQL to avoid database-specific surprises.

Official documentation: [PostgreSQL overview](https://www.postgresql.org/about/), [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html), [MongoDB data modelling](https://www.mongodb.com/docs/manual/data-modeling/), [MongoDB transactions](https://www.mongodb.com/docs/manual/core/transactions/), [About SQLite](https://www.sqlite.org/about.html), and [Appropriate Uses for SQLite](https://www.sqlite.org/whentouse.html).

## 5. Frontend–backend communication

### Alternatives

| Option | Functional fit and maintainability | Security and deployment | Team fit and MVP effort | Main trade-off |
|---|---|---|---|---|
| **REST-style HTTP API with JSON and OpenAPI** | Resource-oriented endpoints map clearly to profiles, skills, recommendations, and exchange requests. Standard HTTP methods and status codes provide familiar semantics. An OpenAPI document can serve as the shared contract and support generated documentation or clients. | HTTPS protects data in transit. The API still requires authentication, object-level authorization, validation, CORS restrictions, response-size limits, and safe error messages. It uses ordinary HTTP infrastructure and is easy to deploy and inspect. | Clear endpoint ownership supports parallel frontend/backend work. Mock responses and an OpenAPI contract can be prepared before implementation. | Some screens may require several requests, and careless endpoint design can return too much or too little data. Contract changes must be managed explicitly. |
| **GraphQL over HTTP** | Clients request selected fields through a typed schema, which can reduce over-fetching and combine nested data access. A single graph can be useful for multiple diverse clients. | A single endpoint does not remove authorization needs. Field-level access, query depth or cost, introspection policy, and error handling add security and operational work. | Both developers must learn schema, resolver, client-cache, and query conventions. The MVP has one web client and a small, predictable data model, so the flexibility has limited current value. | Powerful query flexibility, but more implementation and security complexity than the MVP needs. |
| **WebSocket connection** | WebSockets provide two-way interactive browser–server communication without polling and suit chat or live presence. The project proposal explicitly excludes real-time chat, and the planned request workflow does not require a continuously open connection. | Persistent connections require connection authentication, origin checks, reconnect logic, resource limits, and compatible proxy configuration. Deployment and testing are more involved than ordinary request-response HTTP. | Adds a second communication model for a feature outside the MVP. | Best for real-time events, but unsuitable as the primary CRUD interface and unjustified for the present scope. |

### Decision

Select a **REST-style HTTP API using JSON over HTTPS**, documented with **OpenAPI**.

The MVP operations map naturally to resources and state-changing commands. Standard HTTP semantics are sufficient, the interface can be tested independently, and an OpenAPI contract gives both team members a reviewable integration boundary. API endpoints should be versioned under `/api/v1` to make the initial contract explicit.

The trade-off is that the team must design task-oriented endpoints carefully, especially for reciprocal recommendations and request-state transitions. The API should not expose database tables directly. GraphQL can be reconsidered only if later clients need substantially different data shapes. WebSockets can be reconsidered only if validated requirements add real-time chat or notifications.

Official documentation and standards: [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html), [OpenAPI Specification](https://spec.openapis.org/oas/latest.html), [GraphQL queries](https://graphql.org/learn/queries/), [GraphQL over HTTP](https://graphql.org/learn/serving-over-http/), and [MDN WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API).

## 6. Selected stack

| Layer | Selected technology | Reason for selection |
|---|---|---|
| Frontend | React + TypeScript + Vite | Component-based UI, static deployment, type checking, and no unnecessary server-rendering layer |
| Backend | Node.js + Express + TypeScript | Small HTTP API surface, shared language with frontend, and explicit modular architecture |
| Database | PostgreSQL | Relational integrity, constraints, transactions, and indexes for strongly connected domain data |
| Communication | REST-style JSON API over HTTPS | Simple request-response model for the MVP and broad tooling support |
| API contract | OpenAPI | Reviewable interface for parallel frontend/backend work and generated documentation |

The initial deployment should consist of three independently configurable parts: static frontend assets, one backend service, and one PostgreSQL database. Local development may use containers or locally installed services, but secrets and database files must not be committed. Specific hosting providers are intentionally not selected here because cost, university requirements, and account availability still need confirmation.

## 7. Security and maintenance baseline

The technology choice does not by itself make the application secure. The implementation must include:

- supported dependency versions and automated dependency checks;
- HTTPS outside local development;
- password hashing with a maintained password-hashing library;
- server-side request validation and centralized error handling;
- authentication plus object-level authorization on every protected operation;
- parameterised database access and least-privilege database credentials;
- explicit CORS configuration for the deployed frontend origin;
- secure token or session handling agreed during the authentication design task;
- rate limiting for login and other abuse-sensitive endpoints;
- database migrations, backups for deployed data, and tested restore instructions;
- automated tests for access restrictions and exchange-request state transitions;
- an OpenAPI document kept consistent with the implemented API.

## 8. Consequences and review triggers

The selection favours a small, understandable architecture over framework breadth. It accepts additional responsibility for Express middleware, project structure, and security configuration in exchange for one language across the web stack and a clear separation of frontend and backend.

Review this decision if any of the following occurs:

- the team setup exercise shows a substantially stronger shared capability in Django or Spring Boot;
- university or supervisor requirements mandate another platform or deployment environment;
- validated requirements introduce real-time chat, multiple client applications, or complex live collaboration;
- the data model becomes predominantly unstructured rather than relational;
- deployment constraints make a separately hosted frontend, backend, and database impractical.

Otherwise, implementation and architecture tasks should use this document as the baseline.
