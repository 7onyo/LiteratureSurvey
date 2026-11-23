# Literature survey for “Design and Comparative Evaluation of Retrieval-Augmented Generation Pipelines for Academic Regulations”

This repository it's used to collect the literature related to my thesis on answering questions about academic regulations using RAG. A RAG pipeline retrieves passages from official documents and uses them as evidence to generate an answer.

The thesis aims to compare how reliably different pipelines find the applicable provisions and use them to give a correct answer with supporting citations. For example, a student asking whether they can retake an exam may need both the general resit rule and an exception that applies to their programme. Evaluating retrieval and answer quality separately helps identify whether a pipeline missed the exception or retrieved it and then failed to apply it.

## Focus of the literature survey

- **Academic regulations and university policy.** How have other studies chosen source documents, collected realistic student questions, and established reference answers?
- **Pipeline design.** How do choices such as splitting documents by section, combining keyword and semantic search, or reranking passages affect which provisions reach the generator?
- **Comparative evaluation.** How can the thesis measure retrieval coverage, answer correctness, citation support, and the ability to recognize insufficient evidence? What do improvements cost in response time and token use?

## Repository contents

The [papers directory](papers/) contains collected publications in PDF format. The [BibTeX bibliography](references.bib) is being compiled to provide complete citation details for each source considered. The [reading notes](notes.md) explain and lists some of the important findings for each paper. 

- [Wojtasik et al. (2025) — PoliChat](notes/wojtasik-2025-polichat.md)
- [Liley (2026) — Chunk-level retrieval evaluation on university regulations](notes/liley-2026-chunk-level-retrieval.md)
- [Ferrazzi et al. (2026) — Is Agentic RAG worth it?](notes/ferrazzi-2026-is-agentic-rag-worth-it.md)
- [Friel et al. (2025) — RAGBench](notes/friel-2025-ragbench.md)
- [Hasan et al. (2026) — Engineering RAG Systems for Real-World Applications](notes/hasan-2026-engineering-rag-systems.md)
- [Neha and Bhati (2025) — Traditional RAG vs. Agentic RAG](notes/neha-2025-traditional-rag-vs-agentic-rag.md)
- [Pipitone and Houir Alami (2024) — LegalBench-RAG](notes/pipitone-2024-legalbench-rag.md)
- [Şakar and Emekci (2025) — Maximizing RAG efficiency](notes/sakar-2025-maximizing-rag-efficiency.md)
- [Tariq and Suleman (2026) — Agentic hybrid RAG for university policy navigation](notes/tariq-2026-agentic-hybrid-rag-university-policy.md)
- [Tsai and Huang (2026) — From policy to practice](notes/tsai-2026-from-policy-to-practice.md)
