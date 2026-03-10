# Paper Repro Python Skill

A reusable Codex skill for reproducing research papers in Python with a strict source-priority workflow: read local TeX sources first when available, use full-fidelity PDF-to-Markdown extraction only as fallback, then implement paper-specific code and maintain bilingual project documentation.

## What This Skill Does

- Prioritize local TeX sources (`.tex`, `.bib`, styles, figures) for paper understanding and reproduction.
- Fall back to PDF extraction only when TeX sources are missing or incomplete.
- Preserve original paper content without summarization, paraphrasing, or rewriting scientific statements.
- Plan and implement reproduction in Python based on source materials, not memory.
- Enforce modular engineering principles: low coupling, high cohesion, clear boundaries.
- Encourage module splitting to avoid monolithic files; keep one source file under ~200 lines whenever practical.
- Generate and maintain both `README.md` (English) and `README_zh-CN.md` (Chinese).
- Require README files to start with paper metadata: title, authors (with affiliations and emails), and abstract.
- Require generated images/figures to be embedded in both README files.
- Prefer one chart per image file; only use multi-panel combined figures when comparison across panels is necessary.

## Typical Trigger

Use this skill when your request includes one or more of these goals:

- Reproduce a paper from a local TeX project or a PDF.
- Extract complete paper content to Markdown when PDF fallback is needed.
- Build a cleanly modular Python reproduction project.
- Update project docs with bilingual README files and experiment figures.

Example prompt:

```text
Use $paper-repro-python. If TeX files exist in the folder, read TeX first; otherwise extract this paper PDF to full Markdown (no summarization). Then reproduce in Python with clear modules (avoid monolithic files), and update README.md + README_zh-CN.md with generated figures.
```

## Installation

### Option A: Local install (copy to global Codex skills)

Windows (PowerShell):

```powershell
Copy-Item -Recurse -Force .\paper-repro-python $env:USERPROFILE\.codex\skills\
```

macOS/Linux (bash/zsh):

```bash
mkdir -p "$HOME/.codex/skills"
cp -R ./paper-repro-python "$HOME/.codex/skills/"
```

Then restart the Codex client.

### Option B: Install from GitHub with `$skill-installer`

1. Ensure the repo path points to a folder containing `SKILL.md`.
2. In Codex chat, send one of the following commands.

If the skill is at repo root:

```text
Use $skill-installer and install from:
https://github.com/celynnmoonlight/paper-repro-python/tree/main
```

If the skill is in a subfolder:

```text
Use $skill-installer and install from:
https://github.com/celynnmoonlight/paper-repro-python/tree/main/skills/paper-repro-python
```

If you prefer repo/path form:

```text
Use $skill-installer and install from repo openai/skills path skills/.curated/<skill-name>
```

3. After installation, restart Codex to pick up new skills.

## Directory Layout

```text
paper-repro-python/
  SKILL.md
  README.md
  README_zh-CN.md
  .gitignore
  LICENSE
  agents/
    openai.yaml
```

## Notes

- Keep `SKILL.md` as the source of behavior.
- Keep `agents/openai.yaml` aligned with `SKILL.md` metadata.
- If TeX and PDF disagree, document the discrepancy and prefer the source that is more complete for the targeted claims.
- If extraction quality is limited by scanned PDFs/OCR, mark uncertain text explicitly.