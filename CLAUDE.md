# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a reusable **skill** for reproducing research papers in Python. It defines a workflow that prioritizes local TeX sources over PDF extraction and enforces modular code design with bilingual documentation.

**Compatible with:** Codex, Claude Code, OpenClaw

## Core Workflow (SKILL.md)

1. **Intake and scope** - Confirm input artifacts (TeX paths, PDF, target repo)
2. **Source extraction** - TeX-first path preferred; PDF fallback only when TeX is incomplete
3. **Extraction quality checks** - Validate completeness before reproduction
4. **Reproduction planning** - Build plan from extracted source materials, not memory
5. **Python implementation** - Modular design, low coupling, high cohesion
6. **README requirements** - Paper metadata header, bilingual docs, embedded figures

## Key Principles from SKILL.md

- **Source priority:** Read local TeX (`.tex`, `.bib`, styles, figures) first; use PDF extraction only as fallback
- **No summarization:** Preserve original scientific wording verbatim
- **Modular code:** Keep files under ~200 lines; split responsibilities into separate modules
- **Bilingual docs:** Maintain both `README.md` (English) and `README_zh-CN.md` (Chinese)
- **Figure granularity:** One chart per image file; only combine for multi-panel comparisons

## README Header Format

Every reproduction project README must start with paper metadata:

```markdown
# [Paper Title]

**Authors:** Author Name¹, Co-Author Name²
**Affiliations:**
¹ Department, University, Country (email@university.edu)
² Lab, Institution, Country (email@institution.edu)

## Abstract

[Verbatim abstract text from the paper]
```

## File Structure

```text
paper-repro-python/
  SKILL.md          # Main behavior specification
  README.md         # English documentation
  README_zh-CN.md   # Chinese documentation
  agents/
    codex.yaml      # Codex agent configuration
```

## Notes

- `SKILL.md` is the authoritative source for workflow behavior
- `agents/codex.yaml` metadata must stay aligned with `SKILL.md`
- If TeX and PDF disagree, document the discrepancy and prefer the more complete source
