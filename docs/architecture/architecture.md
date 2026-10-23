# System Architecture and Diagrams

**Project:** Development of a Peer-to-Peer Skill Exchange Platform for University Students  
**Task:** SSE-7  
**Status:** Draft for team review  
**Owner:** Nursultan Makhmutov  
**Required reviewer:** Tamir Burlibaev

## 1. Purpose and scope

This document describes the initial architecture of the Student Skill Exchange MVP. It aligns the selected technology stack with the functional and non-functional requirements for accounts, profiles, skills, search, reciprocal matching, exchange requests, and agreed exchange details.

The architecture deliberately excludes built-in chat, video calls, payments, native mobile applications, and machine-learning recommendations. Students conduct an agreed exchange in person or through an external service.

## 2. Architecture drivers

The design is guided by the following requirements:

- keep the frontend and backend independently deployable;
- provide a clear REST-style JSON API documented with OpenAPI;
- enforce authentication, object-level authorization, validation, and safe error handling on the backend;
- preserve relational integrity and request-state history with PostgreSQL constraints and transactions;
- support transparent reciprocal matching based on offered and wanted skills;
- keep request and agreement workflows consistent for both participants;
- remain small enough for a two-student team to implement and test.

## 3. System context

![System context diagram](diagrams/system-context.svg)

Editable source: [`system-context.drawio`](system-context.drawio) and [`system-context.mmd`](diagrams/system-context.mmd).

University students use the platform in two complementary roles: seeking help and offering help. A user can hold both roles at the same time. The platform supports finding a partner and agreeing on an exchange. The learning session itself takes place outside the platform, either in person or through an external service selected by the participants.

## 4. Use cases

![Use case diagram](diagrams/use-case.svg)

Editable source: [`use-case.drawio`](use-case.drawio) and [`use-case.mmd`](diagrams/use-case.mmd).

The main end-to-end scenario is:

1. A visitor registers and logs in.
2. The student completes a profile and records offered and wanted skills.
3. The student searches manually or reviews reciprocal partner suggestions.
4. The student opens a partner profile and sees why the pair matches.
5. The student sends an exchange request.
6. The recipient accepts or declines the request.
7. After acceptance, either participant records the agreed topic, date, time, and format.

The sender can cancel a request only while it is pending. Built-in messaging and video sessions are outside the MVP.

## 5. Component architecture

![Component diagram](diagrams/component-diagram.svg)

Editable source: [`component-diagram.drawio`](component-diagram.drawio) and [`component-diagram.mmd`](diagrams/component-diagram.mmd).

### 5.1 Frontend

The React application is responsible for pages, forms, routing, client-side feedback, and calling the backend API. Client-side checks improve usability but do not replace backend authorization or validation.

### 5.2 Backend

The Express application exposes the REST API and separates transport logic from domain behaviour:

- **Routes and controllers** translate HTTP requests and responses.
- **Security middleware** authenticates requests, checks authorization, validates input, and rate-limits authentication attempts.
- **Authentication service** manages registration, login, logout, and password verification.
- **Profile and skill service** manages profile fields and offered/wanted skills.
- **Search and matching service** performs catalogue search and reciprocal matching.
- **Exchange request service** enforces request ownership and allowed status transitions.
- **Agreement service** manages the topic, time, format, and optional meeting information for accepted requests.
- **Repository layer** owns database access and transaction boundaries.

### 5.3 Database

PostgreSQL stores users, profiles, the skill catalogue, offered and wanted skills, exchange requests, immutable status-history records, and agreements. Foreign keys, unique constraints, check constraints, and transactions protect the principal invariants.

### 5.4 API contract

OpenAPI is the shared contract between the frontend and backend. It documents request and response schemas, authentication, validation errors, and status codes. The implemented API and the contract must be checked together.

## 6. Principal data relationships

- One user has one profile.
- A user can offer many skills and want many skills.
- Catalogue skills are reused across profiles rather than stored as free-text duplicates.
- An exchange request connects one sender, one recipient, one offered skill, and one wanted skill.
- A request has one current status and many immutable status-history records.
- An accepted request may have one agreement visible to both participants.

A detailed entity-relationship diagram can be added when the database-schema task begins. It is not required to replace the three architectural diagrams in this task.

## 7. Key runtime flows

### 7.1 Reciprocal matching

1. The frontend requests partner suggestions for the authenticated user.
2. The backend verifies the session and loads active offered and wanted skills.
3. The matching service selects users for whom both directions of the skill relationship exist.
4. The response includes the skills that explain each suggestion.

### 7.2 Exchange request

1. The sender selects the offered and wanted skills and submits a request.
2. The backend validates both skills against current profile data and rejects self-requests or duplicate pending requests.
3. The request and its initial history entry are committed in one database transaction.
4. Only the recipient can accept or decline; only the sender can cancel while the request is pending.

### 7.3 Agreement

1. Either participant opens an accepted request.
2. The backend verifies participation and accepted status.
3. The participant records or updates the topic, future date and time, format, and optional location or external link.
4. Both participants receive the same stored agreement details.

## 8. Security and privacy responsibilities

- Passwords are hashed on the backend with a maintained adaptive algorithm and unique salts.
- Every protected operation verifies authentication and permission for the specific resource.
- Request bodies and parameters are schema-validated before domain processing.
- Database operations use parameterised queries.
- Authentication endpoints are rate-limited.
- Secrets are provided through protected environment configuration and are not committed.
- Non-local traffic uses HTTPS.
- API responses expose only fields required for finding and arranging an exchange.
- The platform does not publish private contact information by default.

## 9. Deployment view

The initial deployment consists of three independently configurable parts:

1. static React production assets served through an HTTPS-capable web host;
2. a Node.js/Express API service configured through environment variables;
3. a PostgreSQL database accessible only to the API service.

The frontend receives only the public API base URL. Database credentials and authentication secrets remain on the backend. A reverse proxy or managed host terminates HTTPS and forwards API traffic to Express.

## 10. Requirement-to-component traceability

| Requirement area | Primary components |
|---|---|
| Registration and authentication | Frontend forms, security middleware, authentication service, user repository |
| Profiles and skills | Profile UI, profile and skill service, profile/skill repositories |
| Search | Search UI, search service, indexed skill relationships |
| Reciprocal matching | Match suggestions UI, matching service, user-skill relationships |
| Exchange requests | Request UI, request service, request and history repositories |
| Agreed exchange details | Agreement UI, agreement service, agreement repository |
| Security and privacy | Security middleware, all domain services, environment configuration |
| API documentation | OpenAPI contract and contract checks |

## 11. Assumptions and planned refinement

The component diagram is intentionally a draft. Service boundaries may be combined in code if the implementation remains clear and testable. Exact deployment providers, authentication-session mechanism, database-access library, and supporting frontend libraries will be selected during implementation tasks.

User-research findings must be used to review assumptions about profile fields, search filters, matching value, agreement fields, privacy, and meeting format. Changes must update the requirements, diagrams, and OpenAPI contract together.

## 12. Review and delivery checklist

- [x] System context diagram is included.
- [x] Use case diagram is included.
- [x] Draft component diagram is included.
- [x] Editable sources and readable SVG exports are included.
- [x] Diagram elements align with the selected stack and current MVP scope.
- [x] Requirements, components, data, and main scenarios are traceable.
- [ ] Tamir has reviewed the document through a pull request.
- [ ] Review comments have been resolved and the changes merged into `main`.
- [ ] The pull request is linked to SSE-7.

Suggested branch: `SSE-7-system-architecture`.
