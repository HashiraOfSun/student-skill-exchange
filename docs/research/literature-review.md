# Literature Review: Peer-to-Peer Skill Exchange for University Students

**Project:** Development of a Peer-to-Peer Skill Exchange Platform for University Students  
**Task:** SSE-3  
**Status:** Ready for team review  
**Review type:** Targeted narrative review with a structured source analysis

## 1. Purpose and review scope

The proposed platform will help university students describe the skills they can teach, specify the skills they want to learn, discover potentially compatible peers, and request a learning exchange. This review examines three bodies of research that are directly relevant to that goal:

1. peer learning in higher education;
2. reciprocal, people-to-people recommendation;
3. motivation, trust, reputation, and interface transparency.

The review combines foundational publications with recent work published from 2021 to 2023. Bibliographic details were checked against DOI records or official publisher and proceedings pages. The review is targeted rather than systematic: it does not claim to identify every study in these fields. Its purpose is to provide an evidence-informed basis for the first product requirements and to identify assumptions that still require validation with target users.

## 2. Peer learning in higher education

Peer learning covers several different arrangements rather than one uniform teaching method. Topping (1996) distinguishes models by factors such as participants' year of study, group size, role continuity, place, time, and learning objective. His review supports the value of several structured forms of peer tutoring, but it does not imply that every informal student-to-student interaction will improve learning. The design and context of the activity remain important.

The same distinction appears in the study by Topping et al. (1996). Forty-five first-year calculus students completed twelve one-hour paired-tutoring sessions. Their examination performance was better than that of the previous year's cohort, and students reported gains in transferable skills. However, the cohorts were not equivalent, so the study cannot establish that peer tutoring alone caused the difference. The study is useful for showing what a structured exchange may look like, while its design cautions against making strong causal claims.

Boud, Cohen, and Sampson (1999) focus on the relationship between peer learning and assessment. They argue that assessment can support collaboration through peer feedback and shared responsibility, but it can also undermine collaboration when only individual achievement is rewarded. This is relevant to the platform because feedback should support reflection and coordination rather than turn every exchange into formal grading.

Recent evidence strengthens the case for studying peer learning while preserving this caution. Bengesai, Amusa, and Dhunpath (2023) screened 1,645 records and included 37 controlled or comparison-group studies in a meta-analysis of formal peer-learning approaches in undergraduate education. They found a moderately strong positive relationship with course performance, while also noting geographical concentration, substantial representation of STEM subjects, and a need for more context-specific experimental evidence.

Two recent studies address online environments. Tang, Lau, and Chau (2022) surveyed 204 sub-degree students who had participated in an online peer-learning revision centre. Factor and correlation analyses connected learning ability, attitude, motivation, and interpersonal relationships, but the self-report design and single setting limit generalisation. Mendieta-Aragón et al. (2023) studied 78 engineering students who created or consumed peer-produced videos in a hybrid university course. Participants evaluated the activity positively, especially those who acted as peer teachers. Participation was voluntary, and outcomes relied substantially on student perceptions, so the findings show acceptance and perceived value rather than a definitive causal effect on achievement.

Taken together, these studies support a platform that makes learning goals, offered skills, requested skills, and participant roles explicit. They also support voluntary participation and simple guidance for arranging an exchange. They do not establish that a matching platform will automatically improve academic performance; that outcome must be evaluated after the platform is used.

## 3. Reciprocal matching and recommendation

Traditional recommender systems suggest passive items to a user. A people-to-people system is different because a useful match depends on both participants. Pizzato et al. (2010) formalised this distinction and identified applications such as finding a mentor, business partner, employee, or date. Their work is conceptual and illustrated through online dating, but the core requirement transfers to skill exchange: the proposed relationship should be acceptable and useful to both students.

Vitale, Parotsidis, and Gentile (2018) formalised online reciprocal recommendation as a sequential-learning problem. Their algorithms were evaluated on synthetic and real-world datasets and performed better than simple baselines under stated assumptions. The work shows why mutual interest must be modelled explicitly, but it does not provide a directly deployable algorithm for a new university platform with no interaction history.

