# Findings for the thesis on RAG pipelines for academic regulations

- Did the pipeline retrieve every applicable clause, including exceptions?
- Did the answer apply those clauses correctly and cite the right edition?
- How long did the student wait, and how many tokens did the pipeline use?

## Building the question set and reference answers

### [Wojtasik et al. (2025) - PoliChat](notes/wojtasik-2025-polichat.md)

- Annotators checked 100 answerable questions against 2,350 university documents. They used keyword searches to find evidence the retriever might have missed.
- Adapt this approach to questions written in the language of my university’s regulations. Record the expected answer, required provisions, and acceptable citations for each question.
- Score citations and conclusions separately. In one experiment, a prompt change improved citation F1 while answer correctness fell.

### [Pipitone and Houir Alami (2024) - LegalBench-RAG](notes/pipitone-2024-legalbench-rag.md)

- Mark the start and end of each supporting passage in the source document. The same annotations then work for fixed-length chunks and chunks split by article.
- Measure how much of the required text each pipeline retrieves and how much of its retrieved text is relevant.
- Include questions that require passages from two documents, such as a university-wide rule and a faculty exception.

### [Tsai and Huang (2026) - From Policy to Practice](notes/tsai-2026-from-policy-to-practice.md)

- Store the document title, article identifier, issuance date, and source link with each passage so students can verify the applicable edition.
- Reviewers judged 1,644 of 1,742 answers correct. To investigate individual errors in my comparison, save each question’s retrieved passages, answer, citations, and reviewer decision.
- The assistant gave unsupported advice on an out-of-scope question. Include questions the regulations cannot settle and check whether the system recognizes the missing evidence.

## Comparing retrieval pipelines

### [Liley (2026) - Chunk-level retrieval on university regulations](notes/liley-2026-chunk-level-retrieval.md)

- Hybrid retrieval found all required passages in the top eight for 21 of 24 questions. Dense retrieval did so for 19 and BM25 keyword retrieval for 18.
- All three methods succeeded on eight of nine keyword questions. Report results separately for exact terms, student paraphrases, and questions requiring several provisions.
- Record the rank of the last required clause. For a resit question, this shows how many passages the generator needs before it has both the general rule and the exception.
- Removing section headings hurt retrieval on multi-hop questions. Test the effect of headings using otherwise identical chunks.

### [Tariq and Suleman (2026) - Hybrid RAG for university policy](notes/tariq-2026-agentic-hybrid-rag-university-policy.md)

- On 60 handbook questions with the same generator, the average of four RAGAS metrics rose from 0.66 for dense retrieval to 0.76 for hybrid retrieval with reranking. Adding a retrieval check and question decomposition raised it to 0.83.
- Run BM25, dense retrieval, hybrid retrieval, and hybrid retrieval with reranking separately to isolate the contribution of each change.
- Include a fee from a PDF table and a penalty from a revised regulation. The study found errors caused by broken number extraction and answers quoting superseded rules.

### [Ferrazzi et al. (2026) - Is Agentic RAG Worth It?](notes/ferrazzi-2026-is-agentic-rag-worth-it.md)

- Adaptive query rewriting improved average ranking across four datasets. On the finance dataset, the original query ranked relevant material highest.
- Compare an exact article-number query with a student paraphrase of the same question. Track whether rewriting moves the governing clause up the ranking.
- In a separate two-dataset experiment, fixed reranking outperformed repeated agentic retrieval. On average, 53% of documents appeared again in a repeat search.
- For each follow-up search, record whether it found a missing provision and how much time it added.

### [Neha and Bhati (2025) - Traditional and agentic RAG](notes/neha-2025-traditional-rag-vs-agentic-rag.md)

- The review describes an agentic pipeline that inspects the first results and decides whether to search again.
- Test that decision on a clause that refers to another article. Give both the single-pass and agentic pipelines the same corpus, retriever, and generator.
- Log the follow-up query and its results to check whether the system found the referenced article or followed a similar rule for the wrong programme.

## Evaluating answers and the deployed system

### [Friel et al. (2025) - RAGBench](notes/friel-2025-ragbench.md)

- The TRACe framework measures how much retrieved text is relevant, how much the answer uses, how completely it covers the relevant evidence, and whether its claims have support.
- If the retriever misses a required exception, record a retrieval failure. If it supplies the exception and the answer omits it, record an incomplete answer.
- Check the edition of the cited clause. An answer can faithfully reproduce last year’s deadline and still mislead this year’s students.

### [Şakar and Emekci (2025) - Maximizing RAG Efficiency](notes/sakar-2025-maximizing-rag-efficiency.md)

- On financial filings, a single generation over retrieved passages took a median of 14.93 seconds with answer similarity of 0.895. Reciprocal RAG took 24.56 seconds with similarity of 0.971.
- Check deadlines and units against the source clause. “Five working days” and “five calendar days” can receive similar scores while giving students different instructions.
- In vLLM, record end-to-end latency and actual input and output tokens across all calls for each question.
- When filtering context to save tokens, check whether the filter removed an exception needed for the answer.

### [Hasan et al. (2026) - Engineering RAG Systems](notes/hasan-2026-engineering-rag-systems.md)

- Of 22 users of a municipal-policy assistant, about 91% rated accuracy positively and 45.5% found the sourcing unclear.
- For a student usability test, ask participants to follow a citation and locate the clause supporting the answer. Record how many succeed.
- The authors encountered OCR errors. Check extracted article numbers and table values against the PDFs, then give every pipeline the same verified corpus.
- Record the model revision, vLLM version, and hardware so later runs can reproduce the deployment conditions.
