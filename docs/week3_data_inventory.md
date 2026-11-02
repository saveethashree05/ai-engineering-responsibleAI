## Requirement-to-Data Mapping (Step A1)

| Requirement ID | Needed information / feature | Candidate source | Why usable / constraint |
|---|---|---|---|
| FR1: answer questions from the supported documents | Full extractable text of the official guideline documents | MOSTI National Guidelines on AI Governance & Ethics (PDF); ASEAN Guide on AI Governance and Ethics (PDF) | Official, public, authoritative. Constraint: PDF layout (headings, tables) may affect extraction. |
| FR2 / RAI1: source reference for every answer | Document identity, version and (ideally) page number attached to each text chunk | Same PDFs, plus metadata (filename, SHA-256 checksum) | Basic splitter does not preserve page numbers, so page-level provenance is a known limitation to improve later. |
| NFR4: update documents without rebuilding unrelated parts | Reproducible re-run and a way to detect a changed source | Same PDFs plus checksum in lineage manifest | A changed checksum signals that the source document was updated. |
