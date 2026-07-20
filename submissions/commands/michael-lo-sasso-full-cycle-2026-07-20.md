---
contributor: Michael Lo Sasso
team: Not Skynet
type: command
name: Full Cycle
filename: full-cycle.md
submitted: 2026-07-20
---

# Full Cycle — full-cycle.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** command

## Description

Full 11-step zip processing cycle — thorough analysis, contract check, docs update

## File Contents

```
---
description: Full 11-step zip processing cycle — thorough analysis, contract check, docs, Confluence sync
argument-hint: "[setupXXX zip folder name, optional]"
---
Run the FULL canonical cycle from `memory/rsync-workflow.md` — all 11 steps, no shortcuts, **full thoroughness**. The user explicitly values thoroughness here: read changed files properly, do NOT spot-check or work from `--stat` alone for the analysis step.

1. Extract the zip ($ARGUMENTS if given; otherwise ask which `setupXXX`).
2. Rsync (canonical command).
3. Safety restore: `git checkout -- .github/ .gitignore docs/ scripts/ CLAUDE.md`
4. `git status` + `git diff --stat`.
5. **Contract Check** (full procedure) → flagged summary.
6. **Analyze changes thoroughly** — read the changed files, understand what Make built, note surprises, and check against the build prompts' Verification lists.
7. Update memory (`recent-builds.md`, `MEMORY.md`: pending → shipped + version label; relevant feature memory).
8. Update affected OneDrive docs (verify against code first — no assumptions). **Also sweep the version/status/roadmap blocks, not just feature prose**: "Current release/baseline" headers, Shipped/Recently Shipped tables, Planned / Feature Status / Build Sequence tables, and "as of vXX" / `setupXXX` / count claims — move shipped items out of Planned and bump version stamps (see `/doc-sync` step 2).
9. Commit code — staging-integrity guard; confirm message and main-vs-branch + push per my global rule.
10. Push.
11. Doc sync (`sed`/`cp` → `docs/`, commit, push → auto Confluence sync). Never skip.

The phrases **"full synch"** and **"typical cycle"** mean this same full cycle.

```

