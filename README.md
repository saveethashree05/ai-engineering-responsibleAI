# ai-engineering-responsibleAI
# ResponsibleAI — Responsible AI Guideline Navigator
> A document-grounded assistant that answers questions about responsible AI guidelines, with citations, for AI students and junior practitioners.

## Problem Statement
Guidance on responsible AI is spread across several long official documents (national, regional and international) written in formal policy language. New students and junior practitioners often find it difficult to locate and interpret relevant principles quickly. AI engineering makes it possible to build a document-grounded question-answering assistant that retrieves the relevant passages and answers with appropriate citations.

## Evidence of the Problem
- Malaysia's AI governance ecosystem involves multiple stakeholders and governance initiatives. The ISIS Malaysia white paper recommends stronger coordination of AI policymaking and governance.
  Source: Institute of Strategic and International Studies (ISIS) Malaysia. *AI Governance White Paper.* https://www.mydigital.gov.my/wp-content/uploads/2025/01/AI-Governance_White_Paper-ISIS.pdf
- Responsible AI guidance covers multiple principles (fairness, transparency, safety, privacy, accountability, human oversight) documented across international and regional frameworks, so users must consult several sections to answer specific questions.
  Source: ASEAN Secretariat. (2024). *ASEAN Guide on AI Governance and Ethics.* https://asean.org/wp-content/uploads/2024/02/ASEAN-Guide-on-AI-Governance-and-Ethics_beautified_201223_v2.pdf

## Initial Related Work / Existing Approaches
- **Reading official guidelines directly** — authoritative, but long, fragmented across documents, and hard to search by question.
  Sources: [Malaysia National Guidelines on AI Governance and Ethics](https://www.mosti.gov.my/wp-content/uploads/2024/09/NATIONAL-GUIDELINES-OF-AIGE-20241118.pdf); [ASEAN Guide on AI Governance and Ethics](https://asean.org/wp-content/uploads/2024/02/ASEAN-Guide-on-AI-Governance-and-Ethics_beautified_201223_v2.pdf)
- **General-purpose AI assistants (e.g. ChatGPT, Claude)** — flexible, but answers may not be grounded in the official text and may hallucinate.
  Source: https://chatgpt.com/
- **NIST AI Risk Management Framework (AI RMF 1.0)** — structured guidance for managing AI risks, but users still need to identify and interpret the relevant sections for their specific questions and local context.
  Source: Tabassi, E. (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0).* NIST. https://doi.org/10.6028/NIST.AI.100-1

## Engineering Gap / Limitation
In this initial scan, no citation-grounded assistant with safety guardrails was identified for navigating Malaysian and ASEAN responsible AI guidelines, so users must manually search fragmented documents or rely on general-purpose chatbots that are not grounded in the official text. This project addresses the gap with a retrieval-augmented question-answering assistant over Malaysian, ASEAN and international responsible AI guidelines, with source-grounded answers, citation verification and safety guardrails.

## Project Objectives
- O1: To design a document-grounded assistant for navigating responsible AI guidelines, based on official public documents.
- O2: To develop the assistant using retrieval-augmented generation with guardrails (scope check, citation check, "not legal advice" handling).
- O3: To evaluate the assistant in terms of answer accuracy, groundedness, retrieval quality, response latency and safety.

## Target Users
AI students and junior AI practitioners who need quick, cited answers about responsible AI guidelines.

## Data Sources
- National Guidelines on AI Governance & Ethics — https://www.mosti.gov.my/wp-content/uploads/2024/09/NATIONAL-GUIDELINES-OF-AIGE-20241118.pdf
- ASEAN Guide on AI Governance and Ethics — https://asean.org/wp-content/uploads/2024/02/ASEAN-Guide-on-AI-Governance-and-Ethics_beautified_201223_v2.pdf
- UNESCO Recommendation on the Ethics of AI — https://www.unesco.org/en/legal-affairs/recommendation-ethics-artificial-intelligence

## Responsible AI Risks
- **Hallucination:** the model invents a policy or principle that is not in the guidelines, so the user cites or applies guidance that does not exist.
- **Over-reliance / legal-advice drift:** the user treats answers as legal or compliance advice, resulting in poor decisions in real projects.

