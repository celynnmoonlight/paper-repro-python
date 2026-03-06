---
name: paper-repro-python
description: "Reproduce research papers in Python from a source PDF with full-fidelity extraction into Markdown before implementation. Use when tasks include reading paper PDFs, extracting complete original content into well-formatted Markdown without summarization or rewriting, implementing paper methods and experiments in Python, and producing bilingual project documentation with clear architecture, low coupling, and high cohesion."
---

Follow this workflow end-to-end unless the user explicitly asks to skip steps.

## 1) Intake and scope

- Confirm input artifacts: PDF path, supplementary files, target repository, and expected outputs.
- State assumptions explicitly when information is missing.
- Keep approach adaptable to the specific paper; do not force a fixed dependency stack or rigid project template.

## 2) PDF to Markdown extraction (full-fidelity)

- Extract paper content page by page into Markdown, preserving the original wording.
- Do not summarize, paraphrase, or rewrite scientific statements.
- Preserve structure faithfully:
  - Title, authors, affiliations, abstract, sections, subsections.
  - Equations (LaTeX-friendly when possible), theorem/lemma/proposition blocks.
  - Tables, figure captions, references, appendices, footnotes.
- If a PDF is scanned or partially unreadable:
  - Run OCR and mark uncertain spans clearly.
  - Never silently invent missing text.
- Include image references/placeholders when figures cannot be represented as plain text.
- Produce one primary output file such as `paper_fulltext.md`.

## 3) Extraction quality checks

- Validate completeness before moving to reproduction:
  - Section/headings coverage matches the PDF.
  - Key equations and algorithm blocks are present.
  - References and appendices are included if present in the PDF.
- Report known extraction limitations and exact affected pages/segments.

## 4) Reproduction planning (paper-specific)

- Build a reproduction plan from the extracted Markdown, not from memory.
- Identify:
  - Problem definition, notation, assumptions, and objective functions.
  - Algorithm steps and required components.
  - Dataset generation/loading, training/optimization, and evaluation protocol.
  - Baselines and ablations required for faithful reproduction.
- If details are missing or ambiguous, call out the gap and provide a conservative implementation choice with rationale.

## 5) Python implementation principles

- Implement with modular design and clear boundaries:
  - Separate concerns (data, models/algorithms, training/solver loop, evaluation, utils, config).
  - Prefer low coupling and high cohesion.
- Keep dependencies minimal and paper-driven; choose tools based on the paper's actual needs.
- Avoid over-engineering early; start from the minimum reproducible core, then extend.
- Add tests/checks for critical math or pipeline steps where feasible.
- Preserve reproducibility:
  - deterministic seeds when applicable,
  - explicit config for key hyperparameters,
  - clear experiment entry points.

## 6) README update requirements (bilingual + images)

- Generate and maintain two README files after code changes:
  - `README.md` (English original)
  - `README_zh-CN.md` (Chinese translation aligned with the English version)
- Ensure both files include:
  - paper citation and target claims to reproduce,
  - environment/setup commands,
  - project structure overview and module responsibilities,
  - how to run main experiments,
  - expected outputs/metrics and where artifacts are saved,
  - known deviations from the paper and why.
- Insert generated figures/images into both README files using valid relative Markdown image paths.
- Keep both README files aligned with actual code paths and commands.
- Keep Chinese content as faithful translation of English technical content (no missing key steps).

## 7) Output contract

- Deliver:
  - extracted full-text Markdown file(s),
  - implemented/updated Python code,
  - `README.md` and `README_zh-CN.md` with embedded generated images.
- Clearly separate:
  - exact extracted content (verbatim from source),
  - your implementation notes and engineering decisions.
