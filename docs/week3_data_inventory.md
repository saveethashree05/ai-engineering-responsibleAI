# Week 3 Data Inventory — ResponsibleAI Navigator

## Requirement-to-Data Mapping (Step A1)

| Requirement ID | Needed information / feature | Candidate source | Why usable / constraint |
|---|---|---|---|
| FR1: answer questions from the supported documents | Full extractable text of the official guideline documents | MOSTI National Guidelines on AI Governance & Ethics (PDF); ASEAN Guide on AI Governance and Ethics (PDF) | Official, public, authoritative. Constraint: PDF layout (headings, tables, hard-wrapped lines) may affect extraction. |
| FR2 / RAI1: source reference for every answer | Document identity, version and (ideally) page number attached to each text chunk | Same PDFs, plus metadata (filename, SHA-256 checksum) | Basic splitter does not preserve page numbers, so page-level provenance is a known limitation to improve later. |
| NFR4: update documents without rebuilding unrelated parts | Reproducible re-run and a way to detect a changed source | Same PDFs plus checksum in the lineage manifest | A changed checksum signals that a source document was updated. |

## Data Inventory (Step A4)

| Source ID | Filename / URL | Type and purpose | Version / date / owner | Access / rights | Inspection evidence |
|---|---|---|---|---|---|
| S01 | NATIONAL-GUIDELINES-OF-AIGE-20241118.pdf; https://www.mosti.gov.my/wp-content/uploads/2024/09/NATIONAL-GUIDELINES-OF-AIGE-20241118.pdf | Unstructured text (PDF); primary knowledge source for FR1, FR2; the Week 3 pipeline source | [version/date from cover]; owner: MOSTI; downloaded [date] | Publicly available; redistribution terms [checked / not checked]; raw PDF not committed to GitHub | 138 pages; 256,361 characters; 2 pages with no text (pages [numbers]); size 9,772,377 bytes. In sampled pages (1 and 70) text is readable. Observed: lines are hard-wrapped mid-sentence. |
| S02 | ASEAN-Guide-on-AI-Governance-and-Ethics_beautified_201223_v2.pdf; https://asean.org/wp-content/uploads/2024/02/ASEAN-Guide-on-AI-Governance-and-Ethics_beautified_201223_v2.pdf | Unstructured text (PDF); second knowledge source for FR1, FR3; inspected only this week | [version/date from cover]; owner: ASEAN Secretariat; downloaded [date] | Publicly available; redistribution terms [checked / not checked]; raw PDF not committed to GitHub | 87 pages; 191,311 characters; 0 pages with no text; size 4,233,765 bytes. In sampled pages (1 and 44) text is readable, including a case-study box. Observed: "AI" sometimes extracted as "Al" ([n] occurrences). |

Not yet inventoried (planned for a later iteration): UNESCO Recommendation on the Ethics of AI (S03).
Note: only S01 is processed by the Week 3 pipeline; S02 is inspected as the second source.