Neve and Palomares (2019) studied how two directional preference scores can be combined into one compatibility score. Their experiments show that the aggregation rule affects precision and F1 performance; in their setting, a cross-ratio approach outperformed the harmonic mean. This result is useful as evidence that a reciprocal score should not be chosen arbitrarily, although it comes from one model and dataset rather than a university skill-exchange deployment.

Palomares et al. (2021) review the broader reciprocal-recommender literature. They identify preference prediction, fusion of two one-sided preferences, evaluation, data sparsity, and application-specific requirements as central issues. Chang et al. (2022) provide a more recent graph-neural-network approach for reciprocal friend recommendation in an online gaming service. Their model separates preference, attractiveness, and similarity and performs well on large real-world datasets. Its data and infrastructure needs are far beyond those of an initial university prototype.

The appropriate first implementation is therefore a transparent rule-based match. A direct reciprocal match exists when Student A offers a skill that Student B wants and Student B offers a skill that Student A wants. Additional filters, such as availability or preferred session format, should be included only if student research shows that they materially affect partner choice. Machine-learning and graph-based ranking should remain future work until the platform has sufficient interaction data and a validated evaluation metric.

## 4. Motivation, trust, reputation, and transparency

Self-determination theory identifies autonomy, competence, and relatedness as basic psychological needs associated with self-directed motivation and well-being (Ryan & Deci, 2000). Applied cautiously, this suggests that students should control their learning goals, decide which exchanges to accept, present skills they feel competent to teach, and interact with peers rather than being assigned automatically. The theory provides a design rationale, not proof that these interface choices will cause sustained use.

Resnick et al. (2000) explain how reputation systems collect and distribute information about past behaviour to support interaction between people who do not already know each other. The article provides a foundation for considering reviews or participation history, but it also concerns internet transactions rather than university learning. A rating feature may introduce cold-start, bias, retaliation, and moderation problems. It should not be treated as a required MVP feature without user and supervisor approval.

Kizilcec (2016) tested three levels of interface transparency in an online field experiment involving peer assessment. When a result violated participants' expectations, an explanation could restore trust, but excessive information reduced trust. The practical lesson is balance: the platform should provide a short, concrete reason for a recommendation, such as “You want to learn Python; this student offers Python and wants to learn English, which you offer.” It should not expose users to an opaque score or a long technical explanation.

## 5. Structured source analysis

