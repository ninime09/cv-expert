# CV Expert — AI Resume Optimization Assistant  
# CV Expert — AI 简历优化助手

CV Expert is a local-first Claude Code plugin that provides structured, explainable, and JD-specific AI resume optimization.

CV Expert 是一个本地优先（local-first）的 Claude Code 插件，用于提供结构化、可解释、基于 JD 定制的 AI 简历优化能力。

---

## ✨ Features | 功能特性

- 7-dimension diagnostic report (JD-specific, not generic)  
  7 维度结构化诊断（基于目标 JD，而非泛化分析）

- Interactive Gap Q&A to fill missing information  
  交互式 Gap 问答机制，补充关键信息缺口

- Optimized `.docx` output with Word comment annotations  
  输出优化后的 `.docx` 文件，并为每一处修改添加 Word 评论说明

- SAFE / BOOSTED strategy for campus hiring  
  校招 SAFE / BOOSTED 双输出策略

- Support for campus & experienced hiring modes  
  支持校招与社招模式

- Privacy-first: fully local processing  
  隐私优先：所有处理均在本地完成，不上传文件

---

## 🚀 Quick Start | 快速开始

### Requirements | 环境要求

- Claude Code CLI (`claude`) or Claude Code VSCode extension  
- Python 3.8+  
- macOS or Linux  

---

### Step 1: Install Plugin | 安装插件

```bash
/plugin install /absolute/path/to/cv-expert
```

Or add the `cv-expert` directory to your Claude Code plugin folder.  
或将 `cv-expert` 文件夹添加至 Claude Code 插件目录。

---

### Step 2: Install Python Dependencies | 安装依赖

```bash
bash ${CLAUDE_PLUGIN_ROOT}/skills/cv-expert/scripts/setup.sh
```

Or manually:

```bash
pip install "python-docx>=1.2.0"
```

---

### Step 3: Run | 运行插件

```bash
/cv-expert
```

Claude will guide you through the full 8-phase workflow.  
Claude 将引导你完成完整的 8 阶段优化流程。

---

## 📌 Usage | 使用方式

### Basic Invocation | 基础调用

```bash
/cv-expert
```

Claude will ask for:

1. Target role, company, and hiring mode (campus / experienced)  
2. JD text (paste / local `.txt` path / URL)  
3. Resume `.docx` file path  

Claude 将依次询问：

1. 目标岗位 / 公司 / 招聘模式（校招 / 社招）
2. JD 文本（粘贴 / 本地 `.txt` 路径 / URL）
3. 简历 `.docx` 文件路径

---

### With Arguments | 带参数调用

```bash
/cv-expert /path/to/resume.docx --mode 校招 --strategy BOOSTED
```

- `--mode 校招|社招` — Skip mode selection  
- `--strategy SAFE|BOOSTED` — Skip strategy selection (campus only)

---

## 📥 Input & 📤 Output | 输入与输出

### Inputs | 输入
| Input | Method |
|-------|--------|
| Job Description | Paste text / local .txt path / URL |
| Resume | .docx file path (PDF not supported in V1) |
| Target job info | Answered interactively in Phase 0 |

### Outputs | 输出
| Output | Location |
|--------|----------|
| Optimized resume | `<original_dir>/<name>_optimized_safe.docx` or `_optimized_boosted.docx` |
| Backup (original unchanged) | `<original_dir>/<name>_backup.docx` |
| Diagnostic report | Printed in Claude conversation (Markdown) |
| Interview follow-up predictions | Printed in conversation (6-10 questions, 3 groups) |

If the original directory is not writable, output falls back to `~/Downloads/` then `/tmp/`.
若目录不可写，将自动 fallback 至 `~/Downloads/` 或 `/tmp/`。

---

## 🔄 The 8 Phases | 八阶段流程

| Phase | Name | What Happens |
|-------|------|-------------|
| 0 | Intake | Collect target job info → JD → resume path |
| 1 | Validate | Check file exists (.docx only), JD length ≥ 80 chars, role/company non-empty |
| 2 | Parse | Extract resume structure (sections, bullets, ATS flags) into JSON |
| 3 | Diagnose | 7-dimension diagnosis + JD-to-Evidence mapping table |
| 4 | Gap Q&A | Interactive questions to fill data gaps; BOOSTED mode confirmation per Estimate |
| 5 | Patches | Generate patches.json (replace_text + comment_only) |
| 6 | Write | Apply patches to docx, add Word comments, create backup |
| 7 | Deliver | Show full report, file paths, interview follow-up predictions |

---

## 📊 7 Diagnostic Dimensions | 七大诊断维度

