# Comparison of Existing Skill Exchange and Peer Learning Platforms

**Project:** Development of a Peer-to-Peer Skill Exchange Platform for University Students  
**YouTrack task:** [SSE-4](https://student-skill-exchange.youtrack.cloud/issue/SSE-4/Compare-existing-skill-exchange-and-peer-learning-platforms)  
**Project board:** [Student Skill Exchange Kanban](https://student-skill-exchange.youtrack.cloud/projects/SSE/agiles/204-1/current)  
**Required repository path:** `docs/research/existing-systems-comparison.md`  
**Document owner / task assignee:** Tamir Burlibaev  
**Required peer reviewer:** Nursultan Makhmutov  
**Research and access date:** 23 October 2026  
**Confirmed task deadline:** 23 October 2026, 20:00, Astana time (UTC+5)  
**Repository:** [HashiraOfSun/student-skill-exchange](https://github.com/HashiraOfSun/student-skill-exchange)  
**Status:** Research document prepared; peer review, merge into `main`, and linking the PR to YouTrack remain pending.

## 1. Purpose and method

This comparison examines four existing platforms using the same ten criteria. It supports decisions about profiles, finding a learning partner, arranging an exchange, and the scope of our first version.

The evidence comes from official product pages, help articles, and public service listings retrieved on 23 October 2026. It is a review of documented capabilities. No accounts were created, sessions booked, payments made, or authenticated workflows tested. Provider statements establish what a platform describes, rather than the quality or reliability of its operation.

The following labels apply throughout the comparison:

- **Documented:** the cited material explicitly describes or displays the capability.
- **Unknown:** the reviewed material does not establish the capability or its details. This does not mean the feature is absent.
- **Team interpretation / proposal:** our reasoning or a candidate design decision, kept separate from product facts.

Sources are linked through the IDs in each table cell. Section 7 records a URL and access date for every source. Several Simbi pages were inconsistently retrievable; the relevant source notes explain the evidence available. No numerical ranking is assigned because the platforms serve different purposes and were not tested under comparable conditions.

## 2. Why these four systems were selected

| Platform | Documented focus | Reason for selection |
| --- | --- | --- |
| **Simbi** | A general network for exchanging services, with direct exchanges and internal credits. [S1], [S2] | The closest example of a broad exchange model. It helps us consider what happens when two people do not need each other's services at the same time. |
| **Tandem** | Reciprocal language practice through conversations with other learners and speakers. [T1] | A focused example of expressing what someone can offer and wants to learn, then finding a compatible partner. |
| **Knack** | University-based, course-specific peer tutoring, supported through institutional programs. [K1] | Directly relevant to student communities and to arranging academic help around university courses. |
| **ADPList** | Sessions with experienced mentors in areas including design, engineering, product, and career development. [A1], [A2] | Relevant to students seeking practical feedback. It provides a useful comparison between reciprocal peer exchange and learning from an experienced mentor. |

Together, these systems cover broad service exchange, language exchange, campus tutoring, and professional mentorship. This is a purposive sample, rather than an exhaustive survey of the market.

## 3. Consistent comparison criteria

| ID | Criterion | Question used for every platform |
| --- | --- | --- |
| C1 | User profiles | What information helps a learner understand the person offering help? |
| C2 | Offered and desired skills | How are what a person can teach and what they want to learn represented? |
| C3 | Search and discovery | How can a user find relevant people, offers, or requests? |
| C4 | Partner matching | What connects learning needs with someone able to help? |
| C5 | Request and agreement workflow | How is a proposed interaction initiated and agreed? |
| C6 | Scheduling | How are availability, time, duration, and meeting format arranged? |
| C7 | Communication and learning format | How can participants communicate or conduct a session? |
| C8 | Pricing and exchange model | Who pays, or what is exchanged? |
| C9 | Trust and safety | What documented information or controls support an informed and safer choice? |
| C10 | University community support | Is there documented support for students or institutions, and what remains unverified? |

## 4. Comparison matrix

The matrix is divided into two tables for readability. Both use the same four platforms and the criteria defined above.

### 4.1 Profiles, discovery, and agreement

| Criterion | Simbi | Tandem | Knack | ADPList |
| --- | --- | --- | --- | --- |
| **C1. User profiles** | **Documented:** public provider identity, qualifications, availability notes, and reviews appear on a sampled service page. [S3] | **Documented:** photos, languages spoken and being learned, interests, and learning preferences. [T2] | **Documented:** tutor photo, biography, background, relevant experience, and availability. [K2] | **Documented:** mentor profiles show professional roles, expertise, and reviews; mentors can add a biography. [A1], [A3] |
| **C2. Offered and desired skills** | **Documented:** service offers and separate requests. A paired, structured teach/learn profile is **Unknown**. [S2], [S4] | **Documented:** spoken and target languages represent the two sides of an exchange. General subject-to-subject exchange is **Unknown**. [T1], [T2] | **Documented:** active tutoring courses and course-help requests. Reciprocal skill-pair declarations are **Unknown**. [K3] | **Documented:** mentors specify topics they can help with; mentors may also book learning sessions. Paired reciprocal skill fields are **Unknown**. [A3] |
| **C3. Search and discovery** | **Documented:** categories and public service listings. Specific text-search and filter controls are **Unknown** from the retrieved pages. [S2] | **Documented:** discovery by language, location, and interests; some advanced discovery options belong to Pro. [T1], [T2] | **Documented:** tutors see requests relevant to their active courses. [K3] | **Documented:** browse by expertise, inspect profiles and reviews, and use search filters. [A2] |
| **C4. Partner matching** | **Documented:** members can browse and propose exchanges; credits enable indirect exchange. Automated reciprocal ranking is **Unknown**. [S1], [S2] | **Documented:** the community feed considers language combinations. The exact ranking method is **Unknown**. [T2] | **Documented:** learners request course help and interested tutors respond. This is course-based connection, with no reciprocal skill algorithm confirmed. [K1], [K3] | **Documented:** goal-aligned mentor suggestions and user choice. The ranking method and reciprocal skill matching are **Unknown**. [A1] |
| **C5. Request and agreement workflow** | **Documented:** conversations and exchange proposals. Detailed acceptance, cancellation, and completion states are **Unknown**. [S1] | **Documented:** users initiate conversations. A separate structured exchange-request lifecycle is **Unknown**. [T2] | **Documented:** session requests can be accepted or changed; eligible requests may use Instant Booking. [K4] | **Documented:** choose a mentor and book a time slot. Approval and cancellation rules for every session type are **Unknown**. [A2] |

### 4.2 Arranging a session, cost, trust, and campus context

| Criterion | Simbi | Tandem | Knack | ADPList |
| --- | --- | --- | --- | --- |
| **C6. Scheduling** | **Documented:** a sampled listing includes availability notes and asks users to arrange timing in advance. Built-in calendar booking is **Unknown**. [S3] | **Unknown:** a dedicated availability calendar or booking workflow was not established by the reviewed feature pages. [T1], [T2] | **Documented:** date, time, expected duration, location, availability, and once/weekly scheduling are part of session requests. [K4] | **Documented:** mentors publish availability and session length; learners select an available calendar slot. [A2], [A3] |
| **C7. Communication and learning format** | **Documented:** the sampled listing mentions communication on Simbi and optional external channels. Built-in video is **Unknown**. [S3] | **Documented:** text, voice notes, audio/video calls, corrections, and translation tools. [T1] | **Documented:** messaging, in-person sessions, and a built-in Online Classroom; group sessions are also described. [K1], [K4] | **Documented:** live one-to-one video sessions and post-session notes. [A1], [A3] |
| **C8. Pricing and exchange model** | **Documented:** free joining and cashless exchanges; direct trades or internal credits, which have no dollar value. [S1], [S2], [S4] | **Documented:** a free version and a paid monthly/yearly Pro subscription. Exact regional and university-partnership prices are **Unknown**. [T2], [T4] | **Documented:** institutions fund tutoring for eligible learners. Coverage can be limited to certain students or courses. Institutional fees are **Unknown**. [K1] | **Documented:** free sessions are available and some mentors offer paid sessions. Exact booking fees are **Unknown**; official pages contain inconsistent free-booking wording. [A3], [A4] |
| **C9. Trust and safety** | **Documented:** public reviews and self-described qualifications. Credential verification, reporting, and moderation controls are **Unknown** in the inspected pages. [S3], [S4] | **Documented:** application review, authentic-profile rules, reporting, moderation, and an appeals process. Their effectiveness was not tested. [T1], [T3] | **Documented:** course approval and possible training requirements govern tutor activation. Additional identity and moderation controls are **Unknown** here. [K3] | **Documented:** mentor applications are manually reviewed and previous mentees can leave reviews. Detailed identity-check methods are **Unknown**. [A2], [A3] |
| **C10. University community support** | **Documented:** a general community network. University verification, campus-only membership, and institutional administration are **Unknown**. [S2], [S4] | **Documented:** university partnerships, campus rollouts, onboarding support, and optional usage reporting. Campus-only membership and university sign-in are **Unknown**. [T4] | **Documented:** school-specific courses and peer tutors, with institutional eligibility rules. Availability at Astana IT University is **Unknown**. [K1], [K4] | **Documented:** students are included among the intended mentees. Current university-only networks and institutional sign-in are **Unknown** from these sources. [A2] |

### 4.3 Important qualifications

**ADPList pricing:** the mentor recruitment page contains a general statement that booking a mentor is free. Its comparison guide, updated on 15 October 2026, explicitly describes both free and paid sessions. We retain that distinction and leave exact charges unverified; the price and terms of a particular booking need to be checked before use. [A3], [A4]

**Knack access and booking:** free access depends on institutional coverage, rather than being guaranteed to every university student. Its documentation also distinguishes course-help requests from scheduling a particular session. Instant Booking describes confirmation of eligible session requests; it should not be read as a guarantee of immediate tutoring. [K1], [K3], [K4]

**University support:** Tandem explicitly advertises an institutional offering, so it would be inaccurate to describe all non-tutoring platforms as lacking university support. Campus-only access or identity verification requires separate evidence. [T4]

**Simbi retrieval:** the service catalog, organizational profile, and a sampled service page supplied usable public evidence. The How It Works description was available as an official indexed extract, while direct retrieval was unsuccessful. Some other Simbi requests also returned access errors. These observations limit verification; they do not establish missing features or a platform-wide outage. [S1], [S2], [S3], [S4]

## 5. What existing systems address

The observations below are product facts followed by our interpretation of their relevance.

- **Exchanging help without an immediate reciprocal match:** Simbi documents internal credits as well as direct exchange. **Team interpretation:** an exchange design needs an explicit policy for cases where one person's offer does not interest the other. Credits are one possible approach, with additional accounting and dispute-handling decisions. [S1], [S2]
- **Finding someone with complementary knowledge:** Tandem makes spoken and target languages visible and uses language combinations in discovery. **Team interpretation:** showing both sides of a learning relationship can guide our profile and matching design. Whether the same approach works across unrelated subjects needs testing. [T1], [T2]
- **Organising academic support inside a university:** Knack connects university courses, peer tutors, and session arrangements. **Team interpretation:** campus context and concrete session details deserve separate attention; the institutional funding model is a different commitment from a student-run prototype. [K1], [K4]
- **Getting feedback from a more experienced person:** ADPList supports choosing a professional mentor and booking a session. **Team interpretation:** mentor-led help is a relevant alternative when a student wants feedback rather than a reciprocal exchange. Our service must offer a useful reason to choose peer exchange in that situation. [A1], [A2]

The comparison documents several workable approaches. It does not establish how frequently our intended users face a problem, how satisfied they are with existing options, or whether they will adopt another platform. Those questions belong in real student interviews and prototype evaluation.

## 6. Proposed contribution and requirement implications

Our repository describes a first version with student profiles, offered and desired skills, skill search, suggested partners, exchange requests, and agreement on a topic, time, and format. Built-in video, payments, a native mobile app, and machine learning are outside that stated scope. The README was observed at the repository state associated with commit `6234b14e69aa693151e0fe9e61dcbb54e2bdd77e`. [P1]

The team's SSE-3 literature review supports a small first version with transparent reciprocal matching and voluntary exchanges. The decisions below connect that direction with the product comparison. They are **team proposals**, to reconcile with SSE-6 requirements and evidence from SSE-2 student research. The value of the proposed combination remains a hypothesis to evaluate, rather than a claim of market-wide novelty.

### 6.1 Profiles and reciprocal discovery in the MVP

Keep offered and wanted skills separate. Provide skill search and simple rules that check both directions: Student A offers what Student B wants, and Student B offers what Student A wants. Show a short explanation, such as a Python-for-English exchange, and let students choose. Tandem's two language roles provide a useful product reference. [T2]

### 6.2 Exchange requests in the MVP

Support a request with the proposed help in both directions, followed by acceptance or rejection. Record the agreed topic, time, and format. Knack's concrete session requests are a useful reference. Check cancellation, completion, and rescheduling rules against SSE-6 before implementation. [K4]

### 6.3 Filters that need student validation

Knack and ADPList show availability and session details, but that does not establish which discovery filters our students need. Validate availability, language, proficiency, and session-format filters through SSE-2. Recording an agreed time and format does not require an availability calendar or calendar integration. [K4], [A3]

### 6.4 Trust measures and future ratings

Profiles, reviews, and approval rules provide different kinds of information about a partner. For the pilot, propose clear experience descriptions, deliberate contact sharing, and a basic reporting procedure with an assigned owner. Treat self-reported ability separately from verified credentials. Public ratings remain a future candidate; their value and moderation costs need user and supervisor review. [S3], [T3], [K3], [A3]

### 6.5 A manageable exchange model

Keep payments and credit balances outside the first version. Simbi's credits address exchanges without an immediate reciprocal match, but introduce additional accounting rules. Test how often direct matches are possible and define what students can do when no suitable reciprocal partner is available. Confirm pilot eligibility separately. [S1], [S2], [K1], [T4]

Machine-learning and graph-based ranking remain future work under SSE-3; formal grading is outside the current scope. Calendar integrations and additional institutional administration need separate justification before being added.

**Conclusion:** existing services already address broad exchange, language practice, campus tutoring, and professional feedback. Our proposed contribution is a clear, multi-subject exchange journey for university students: describe both learning roles, discover a suitable partner, and agree on the exchange. Student research and usability tests must establish local demand, usefulness, and whether this journey improves on students' current alternatives.

## 7. Sources and access record

Every source below was accessed or retrieved on **23 October 2026**. Publication or update dates, where noted, are separate from the access date. Official sources describe their own products and may contain promotional language; performance statistics and testimonials were not treated as independent evidence.

| ID | Official source | Access date | Evidence used and retrieval notes |
| --- | --- | --- | --- |
| S1 | [Simbi: How It Works](https://simbi.com/howitworks) | 2026-10-23 | Official indexed extract describes conversations, proposed exchanges, and direct/credit exchange. Full-page retrieval was unsuccessful, including a 403 response; detailed workflow states remain Unknown. |
| S2 | [Simbi: All Services](https://simbi.com/services) | 2026-10-23 | Category browsing, service listings, request navigation, and the explanation of internal credits. |
| S3 | [Simbi: sampled public service listing](https://simbi.com/jennifer-ferencz-barato/reserved-for-anat) | 2026-10-23 | Qualifications, availability notes, reviews, and communication described on one public listing. Later retrieval failed. The sample does not establish every member's practices or verify delivery of the service. |
| S4 | [Simbi Community Development: official organizational profile](https://simbi.com/simbi) | 2026-10-23 | Free joining/cashless model, public requests, and review display. |
| T1 | [Tandem: product homepage](https://tandem.net/) | 2026-10-23 | Language exchange, partner discovery, communication modes, and application review. |
| T2 | [Tandem: Everything You Can Do on Tandem](https://tandem.net/blog/tandem-app-overview) | 2026-10-23 | Profile fields, language-combination feed, free/Pro distinction, and described interaction tools. Exact local prices were not established. |
| T3 | [Tandem: Community Guidelines](https://tandem.net/pages/community-guidelines) | 2026-10-23 | Authentic-profile rules, reporting, moderation, and appeals. Page states last updated 14 July 2025. |
| T4 | [Tandem for Universities](https://tandem.net/pages/partnerships/universities) | 2026-10-23 | University partnerships, rollout/onboarding support, premium access, and optional usage reporting. Campus-only access and partnership prices remain Unknown. |
| K1 | [Knack: Students](https://www.joinknack.com/students) | 2026-10-23 | Campus peer tutoring, communication formats, institution-funded access, and student/course coverage limitations. |
| K2 | [Knack: Completing your Tutor Profile](https://help.joinknack.com/en/articles/3636944-completing-your-tutor-profile) | 2026-10-23 | Tutor biography, experience, and availability. Page dated 3 June 2026. |
| K3 | [Knack: Open Student Requests](https://help.joinknack.com/en/articles/3636980-open-student-requests) | 2026-10-23 | Course-based request feed, tutor responses, approval, and possible training requirements. Page dated 29 October 2024. |
| K4 | [Knack: Scheduling a Tutoring Session](https://help.joinknack.com/en/articles/3636906-scheduling-a-tutoring-session) | 2026-10-23 | Session details, tutor responses, recurrence, and eligible Instant Booking. Page dated 3 June 2026. |
| A1 | [ADPList: product homepage](https://adplist.org/) | 2026-10-23 | Professional mentor profiles, goal-aligned suggestions, and one-to-one sessions. |
| A2 | [ADPList: Find a Mentor](https://adplist.org/find-a-mentor) | 2026-10-23 | Expertise-based discovery, student audience, profiles/reviews, and the booking journey. |
| A3 | [ADPList: Become a Mentor](https://adplist.org/become-a-mentor) | 2026-10-23 | Mentor application review, topics, profiles, availability, notes, reviews, and mentor/mentee roles. Page states updated 15 October 2026; free-booking wording is qualified by A4. |
| A4 | [ADPList: Best Mentorship Platforms in 2026](https://adplist.org/guides/best-mentorship-platforms) | 2026-10-23 | Used only for ADPList's own free/paid-session description and variable availability. Page states updated 15 October 2026. Its comparisons of other providers were not used as evidence about them. |
| P1 | [Student Skill Exchange: repository README](https://github.com/HashiraOfSun/student-skill-exchange) | 2026-10-23 | Public README inspected in the browser; repository latest commit displayed as `6234b14e69aa693151e0fe9e61dcbb54e2bdd77e`. Used to align proposals with the stated project scope. |

### Related team document

**SSE-3 — Literature Review: Peer-to-Peer Skill Exchange for University Students**, supplied on 23 October 2026. Sections 6 and 7 inform the scope decisions in this report. This is a team synthesis, distinct from the official product sources above.

## 8. Review and delivery checklist

- [x] Four relevant systems are compared using the same ten criteria.
- [x] The selection reasons are explained.
- [x] Product claims are linked to sources with access dates.
- [x] Unverified capabilities are marked Unknown.
- [x] Observations are separated from team interpretations and proposals.
- [x] The conclusion explains existing approaches and the intended project contribution.
- [ ] Nursultan has reviewed this document through a pull request.
- [ ] Review comments have been resolved and the changes merged into `main`.
- [ ] The pull request is linked to the corresponding YouTrack task.

Suggested branch: `SSE-4-existing-systems-comparison`. Commit this file at `docs/research/existing-systems-comparison.md` and open a pull request into `main` with a title such as `SSE-4: compare existing skill exchange platforms`. Include the SSE-4 task link in the PR description. Nursultan must review the document; resolve any comments before merging, then add the PR link to SSE-4. Mark the task complete only after these steps are finished.

[S1]: https://simbi.com/howitworks
[S2]: https://simbi.com/services
[S3]: https://simbi.com/jennifer-ferencz-barato/reserved-for-anat
[S4]: https://simbi.com/simbi
[T1]: https://tandem.net/
[T2]: https://tandem.net/blog/tandem-app-overview
[T3]: https://tandem.net/pages/community-guidelines
[T4]: https://tandem.net/pages/partnerships/universities
[K1]: https://www.joinknack.com/students
[K2]: https://help.joinknack.com/en/articles/3636944-completing-your-tutor-profile
[K3]: https://help.joinknack.com/en/articles/3636980-open-student-requests
[K4]: https://help.joinknack.com/en/articles/3636906-scheduling-a-tutoring-session
[A1]: https://adplist.org/
[A2]: https://adplist.org/find-a-mentor
[A3]: https://adplist.org/become-a-mentor
[A4]: https://adplist.org/guides/best-mentorship-platforms
[P1]: https://github.com/HashiraOfSun/student-skill-exchange
