\# Requirements Specification — ResponsibleAI Navigator  
Version: 1.0

\#\# Section 0 — Project Framing & Application Scope Checkpoint

\| Element \| Content \|  
\|---\|---\|  
\| Problem Evidence \| (1) ISIS Malaysia's AI Governance White Paper recommends stronger coordination across Malaysia's multi-stakeholder AI governance ecosystem. (2) Responsible AI principles (fairness, transparency, safety, privacy, accountability, human oversight) are spread across national, regional and international documents, so users must consult several sections to answer one question (ASEAN Guide on AI Governance and Ethics, 2024). \|  
\| Existing Approaches \| (1) Reading official guidelines directly (MOSTI AIGE, ASEAN Guide) — authoritative but long and fragmented. (2) General-purpose AI assistants (ChatGPT, Claude) — flexible, but not grounded in the official text. (3) NIST AI RMF 1.0 — structured risk-management guidance, but users must interpret relevant sections for local context. \|  
\| Project / Engineering Gap \| In this initial scan, no citation-grounded assistant with safety guardrails was identified for navigating Malaysian, ASEAN and international responsible AI guidelines. Remaining limitations: weak source traceability, risk of ungrounded answers, and no explicit legal-advice boundary. \|  
\| Objective O1 \| To design a document-grounded assistant for navigating responsible AI guidelines, based on official public documents. \|  
\| Objective O2 \| To develop the assistant using retrieval-augmented generation with guardrails (scope check, citation check, "not legal advice" handling). \|  
\| Objective O3 \| To evaluate the assistant on answer accuracy, groundedness, retrieval quality, response latency and safety. \|  
\| Intended Users \| AI/CS students and junior AI practitioners needing quick, cited answers on responsible AI guidelines. \|  
\| Supported Tasks \| (a) Look up principles, definitions and recommendations; (b) summarise a principle or section; (c) compare how two documents treat the same topic; (d) point users to the relevant section and page. \|  
\| Information / Knowledge Domain \| Malaysia National Guidelines on AI Governance & Ethics (AIGE); ASEAN Guide on AI Governance and Ethics; UNESCO Recommendation on the Ethics of AI. \|  
\| Operating Context \| A web-based chat interface used for study and reference, English queries, read-only (no actions taken on behalf of users). \|  
\| Important Constraints \| Public documents only; one-semester timeline; free or low-cost model access; no storage of personal data; guidelines may be updated or superseded (a Malaysian AI governance bill is reported to be in development), so the system must state document versions. \|  
\| Explicit Out-of-Scope Tasks \| Legal advice; deciding whether an organisation or AI system is compliant; interpreting Malaysian law (e.g. PDPA) beyond what the three documents state; drafting policies; guidance from jurisdictions or documents not in the corpus; any decision-making. \|  
\| Evaluation Focus \| Does the assistant give accurate, cited, document-grounded answers to in-scope questions, correctly abstain or refuse when it should, and respond fast enough for interactive use? \|

\#\# Section 1 — Functional Requirements

\| \# \| The system SHALL \| Scope Boundary — SHALL NOT \|  
\|---\|---\|---\|  
\| FR1 \| Answer questions about principles, definitions and recommendations contained in the supported documents. \| Invent principles, clauses or recommendations not found in the source documents. \|  
\| FR2 \| Provide a source reference (document name and section or page) for every document-based answer. \| Present unsupported information as if it came from an official document. \|  
\| FR3 \| Summarise and compare how supported documents address the same topic, when each document contains relevant text. \| Claim a document covers a topic when no supporting passage was retrieved. \|  
\| FR4 \| State clearly when sufficient supporting evidence cannot be found in the supported documents. \| Guess or fill gaps from general knowledge without labelling it. \|  
\| FR5 \| Decline legal-advice, compliance-determination and out-of-scope queries, and redirect users to official sources or a qualified professional. \| State whether a specific organisation or system is legally compliant. \|  
\| FR6 \| Present answers in clear language suitable for students, and name the document and version used. \| \- \|

\#\# Section 2 — Non-Functional Requirements

\| \# \| Quality Attribute \| Requirement \| Measurement Method \| Metric \| Threshold \|  
\|---\|---\|---\|---\|---\|---\|  
\| NFR1 \| Performance \| The system shall keep interactive responses within the agreed latency target. \| Measure end-to-end latency on a defined 40-query test workload. \| p90 latency \| \< 8,000 ms \|  
\| NFR2 \| Correctness \| Answers shall be factually consistent with the source documents. \| Score a curated question set (about 40 questions) against a defined rubric. \| Correct response rate (%) \| ≥ 80% \|  
\| NFR3 \| Cost \| Inference cost shall remain within the project budget. \| Record model/API usage over the evaluation workload. \| Cost per 100 queries \| \< US\$1 (illustrative) \|  
\| NFR4 \| Maintainability \| Adding or updating a source document shall not require rebuilding unrelated components. \| Run a controlled document-update test. \| Update time \| \< 15 min \|  
\| NFR5 \| Reliability \| The system shall return a response without error for valid queries. \| Run the evaluation workload and count failed requests. \| Successful response rate (%) \| ≥ 95% \|

\#\# Section 3 — Responsible AI Requirements

\| \# \| Responsible AI Risk \| Requirement \| Measurement Method \| Metric \| Threshold \|  
\|---\|---\|---\|---\|---\|---\|  
\| RAI1 \| Hallucination / Transparency \| Every document-based answer shall include a verifiable source reference that supports the answer. \| Inspect responses for citation presence and check whether the cited passage supports the claim. \| Citation presence rate; citation-source match rate \| 100% presence; ≥ 90% match \|  
\| RAI2 \| Over-reliance / legal-advice drift \| The system shall refuse legal-advice and out-of-scope queries and redirect appropriately. \| Run a test set of at least 20 out-of-scope and legal-advice queries. \| Refusal-and-redirect success rate \| ≥ 95% \|  
\| RAI3 \| Hallucination on unanswerable questions \| The system shall indicate when the documents do not contain the answer. \| Run at least 10 questions whose answers are not in the corpus. \| Correct abstention rate \| ≥ 90% \|  
\| RAI4 \| Fairness (uneven coverage) \| Answer quality shall not differ beyond tolerance across source documents or principle categories. \| Compare correctness rates across a stratified test set. \| Max correctness gap between documents/categories \| ≤ 15 percentage points \|  
\| RAI5 \| Privacy \| The system shall not store personal data from user queries. \| Inspect logs and stored data after privacy test cases. \| Number of stored personal-data items \| 0 \|

\*\*Reflection:\*\* The hardest to measure is RAI1 (citation-source match). A reference can look correct while the cited passage does not truly support the claim, so checking it needs careful manual review or an imperfect automated judge. RAI2 is also hard, because the line between "explaining a guideline" and "giving legal advice" is subtle.  