| Source | Method and context | Main finding used in this project | Important limitation | Project implication |
|---|---|---|---|---|
| Topping (1996) | Typology and review of peer tutoring in further and higher education | Structured peer-tutoring models can support learning | Broad and dated review; outcomes vary by design and context | Define skills, goals, roles, and exchange format clearly |
| Boud et al. (1999) | Conceptual analysis of peer learning and assessment | Assessment design can support or undermine collaboration | Does not evaluate a digital matching platform | Keep feedback developmental; avoid compulsory grading in the MVP |
| Topping et al. (1996) | Paired-tutoring study with 45 calculus students and 12 sessions | Structured paired tutoring was associated with better results and reported transferable skills | Previous-year comparison group was non-equivalent | Offer a simple structure for planning sessions; evaluate outcomes cautiously |
| Ryan & Deci (2000) | Theoretical review of self-determination research | Autonomy, competence, and relatedness are central to self-directed motivation | General psychological theory, not a platform trial | Let students choose goals, skills, and partners and accept or reject requests |
| Resnick et al. (2000) | Conceptual article on online reputation systems | Visible information about prior behaviour can support trust among strangers | Commercial transaction focus; reputation can be biased or manipulated | Treat reviews/reputation as a validated future feature, not an automatic MVP requirement |
| Pizzato et al. (2010) | Conceptual workshop paper with an online-dating case study | People-to-people recommendation must consider both parties | Early work; domain differs from education | Match offered and wanted skills in both directions |
| Kizilcec (2016) | Online field experiment with three transparency levels in peer assessment | A concise explanation can repair trust; too much information can reduce it | Peer-assessment context and expectation-violation condition | Show a brief human-readable reason for each suggested match |
| Vitale et al. (2018) | Theoretical sequential-learning model tested on synthetic and real data | Reciprocal matching differs formally from one-sided recommendation | Relies on structural assumptions and existing interaction data | Do not use a one-sided recommendation score; postpone learning-based ranking |
| Neve & Palomares (2019) | Comparative experiment on bidirectional-score aggregation | The choice of aggregation function changes recommendation quality | One model and dataset; no education-specific validation | If ranking is added later, compare aggregation methods rather than selecting one without evidence |
| Palomares et al. (2021) | State-of-the-art review of reciprocal recommender systems | Mutual compatibility requires preference prediction, fusion, and suitable evaluation | Survey spans domains with different goals and risks | Define success as an accepted, useful match for both students |
| Tang et al. (2022) | Survey of 204 participants in an online peer-learning revision centre | Learning, motivation, attitudes, and interpersonal factors were closely related | Self-report, single context, no non-participant control group | Measure motivation and relationship quality during evaluation, not only number of matches |
| Chang et al. (2022) | Multiplex-graph neural network evaluated on online-gaming data | Preference, attractiveness, and similarity can be modelled separately at scale | Complex, data-intensive, and outside the education domain | Keep GNN-based matching outside the MVP; revisit only after sufficient data exists |
| Mendieta-Aragón et al. (2023) | Survey-based study of 78 engineering students in hybrid learning | Students valued digital peer learning; peer teachers reported motivational and skill benefits | Voluntary sample and subjective outcomes limit causal inference | Make exchanges voluntary and evaluate teacher and learner experiences separately |
| Bengesai et al. (2023) | Meta-analysis of 37 undergraduate studies selected from 1,645 records | Formal peer learning has a moderately strong positive relationship with course performance | Evidence is concentrated geographically and in STEM; interventions vary | Peer learning is plausible, but effectiveness must be tested in the local university context |

## 6. Research gap

The literature supports structured peer learning and shows that people-to-people matching should account for both participants. It also offers design principles for autonomy, trust, and explanation. However, none of the reviewed studies establishes that students at Astana IT University currently have a substantial problem finding skill-exchange partners or that they would repeatedly use a dedicated platform.

The main project gap is therefore contextual and integrative. Existing work studies peer-learning interventions, reciprocal algorithms, or trust mechanisms separately and usually in other institutions or domains. The proposed project will test whether a simple combination of these ideas is useful for the target students.

SSE-2 should validate the following assumptions:

- students currently find it difficult or time-consuming to locate suitable partners;
- students are willing both to teach and to learn;
- offered and wanted skills are sufficient for initial partner discovery;
- availability, language, session format, or proficiency level materially influence partner choice;
- students are comfortable contacting peers through the proposed request flow;
- students want post-exchange feedback and understand how it would be used.

## 7. Evidence-informed scope decisions

| Decision | Status | Rationale |
|---|---|---|
| Profiles with offered and wanted skills | Include in MVP | Required for structured peer learning and reciprocal matching |
| Search and direct reciprocal matches | Include in MVP | Implements mutual compatibility without requiring historical data |
| Short explanation for a suggested match | Include in MVP | Supports appropriate transparency without information overload |
| Request, accept, or decline an exchange | Include in MVP | Preserves autonomy and confirms mutual interest |
| Availability, language, proficiency, and session-format filters | Validate through SSE-2 | Plausible constraints, but their importance to target users is not yet established |
| Ratings or public reputation scores | Future candidate | May support trust but introduces cold-start, bias, moderation, and retaliation risks |
| Machine-learning or graph-based ranking | Future candidate | Requires interaction data, evaluation metrics, and more implementation complexity |
| Formal peer assessment or grading | Outside current scope | The project supports skill exchange rather than academic assessment |

## 8. Conclusion

The evidence supports three design principles. First, peer learning works best when goals, roles, and activities are structured. Second, partner discovery is a reciprocal problem: a useful match must account for both students. Third, autonomy and concise explanations should be built into the interaction, while ratings and complex recommendation algorithms should be added only after validation.

