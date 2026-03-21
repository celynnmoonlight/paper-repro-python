# Changelog

All notable changes to this project will be documented in this file.

## [1.0.1] - 2026-03-21

### Changed

- **Extended source priority workflow**: Added support for user-preprocessed documents as secondary source before PDF fallback
  - Source priority is now: TeX sources → user-preprocessed documents (`.md`, `.json`, images) → PDF extraction
  - Users can provide their own extracted content (e.g., from prior PDF parsing) and the skill will read it before falling back to raw PDF

### Added

- **Logging and data persistence**: New requirements for saving execution logs and output data
  - Logs must be saved to timestamped files in `logs/` directory
  - Output data must be saved to `outputs/` or `results/` directory in structured formats (JSON, CSV, etc.)
  - Configuration snapshots must be saved alongside outputs for reproducibility

- **Result verification workflow**: Mandatory comparison of reproduction results against paper-reported metrics
  - Extract quantitative metrics from paper source
  - Compute same metrics from reproduction outputs
  - Document both values side by side
  - Investigate and fix discrepancies when results deviate significantly
  - Define acceptable tolerance based on paper domain

### Updated

- `SKILL.md`: Added sections 6 (Logging and data persistence) and 7 (Result verification and comparison); renumbered subsequent sections
- `README.md` and `README_zh-CN.md`: Updated feature descriptions to include logging and verification requirements

## [1.0.0] - 2026-03-11

### Added

- Initialize Paper Repro Python skill project with core files:
  - `.gitignore` for development environment files
  - MIT License
  - Bilingual README files (`README.md`, `README_zh-CN.md`)
  - Codex agent configuration (`agents/codex.yaml`)
  - Skill behavior specification (`SKILL.md`)

### Features

- **TeX-first workflow**: Prioritize local TeX sources (`.tex`, `.bib`, styles, figures) over PDF extraction
- **PDF fallback**: Full-fidelity PDF-to-Markdown extraction when TeX is unavailable
- **Figure granularity**: One chart per image file by default; multi-panel only for comparisons
- **Multi-platform compatibility**: Support for Codex, Claude Code, and OpenClaw
- **Bilingual documentation**: Automatic maintenance of English and Chinese README files
- **Implicit skill invocation**: Added `allow_implicit_invocation` policy for Codex

### Documentation

- Update GitHub repository URLs from placeholder to actual repository address
- Add installation instructions for Claude Code and OpenClaw
- Add platform compatibility notice in README header
- Fix formatting and line ending issues in README and SKILL.md

### Renamed

- Rename `agents/openai.yaml` to `agents/codex.yaml` for Claude Code compatibility
