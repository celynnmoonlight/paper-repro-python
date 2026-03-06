# Paper Repro Python Skill

A reusable Codex skill for reproducing research papers in Python with a strict workflow: full-fidelity PDF-to-Markdown extraction first, paper-specific implementation second, and bilingual project documentation third.

## What This Skill Does

- Extract full paper content from PDF into Markdown without summarization, paraphrasing, or rewriting.
- Preserve paper structure: sections, equations, theorem blocks, tables, captions, references, and appendices.
- Plan and implement reproduction in Python based on extracted content, not memory.
- Enforce modular engineering principles: low coupling, high cohesion, clear boundaries.
- Generate and maintain both `README.md` (English) and `README_zh-CN.md` (Chinese).
- Require generated images/figures to be embedded in both README files.

## Typical Trigger

Use this skill when your request includes one or more of these goals:

- Read a paper PDF and extract complete content to Markdown.
- Reproduce the paper in Python.
- Update project docs with bilingual README files and experiment figures.

Example prompt:

```text
Use $paper-repro-python. Extract this paper PDF to full Markdown first (no summarization), then reproduce in Python, and update README.md + README_zh-CN.md with generated figures.
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
https://github.com/celynnmoonlight/codex-skill-paper-repro-python/tree/main
```

If the skill is in a subfolder:

```text
Use $skill-installer and install from:
https://github.com/celynnmoonlight/codex-skill-paper-repro-python/tree/main/skills/paper-repro-python
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
- If extraction quality is limited by scanned PDFs/OCR, mark uncertain text explicitly.
