---
description: Launch the 简历优化助手 — AI-powered resume optimization with 7-dimension
  diagnosis, interactive Gap Q&A, and Word comment annotations. Supports 校招/社招 modes
  with Evidence Mining & Reframing.
argument-hint: [resume_path] [--mode 校招|社招] [--strategy SAFE|BOOSTED]
allowed-tools: [Read, Bash, Glob, WebFetch]
---

# CV Expert — /cv-expert

This command launches the 简历优化助手 skill. It will guide you through 8 phases:

- **Phase 0: Intake** — Collect target job info, JD, and resume path
- **Phase 1: Validate** — Validate all inputs
- **Phase 2: Parse** — Parse your resume into structured format
- **Phase 3: Diagnose** — 7-dimension diagnostic report with JD-to-Evidence mapping
- **Phase 4: Gap Q&A** — Interactive Q&A to fill information gaps
- **Phase 5: Patches** — Generate optimization patches
- **Phase 6: Write** — Produce optimized .docx with Word comments
- **Phase 7: Deliver** — Final report + interview follow-up predictions

Arguments provided: $ARGUMENTS

If a file path argument was provided, treat it as the resume .docx path in Phase 0 Step C (skip asking for it, but still confirm).
If `--mode` was specified, use it as the mode selection in Phase 0 Step A.
If `--strategy` was specified, use it as the output strategy in Phase 0 (skip asking).

**Start the cv-expert skill now. Begin with Phase 0: Structured Intake.**
