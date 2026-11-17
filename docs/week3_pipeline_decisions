# Week 3 Pipeline Decisions — ResponsibleAI Navigator

Diagram: `docs/week3_pipeline_diagram.png`
Notebook: `notebooks/week3_pipeline.ipynb`

## 1. Requirements supported
- FR1: answer questions from the supported documents (needs the document text in usable form)
- FR2 / RAI1: source reference for every answer (needs source identity attached to each chunk)
- NFR4: update documents without rebuilding unrelated parts (needs a repeatable run and change detection)

## 2. Selected source
S01: MOSTI National Guidelines on AI Governance & Ethics (PDF, 138 pages, filename date 20241118). S02 (ASEAN Guide) was inspected but not processed; S03 (UNESCO) is planned for a later iteration. Details are in `docs/week3_data_inventory.md`.

## 3. Part B comparison and evidence

| Approach A: fixed-500 | Approach B: paragraph-aware-500 | Observed evidence | Selected approach and trade-off |
|---|---|---|---|
| 513 chunks, average 500 characters | 515 chunks, average 498 characters | Both start mid-sentence in 85% of chunks and end without punctuation in 98% (A) and 99% (B). The cleaned text has only 5 blank-line breaks against 4,999 single newlines, so paragraph-aware splitting has almost no paragraph boundaries and falls back to fixed cutting. | Selected fixed-500: same measured result as paragraph-aware with simpler logic, supporting FR1. Accepted limitation: chunks often cut mid-sentence and carry no page number. |

## 4. Chosen preparation configuration
- Extraction: PDF text extraction (pypdf), 138 pages, 256,501 characters extracted (256,438 after cleaning)
- Cleaning: collapse repeated spaces and tabs; trim ends
- Chunking: fixed 500-character chunks, no overlap
- Output: 513 records with fields `id`, `source`, `text`, `page` (page = null)

## 5. Accepted limitation
- Chunks often cut mid-word or mid-sentence (85% start mid-sentence in Part B).
- Page numbers are not tracked (`page` is null), which weakens FR2 and RAI1 because answers cannot yet cite a page.
- Page furniture is embedded in the text. In inspected record 50, a stray page number ("10") and an image credit appear inside the chunk text.
- Planned improvement (later iteration): sentence-aware, page-tracked chunking with overlap, then evaluate retrieval quality.

## 6. Representative record inspection
Record 50 of 513 is readable but begins mid-word and contains page furniture, which confirms the Part B finding. The record count (513) matches Part B.

## 7. Differences from Part B
- Part B records contain `record_id` and `source_sha256` per record.
- Part C records contain `id` and the full source path; checksums are held in `pipeline_manifest.json` instead of in each record.
- The method, configuration and record count (513) are identical.
- Both manifests exist: `data/week3_manifest.json` (Part B) and `data/pipeline_v1/documents/pipeline_manifest.json` (Part C).

## 8. ETL / ELT decision
ETL. Text is extracted from the PDF and transformed (cleaned and chunked) before being loaded as JSONL, because the chunk format is needed before any later step can use the data. ELT was not chosen because there is no database or warehouse to transform inside, and the raw PDF is kept unchanged in `data/raw/`.

## 9. Batch vs streaming rationale
Batch. The guideline documents are static files that change rarely, so the pipeline runs on demand. When a document is updated, a changed SHA-256 checksum signals that the pipeline should be rerun (supports NFR4). Streaming is not justified because there is no continuous data source.

## 10. Output location
- Part B output: `data/processed/prepared_text.jsonl`
- Part C output: `data/pipeline_v1/documents/prepared_text.jsonl`
- Manifests: `data/week3_manifest.json` and `data/pipeline_v1/documents/pipeline_manifest.json`
- Notebook: `notebooks/week3_pipeline.ipynb`

## 11. Provenance and access caveat
The source PDF states "all rights reserved" and no reproduction without permission. The raw PDF and prepared text chunks are therefore not committed to GitHub; only manifests (hashes and metadata), the notebook, the inventory, the diagram and this file are shared. The manifests carry the lab's default values "Not verified" for source version and access rights; the checked rights information is recorded in `docs/week3_data_inventory.md`. The checksum validation confirms that files match their recorded hashes, not that the data is legally shareable or of sufficient quality.

## 12. Stage contracts

| Stage | Contract / evidence | Failure response |
|---|---|---|
| Ingest | Chosen source file exists in `data/raw/` and its use is documented in the inventory | Stop for missing input |
| Inspect | PDF is readable and yields extractable text (138 pages; 2 pages without text) | Stop if no text can be extracted; flag for OCR |
| Prepare | Fixed 500-character method produces 513 chunks | Stop and report transformation failure |
| Validate | Output exists, is non-empty, with SHA-256 fingerprints | Stop for missing or empty output |
| Record lineage | Source linked to exact output in both manifests; rerun gives identical fingerprints | Stop and report missing mapping or checksum mismatch |

## 13. Traceability

| Requirement | Pipeline element | Evidence |
|---|---|---|
| FR1 | Extraction and chunking of S01 | 513 readable chunks; record 50 inspected |
| FR2 / RAI1 | Source identity and checksum in manifests | Manifest links S01 to output; page numbers missing (limitation) |
| NFR4 | Checksum-based change detection and repeatable run | Cell 9 repeatability check: PASS |
