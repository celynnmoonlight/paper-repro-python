# Paper Repro Python 技能

这是一个可复用的 Codex 技能，用于用 Python 复现科研论文，并强制执行以下流程：先完整提取 PDF 到 Markdown，再按论文实现，最后产出双语项目文档。

## 这个技能能做什么

- 将论文 PDF 完整提取为 Markdown，不允许总结、改写或篡改原文。
- 保留论文结构：章节、公式、定理块、表格、图注、参考文献、附录。
- 基于提取结果（而不是记忆）制定并实现 Python 复现实验。
- 强制工程实现遵循低耦合、高内聚、边界清晰。
- 生成并维护 `README.md`（英文）和 `README_zh-CN.md`（中文）。
- 要求在两个 README 中都插入生成的图片/实验图（Markdown 相对路径）。

## 典型触发方式

当你的需求包含以下任一目标时可使用本技能：

- 读取论文 PDF 并完整提取到 Markdown。
- 用 Python 复现论文。
- 更新包含双语 README 和实验图片的项目文档。

示例提示词：

```text
使用 $paper-repro-python。先把这篇论文 PDF 完整提取到 Markdown（不要概括），再用 Python 复现，并更新 README.md 和 README_zh-CN.md，插入生成图片。
```

## 安装方式

### 方式 A：本地安装（复制到全局 Codex skills）

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

### 方式 B：通过 `$skill-installer` 从 GitHub 安装

1. 确保你提供的仓库路径对应的目录里包含 `SKILL.md`。
2. 在 Codex 对话中发送以下命令之一。

如果技能在仓库根目录：

```text
使用 $skill-installer，从这个地址安装：
https://github.com/<owner>/<repo>/tree/main
```

如果技能在子目录：

```text
使用 $skill-installer，从这个地址安装：
https://github.com/<owner>/<repo>/tree/main/skills/paper-repro-python
```

如果你更习惯 repo/path 形式：

```text
使用 $skill-installer，从 openai/skills 的 skills/.curated/<skill-name> 安装
```

3. 安装完成后重启 Codex，加载新技能。

## 目录结构

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

## 备注

- `SKILL.md` 是行为规范的主文件。
- `agents/openai.yaml` 需要与 `SKILL.md` 的元信息保持一致。
- 如果 PDF 是扫描版/OCR 质量有限，必须显式标注不确定文本。
