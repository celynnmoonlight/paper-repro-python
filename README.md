# Paper Repro Python Skill

A reusable skill for reproducing research papers in Python with a strict source-priority workflow: read local TeX sources first, then user-preprocessed documents (`.md`, `.json`, images), and use PDF extraction only as last resort, then implement paper-specific code and maintain bilingual project documentation.

**Compatible with:** Codex, Claude Code, OpenClaw

## What This Skill Does

- Prioritize local TeX sources (`.tex`, `.bib`, styles, figures) for paper understanding and reproduction.
- Read user-preprocessed documents (`.md`, `.json`) and images (`.png`, `.jpg`, `.svg`) as secondary source when TeX is unavailable.
- Fall back to PDF extraction only when both TeX and preprocessed documents are missing or incomplete.
- Preserve original paper content without summarization, paraphrasing, or rewriting scientific statements.
- Plan and implement reproduction in Python based on source materials, not memory.
- Enforce modular engineering principles: low coupling, high cohesion, clear boundaries.
- Encourage module splitting to avoid monolithic files; keep one source file under ~200 lines whenever practical.
- Save execution logs and output data for debugging and comparison (logs in `logs/`, data in `outputs/` or `results/`).
- Compare reproduction results against paper-reported metrics and investigate discrepancies.
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
Use $paper-repro-python. If TeX files exist, read TeX first; then check for user-preprocessed documents (.md, .json, images); only fall back to PDF extraction if needed. Then reproduce in Python with clear modules (avoid monolithic files), and update README.md + README_zh-CN.md with generated figures.
```

## Installation

### Codex

#### Option A: Local install (copy to global Codex skills)

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

#### Option B: Install from GitHub with `$skill-installer`

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

### Claude Code

Copy the skill folder to your project's `.claude/skills/` directory:

```bash
mkdir -p .claude/skills
cp -R paper-repro-python .claude/skills/
```

Or install globally:

```bash
mkdir -p "$HOME/.claude/skills"
cp -R paper-repro-python "$HOME/.claude/skills/"
```

### OpenClaw

Copy the skill folder to OpenClaw's skills directory:

```bash
cp -R paper-repro-python ~/.openclaw/skills/
```

Or use OpenClaw's skill installer if available.

## Directory Layout

```text
paper-repro-python/
  SKILL.md
  README.md
  README_zh-CN.md
  .gitignore
  LICENSE
  agents/
    codex.yaml
```

## Notes

- Keep `SKILL.md` as the source of behavior.
- Keep `agents/codex.yaml` aligned with `SKILL.md` metadata.
- If TeX and PDF disagree, document the discrepancy and prefer the source that is more complete for the targeted claims.
- If extraction quality is limited by scanned PDFs/OCR, mark uncertain text explicitly.
