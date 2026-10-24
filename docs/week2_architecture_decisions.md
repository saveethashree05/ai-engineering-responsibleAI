# Architecture Decisions & Traceability — ResponsibleAI Navigator

## Architecture Decision Records

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
|---|---|---|---|---|
| Include knowledge access | FR1, FR2, NFR2, RAI1: answers must be grounded in official documents and traceable | Language model only; static keyword search; dynamic knowledge access | Dynamic knowledge access component over the approved documents | More system complexity, but better grounding and source traceability |
| Include explicit scope / safety control | FR5, RAI2: legal-advice and out-of-scope queries must be refused | Instruction in the model prompt only; explicit scope-control component | Explicit scope control component | Possible false refusals and extra processing time, but more reliable refusal behaviour |
| Include grounding / citation check on outputs | FR4, RAI1, RAI3: answers must be supported and abstain when evidence is missing | Trust model output; separate output check | Separate output check before the response is returned | Added latency and possible rejection of valid answers, but fewer unsupported answers |

## Architecture needs from requirements
[Paste the Step C2 table from above]

## Initial Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
|---|---|---|---|---|
| O1 | FR2, RAI1 | Source citation and support | Knowledge Access + Grounding / Citation Check | Citation presence and match results |
| O2 | FR5, RAI2 | Out-of-scope and legal-advice refusal | Scope / Safety Control | Refusal test-set results |
| O3 | FR1, NFR2 | Answer correctness | Knowledge Access + Language Model Service | Correct response rate on the curated question set |
| O3 | FR4, RAI3 | Abstention when evidence is missing | Grounding / Citation Check | Abstention test results |
| O3 | NFR1 | Response latency | Whole request path | p90 latency measurement |
