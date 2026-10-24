# Evaluation Criteria — ResponsibleAI Navigator

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold | User / Business Outcome |
|---|---|---|---|---|---|---|
| O3 / NFR2 | Answer correctness | Domain-specific capability | Evaluate a curated set of about 40 in-scope questions against a rubric based on the source documents. | Correct response rate | ≥ 80% | Users receive reliable answers about responsible AI guidelines. |
| O1 / FR2 / RAI1 | Source citation and support | Instruction-following capability | Inspect responses for citation presence and verify that the cited passage supports the answer. | Citation presence rate; citation-source match rate | 100% presence; ≥ 90% match | Users can verify answers against official documents. |
| O2 / FR5 / RAI2 | Out-of-scope and legal-advice refusal | Instruction-following capability | Test with at least 20 out-of-scope and legal-advice queries. | Refusal-and-redirect success rate | ≥ 95% | Reduces the risk of users treating answers as legal advice. |
| O3 / FR4 / RAI3 | Abstention when evidence is missing | Domain-specific capability | Test with at least 10 questions not answerable from the corpus. | Correct abstention rate | ≥ 90% | Users are not given invented guidance. |
| O3 / NFR1 | Response latency | Cost and latency | Measure end-to-end response time across the evaluation workload. | p90 latency | < 8 s | Users get a sufficiently responsive study tool. |
| O1 / FR6 | Response clarity | Generation capability | Rate responses with a simple 3-point clarity rubric. | Clarity rubric score | Average ≥ 2 out of 3 | Students can understand policy language. |

**Reflection:** Citation support (RAI1) is the most important criterion. Users rely on citations to verify answers, so an assistant that cites unsupported passages would look trustworthy while misleading them.
