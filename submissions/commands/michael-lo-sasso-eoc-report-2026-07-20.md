---
contributor: Michael Lo Sasso
team: Not Skynet
type: command
name: eoc-report
filename: eoc-report.md
submitted: 2026-07-20
---

# eoc-report — eoc-report.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** command

## Description

Turns a cycle's commits/diff/build notes into one self-contained HTML report 

## File Contents

```
---
description: End-of-cycle release notes — turn a cycle's commits/diff/build notes into one self-contained HTML report (never auto-publishes)
argument-hint: "[version label, e.g. v43 / setupXXX — optional]"
---
Produce an **end-of-cycle (EOC) release-notes report** as a single self-contained HTML file. This is a read-only reporting path: it analyzes and writes ONE local HTML file. It does NOT commit, push, sync, or publish anything.

## 1. Resolve inputs (ask only for what's missing)
- **Version label:** `$ARGUMENTS` if given (e.g. `v43 / setupHOMECTA`). Otherwise ask which cycle/version this report closes.
- **Source material**, in order of preference — use what's available, ask if none is provided:
  1. A commit range or `git log`/`git diff` in `/Users/michael.losasso/Projects/clickable-demo-framework/` (e.g. since the prior version's tip).
  2. A changelog / notes / file path the user points to.
  3. `memory/recent-builds.md` plus the active feature-memory file for the cycle.
- If you cannot find grounded source material, **ask for the file path or commit range** — do not invent a cycle.

## 2. Extract facts, drop unsupported claims
- Every **Key finding** must trace to a concrete source: a commit hash, a changed file/path, a Figma frame node, or a specific notes line. Cite it.
- If something is plausible but not grounded in the source, **do not assert it** — move it to **Open questions** instead.
- Prefer what *shipped* (features, fixes, refactors, removals) over intent. Note removals/deprecations explicitly.

## 3. Build the report
Write ONE self-contained `.html` file (all CSS inline in a `<style>` block, no external assets, no CDN links, no JS required). Sections in this order:
1. **Header** — version label, report date, and the source range/inputs used (commit range, file paths, frames).
2. **Executive summary** — 2–4 sentences a stakeholder can scan: what this cycle delivered and why it matters.
3. **Key findings (what shipped)** — grouped cards or rows (Features / Fixes / Refactors / Removals). Each item carries a short source tag (commit hash or file).
4. **Evidence / source references** — a compact table mapping each claim to its source (commit, file, frame, or notes line).
5. **Open questions** — anything unresolved, ambiguous, or deferred (e.g. pending carry-backs).
6. **Recommended next actions** — concrete follow-ups, ordered by priority.

Use clean, readable styling: system font stack, generous whitespace, one accent color (`#5B2A86` Transcarent-ish purple), subtle card borders, a muted source-tag chip, print-friendly. No heavy frameworks.

## 4. Save & report
- Save to `reports/eoc-<version-slug>-<YYYY-MM-DD>.html` relative to the current working directory (create `reports/` if missing). Slugify the version (e.g. `v43-setupxxx`).
- Print the **absolute path** of the saved file and offer to open it in a browser preview. Do not open or share it without the user asking.

## Guardrails (hard rules)
- **Never** post, send, email, commit, push, or publish the report or its contents.
- **Never** write into `docs/` or trigger the Confluence sync action — this path stays dormant.
- Only file write permitted is the single HTML report (and `reports/` if it must be created).
- If the user later wants it on Confluence, that's a separate explicit step via `/doc-sync` — not this skill.

```