| # | Dimension | 校招 Weight | 社招 Weight | Notes |
|---|-----------|------------|------------|-------|
| 1 | Eligibility & Risk Signals | 10% | 15% | **Never blocks flow** — risk notes only |
| 2 | Keyword + Evidence | 25% | 20% | Coverage % + evidence mapping |
| 3 | Impact & Quantification | 20% | 25% | Fact/Estimate/Need-confirm labeling |
| 4 | Competency Map | 20% | 15% | JD skill chain coverage |
| 5 | Story & Structure | 15% | 10% | Timeline, narrative flow |
| 6 | Language & Trust | 5% | 10% | Action verbs, fluff detection |
| 7 | ATS & Formatting | 5% | 5% | Tables, textboxes (best-effort), dates |

Each dimension uses different weights for campus vs experienced hiring.  
校招与社招模式采用不同权重体系。

---

## 🎯 Output Strategy (Campus Mode) | 校招输出策略

### SAFE (Default)

Only confirmed facts appear in the resume body.  
Estimates remain in Word comments.

仅将已确认事实写入正文，估算数据仅出现在评论中。

---

### BOOSTED

After confirmation, reasonable estimates may appear in the body (with ⚠️ label).

确认后，合理估算可写入正文（带 ⚠️ 标记）。


File naming:
- `_optimized_safe.docx` — SAFE mode output
- `_optimized_boosted.docx` — BOOSTED mode output

---

## 🏷 Quantification Labels | 数据标注说明

Every change in the optimized resume is labeled:
优化后简历中的每一个改动都会被标注：

| Label | Meaning | In Body? |
|-------|---------|---------|
| ✅ Fact | You confirmed the number | Yes (both modes) |
| ⚠️ Estimate | Reasonable inference, basis explained | SAFE: comment only / BOOSTED: body after confirmation |
| ❓ Need confirm | Insufficient info | Comment only, never in body |

---

## 🔒 Privacy | 隐私说明

🔒 All processing happens locally on your machine.
- Your resume is parsed locally using `python-docx`
- JD text is analyzed by Claude within your session
- No files are uploaded to external servers
- The plugin does not save or log your resume content

所有处理均在本地完成，不上传、不保存、不记录用户简历内容。
---

## Python Scripts Reference

All scripts output JSON to stdout and accept `--help` for usage.

```bash
# Validate inputs
python3 scripts/validate_input.py \
  --file "/path/resume.docx" \
  --jd-text "..." \
  --target-role "Analyst" \
  --target-company "Amazon"

# Parse resume
python3 scripts/parse_resume.py \
  --input "/path/resume.docx" \
  --output "/tmp/parsed.json"

# Apply patches
python3 scripts/write_resume.py \
  --input "/path/resume.docx" \
  --patches "/tmp/patches.json" \
  --output "/path/resume_optimized_safe.docx" \
  --backup "/path/resume_backup.docx"
```

---

## 📁 Project Structure | 项目结构

```
cv-expert/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   └── cv-expert.md                ← /cv-expert slash command
├── skills/
│   └── cv-expert/
│       ├── SKILL.md                ← Main 8-phase orchestration
│       ├── references/
│       │   ├── diagnostic-rubric.md
│       │   ├── jd-parsing.md
│       │   ├── patch-schema.md
│       │   └── 校招-templates.md
│       ├── scripts/
│       │   ├── setup.sh
│       │   ├── text_utils.py       ← Shared normalize_text()
│       │   ├── validate_input.py
│       │   ├── parse_resume.py
│       │   └── write_resume.py
│       └── examples/
│           ├── mock_jd_校招.txt
│           ├── mock_jd_社招.txt
│           ├── test_校招_cs_intern.md
│           ├── test_社招_missing_kpi.md
│           └── test_error_handling.md
└── README.md
```

---

## 🛠 Troubleshooting | 常见问题

| Error | Cause | Fix |
|-------|-------|-----|
| `python-docx not installed` | setup.sh not run | `bash setup.sh` |
| `File not found` | Wrong path | Use absolute path |
| `PDF not supported` | Wrong format | Open in Word → Save As .docx |
| `.doc not supported` | Legacy format | Open in Word → Save As .docx |
| `JD too short` | Incomplete JD | Paste the full JD text |
| Patches failing | para_id mismatch | Re-parse the document if it was edited after parsing |
| Comments not visible | Old Word version | Update to Word 2016+ or open in Word for Mac |

---

## Development Notes 开发笔记

### Adding V2 Features (append_run patch type)

The `write_resume.py` framework is designed to accept additional patch types. To add `append_run`:

1. Add `apply_append_run()` function in `write_resume.py`
2. Update `apply_patches()` dispatcher
3. Update `patch-schema.md` with the new type's schema
4. Increment patch_version to "1.2"

### Replacing the docx comment API

If your `python-docx` version doesn't support `doc.add_comment()`, the script falls back to manual XML insertion. To verify:

```python
python3 -c "from docx import Document; d = Document(); print(hasattr(d, 'add_comment'))"
```

If `False`, the XML fallback in `write_resume.py` will be used automatically.
