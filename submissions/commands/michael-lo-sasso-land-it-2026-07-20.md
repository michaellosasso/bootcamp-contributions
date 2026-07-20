---
contributor: Michael Lo Sasso
team: Not Skynet
type: command
name: Land It
filename: land-it.md
submitted: 2026-07-20
---

# Land It — land-it.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** command

## Description

Land the latest Make zip into the repo and push — cheap, no deep analysis or doc sync

## File Contents

```
---
description: Land the latest Make zip into the repo and push — cheap, no deep analysis or doc sync
argument-hint: "[setupXXX zip folder name, optional]"
---
Run the CHEAP "Land it" path defined in `memory/rsync-workflow.md` (Partial-Cycle Menu): steps 1–5 + 9–10 only. This is the deliberately shallow, low-token path — do NOT do deep behavioral analysis.

1. Locate/extract the latest Make zip ($ARGUMENTS if given; otherwise ask which `setupXXX`) under `/private/tmp/`.
2. Run the canonical rsync (zip → `/Users/michael.losasso/Projects/clickable-demo-framework/`).
3. Safety restore: `git checkout -- .github/ .gitignore docs/ scripts/ CLAUDE.md`
4. `git status` + `git diff --stat` — flag any unexpected files.
5. Run the **Contract Check** (rsync-workflow.md §"Contract Check Procedure") and the **staging-integrity guard**. Produce the short flagged summary.
6. **SKIP** step 6 (deep analysis), step 8 (OneDrive docs), step 11 (doc sync). **Do NOT touch `docs/`** — the Confluence Action must stay dormant.
7. Confirm with me: commit to `main` vs a branch, and confirm the push (per my global branch-first / push-only-when-asked rule). Then stage source files only (respect the staging-integrity guard — list untracked `.tsx`/`.ts` outside `src/imports/` and `src/app/components/ui/` and include genuine new source), commit with a factual message, push.
8. Add a one-line status note to the relevant memory file (e.g. `recent-builds.md` / the active feature memory).

Stop after pushing. No docs, no Confluence, no deep verification unless I separately ask.

```