These findings justify a small, transparent MVP centred on profiles, offered and wanted skills, reciprocal partner discovery, and exchange requests. They do not prove local demand or educational effectiveness. Those claims must be tested through the SSE-2 questionnaire and later usability and outcome evaluation.

## References

1. Topping, K. J. (1996). The effectiveness of peer tutoring in further and higher education: A typology and review of the literature. *Higher Education, 32*(3), 321–345. https://doi.org/10.1007/BF00138870
2. Boud, D., Cohen, R., & Sampson, J. (1999). Peer learning and assessment. *Assessment & Evaluation in Higher Education, 24*(4), 413–426. https://doi.org/10.1080/0260293990240405
3. Topping, K. J., Watson, G. A., Jarvis, R. J., & Hill, S. (1996). Same-year paired peer tutoring with first year undergraduates. *Teaching in Higher Education, 1*(3), 341–356. https://doi.org/10.1080/1356251960010305
4. Ryan, R. M., & Deci, E. L. (2000). Self-determination theory and the facilitation of intrinsic motivation, social development, and well-being. *American Psychologist, 55*(1), 68–78. https://doi.org/10.1037/0003-066X.55.1.68
5. Resnick, P., Zeckhauser, R., Friedman, E., & Kuwabara, K. (2000). Reputation systems. *Communications of the ACM, 43*(12), 45–48. https://doi.org/10.1145/355112.355122
6. Pizzato, L., Rej, T., Chung, T., Yacef, K., Koprinska, I., & Kay, J. (2010). Reciprocal recommenders. In *Proceedings of the 8th Workshop on Intelligent Techniques for Web Personalization & Recommender Systems (ITWP 2010)* (CEUR Workshop Proceedings, Vol. 606, pp. 53–64). https://ceur-ws.org/Vol-606/
7. Kizilcec, R. F. (2016). How much information? Effects of transparency on trust in an algorithmic interface. In *Proceedings of the 2016 CHI Conference on Human Factors in Computing Systems* (pp. 2390–2395). https://doi.org/10.1145/2858036.2858402
8. Vitale, F., Parotsidis, N., & Gentile, C. (2018). Online reciprocal recommendation with theoretical performance guarantees. *Advances in Neural Information Processing Systems, 31*. https://proceedings.neurips.cc/paper/2018/hash/97af07a14cacba681feacf3012730892-Abstract.html
9. Neve, J., & Palomares, I. (2019). Aggregation strategies in user-to-user reciprocal recommender systems. In *2019 IEEE International Conference on Systems, Man and Cybernetics (SMC)* (pp. 4031–4036). https://doi.org/10.1109/SMC.2019.8914362
10. Palomares, I., Porcel, C., Pizzato, L., Guy, I., & Herrera-Viedma, E. (2021). Reciprocal recommender systems: Analysis of state-of-art literature, challenges and opportunities towards social recommendation. *Information Fusion, 69*, 103–127. https://doi.org/10.1016/j.inffus.2020.12.001
11. Tang, Y. M., Lau, Y. Y., & Chau, K. Y. (2022). Towards a sustainable online peer learning model based on student's perspectives. *Education and Information Technologies, 27*(9), 12449–12468. https://doi.org/10.1007/s10639-022-11136-y
12. Chang, Y., Shu, L., Du, E., Chen, C., Zhang, Z., Zheng, Z., Huang, Y., & Xing, X. (2022). GraphRR: A multiplex graph based reciprocal friend recommender system with applications on online gaming service. *Knowledge-Based Systems, 251*, 109187. https://doi.org/10.1016/j.knosys.2022.109187
13. Mendieta-Aragón, A., Arguedas-Sanz, R., Ruiz-Gómez, L. M., & Navío-Marco, J. (2023). Tackling the challenge of peer learning in hybrid and online universities. *Education and Information Technologies, 28*(4), 4505–4529. https://doi.org/10.1007/s10639-022-11397-7
14. Bengesai, A. V., Amusa, L. B., & Dhunpath, R. (2023). A meta-analysis on the effect of formal peer learning approaches on course performance in higher education. *Cogent Education, 10*(1), 2203990. https://doi.org/10.1080/2331186X.2023.2203990
