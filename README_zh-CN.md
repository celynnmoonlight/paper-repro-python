# Paper Repro Python 技能

这是一个可复用的技能，用于用 Python 复现科研论文，并强制执行”源文件优先”的流程：优先读取本地 TeX 源文件；其次读取用户预处理文档（`.md`、`.json`、图片）；仅在前两者都不可用时，才回退到 PDF 全量提取 Markdown；随后进行论文复现并维护双语项目文档。

**兼容平台：** Codex、Claude Code、OpenClaw

## 这个技能能做什么

- 优先读取本地 TeX 源（`.tex`、`.bib`、样式文件、图片资源）来理解和复现论文。
- 在 TeX 不可用时，读取用户预处理文档（`.md`、`.json`）和图片（`.png`、`.jpg`、`.svg`）作为次要来源。
- 仅在 TeX 和预处理文档都不可用或不完整时，才回退到 PDF 提取。
- 保留论文原始内容，不允许总结、改写或篡改科学表述。
- 基于源材料（而不是记忆）制定并实现 Python 复现实验。
- 强制工程实现遵循低耦合、高内聚、边界清晰。
- 鼓励按职责拆分模块，避免”所有代码写在一起”；单个源码文件尽量控制在约 200 行以内。
- 保存运行日志和输出数据以便调试和对比（日志存于 `logs/`，数据存于 `outputs/` 或 `results/`）。
- 将复现结果与论文报告的指标进行对比，并调查差异原因。
- 生成并维护 `README.md`（英文）和 `README_zh-CN.md`（中文）。
- 要求 README 文件开头必须包含论文元信息：标题、作者（含单位和邮箱）、摘要原文。
- 要求在两个 README 中都插入生成的图片/实验图（Markdown 相对路径）。
- 图片输出粒度默认一图一文件；仅在确实需要多图对比时才使用拼图（多子图合并）。

## 典型触发方式

当你的需求包含以下任一目标时可使用本技能：

- 从本地 TeX 工程或 PDF 复现论文。
- 在需要时将论文 PDF 完整提取为 Markdown。
- 搭建结构清晰、模块化的 Python 复现项目。
- 更新包含双语 README 和实验图片的项目文档。

示例提示词：

```text
使用 $paper-repro-python。如果目录里有 TeX 文件就先读 TeX；其次检查用户预处理文档（.md、.json、图片）；仅在前两者都不可用时才回退到 PDF 提取。然后用 Python 复现，代码按模块拆分（避免大杂烩文件），并更新 README.md 和 README_zh-CN.md，插入生成图片。
```

## 安装方式

### Codex

#### 方式 A：本地安装（复制到全局 Codex skills）

Windows（PowerShell）：

```powershell
Copy-Item -Recurse -Force .\paper-repro-python $env:USERPROFILE\.codex\skills\
```

macOS/Linux（bash/zsh）：

```bash
mkdir -p "$HOME/.codex/skills"
cp -R ./paper-repro-python "$HOME/.codex/skills/"
```

完成后重启 Codex 客户端。

#### 方式 B：通过 `$skill-installer` 从 GitHub 安装

1. 确保你提供的仓库路径对应的目录里包含 `SKILL.md`。
2. 在 Codex 对话中发送以下命令之一。

   如果技能在仓库根目录：

   ```text
   使用 $skill-installer，从这个地址安装：
   https://github.com/celynnmoonlight/paper-repro-python/tree/main
   ```

   如果技能在子目录：

   ```text
   使用 $skill-installer，从这个地址安装：
   https://github.com/celynnmoonlight/paper-repro-python/tree/main/skills/paper-repro-python
   ```

   如果你更习惯 repo/path 形式：

   ```text
   使用 $skill-installer，从 openai/skills 的 skills/.curated/<skill-name> 安装
   ```

3. 安装完成后重启 Codex，加载新技能。

### Claude Code

将技能文件夹复制到项目的 `.claude/skills/` 目录：

```bash
mkdir -p .claude/skills
cp -R paper-repro-python .claude/skills/
```

或全局安装：

```bash
mkdir -p "$HOME/.claude/skills"
cp -R paper-repro-python "$HOME/.claude/skills/"
```

### OpenClaw

将技能文件夹复制到 OpenClaw 的 skills 目录：

```bash
cp -R paper-repro-python ~/.openclaw/skills/
```

或使用 OpenClaw 的技能安装器（如有）。

## 目录结构

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

## 备注

- `SKILL.md` 是行为规范的主文件。
- `agents/codex.yaml` 需要与 `SKILL.md` 的元信息保持一致。
- 如果 TeX 与 PDF 内容存在冲突，需要显式记录差异并说明采用依据。
- 如果 PDF 是扫描版/OCR 质量有限，必须显式标注不确定文本。
