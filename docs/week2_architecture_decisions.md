# Architecture Decisions & Traceability — ResponsibleAI Navigator
Version: 1.0

V1 conceptual architecture diagram: `docs/week2_architecture_v1.png`

## 1. Simplest Architecture (Step C1)
User Query → AI Application → Language Model → Response

This simple flow cannot satisfy the requirements: it cannot provide verifiable source references (FR2, RAI1), cannot reliably refuse legal-advice or out-of-scope queries (FR5, RAI2), is not grounded in the official documents (FR1, NFR2), and cannot indicate when evidence is missing (FR4, RAI3). Components were therefore added only where a requirement justified them.

## 2. Architecture Needs from Requirements (Step C2)

| Requirement ID | What does the requirement need? | Architecture Response |
|---|---|---|
| FR1 / NFR2 | Answers must be consistent with the official documents | Knowledge Source + Knowledge Access |
| FR2 / RAI1 | Every document-based answer needs a verifiable source reference | Source information passed with retrieved passages; Grounding / Citation Check |
| FR4 / RAI3 | The system must say when the documents do not contain the answer | Grounding / Citation Check with a "not found in documents" path |
| FR5 / RAI2 | Legal-advice and out-of-scope queries must be refused and redirected | Scope / Safety Control + Refusal and Redirect |
| NFR1 | Responses must meet the latency target | Limited number of retrieved passages; short request path |
| NFR4 | Documents must be updatable without rebuilding other components | Knowledge Source kept separate from the application |
| RAI5 / evaluation criteria | No personal data stored; evidence needed for scoring | Evaluation Point that records only test queries, retrieved passages and answers |

## 3. Architecture Decision Records

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
|---|---|---|---|---|
| ADR1: Include knowledge access | FR1, FR2, NFR2, RAI1: answers must be grounded in official documents and traceable | Language model only; static keyword search; dynamic knowledge access | Dynamic knowledge access component over the approved documents | More system complexity, but better grounding and source traceability |
| ADR2: Include explicit scope / safety control | FR5, RAI2: legal-advice and out-of-scope queries must be refused | Instruction in the model prompt only; explicit scope-control component | Explicit scope-control component before knowledge access | Possible false refusals and additional processing time, but more reliable refusal behaviour |
| ADR3: Include grounding / citation check on outputs | FR4, RAI1, RAI3: answers must be supported and abstain when evidence is missing | Trust the model output; separate output check | Separate output check before the response is returned | Added latency and occasional rejection of valid answers, but fewer unsupported answers reach the user |

## 4. Initial Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
|---|---|---|---|---|
| O1 | FR2, RAI1 | Source citation and support | Knowledge Access + Grounding / Citation Check | Citation presence and citation-source match results |
| O2 | FR5, RAI2 | Out-of-scope and legal-advice refusal | Scope / Safety Control | Refusal test-set results (at least 20 queries) |
| O3 | FR1, NFR2 | Answer correctness | Knowledge Access + Language Model Service | Correct response rate on the curated question set |
| O3 | FR4, RAI3 | Abstention when evidence is missing | Grounding / Citation Check | Abstention test results (at least 10 queries) |
| O3 | NFR1 | Response latency | Whole request path | p90 latency measurement |

## 5. Final Review Checklist

- **Does each major component support a requirement or evaluation need?** Yes. Each component is mapped to requirement IDs in Section 2.
- **Is any important data source, safety control, or evaluation point missing?** No missing component identified for V1. Monitoring and deployment are deferred to later topics.
- **Have I added any technology or component that is not yet justified?** No. Components are labelled by function and no specific models, databases or frameworks are named.
- **Is there a simpler architecture that could still satisfy the requirements?** Possibly, for example by merging the grounding check into the model prompt. This would be tested against the RAI1 and RAI3 thresholds before being adopted, because the simple version cannot guarantee citation support.

## 6. Reflection
The most important trade-off is ADR3 (grounding / citation check). It is driven by RAI1 and RAI3, which require supported citations and honest abstention. The accepted trade-off is extra latency and occasional rejection of valid answers. The component is also the hardest to verify automatically, because a citation can look correct while the cited passage does not support the claim.
