---
contributor: Mike
team: Not Skynet
type: command
name: Sample Command
filename: Sample MD
submitted: 2026-06-29
---

# Sample Command — Sample MD

**Contributor:** Mike | **Team:** Not Skynet
**Type:** command

## Description

Brief description

## File Contents

```
---
description: Changelog — turn source material (PR links/numbers, a commit range, a diff, a branch/PR list, or a release-notes draft) into a self-contained HTML changelog, drafted then graded against a quality rubric (never auto-publishes)
argument-hint: "[topic label + source: PR link(s)/#, commit range, repo, or pasted text]"
---
Turn source material into a **changelog** as a single self-contained HTML report, then **grade it against a rubric** in a separate pass. Reusable across any project — driven entirely by the inputs you point it at, not hardcoded to any repo or product.

## 1. Resolve inputs (ask only for what's missing)
- **`$ARGUMENTS` may contain a topic label and/or a source** — e.g. `/changelog acme-web https://github.com/org/repo/pull/8`, a PR number, a commit range (`v1.2..main`), a repo, or pasted notes/diff summary.
- **Source material:** a PR link or number, a commit range, a repo + branches, a release-notes draft, a copied diff summary, or pasted text. If nothing is given, **ask** — do not invent changes.
- **Grounding (optional, read-only):** if a GitHub PR/repo is referenced and `gh` is available, you MAY fetch metadata to ground entries — `gh pr view <n>`, `gh pr diff <n> --name-only`, `gh api repos/<o>/<r>/branches`, `gh pr list`. Mark each entry's evidence basis: **diff reviewed** vs **title only**. Do not fetch auth-gated content beyond what `gh` returns; never push or comment.
- **Topic label:** from `$ARGUMENTS`, or derive from the repo/source.

## 2. Draft the changelog (do this first — no rubric yet)
Group changes into these sections, in order:
1. **User-facing changes** — what end users will notice.
2. **Internal / operational changes** — admin/ops/infra/dev-only.
3. **Fixes** — bug fixes (say "none" honestly if there are none).
4. **Known risks & follow-up** — unresolved work, caveats, things to verify.

Separate **shipped/merged** from **proposed/open** changes — never blend them.

## 3. Author to this rubric (the changelog must pass all six)
1. Every item links to a PR, issue, commit, or source note.
2. User-facing changes are separated from internal-only changes.
3. Each item states **who is affected** (which users/roles; "no users" if none).
4. Impact claims are supported by evidence **or removed** — tag each item's evidence basis (diff-reviewed vs title-only); don't assert beyond the source.
5. Follow-up work is clearly labeled and **not presented as shipped** — distinguish merged/shipped from open/proposed.
6. The output is scannable by someone who didn't work on the change (clear sections, consistent per-item pattern, status/audience/evidence tags).

## 4. Grade in a separate pass
After drafting, grade the changelog check-by-check against the six rules. Return a short table of PASS/FAIL per check, and for any failure (or soft spot), state the fix — and apply it. Be honest: surface title-only entries, unconfirmed audiences, and unshipped-as-shipped risks rather than rubber-stamping.

## 5. Output: self-contained HTML
Write ONE `.html` file: all CSS inline in a `<style>` block, no external assets, no JS required. Scannable layout — section headers, one card/row per item, and small tags for **status** (shipped/proposed), **audience** (who's affected), and **evidence** (diff-reviewed/title-only). Include the rubric-grading table at the end. One accent color (`#5B2A86`), system font stack, print-friendly.
- Save to `changelogs/changelog-<topic-slug>-<YYYY-MM-DD>.html` relative to the cwd (create `changelogs/` if missing). Slugify the topic.
- Print the **absolute path**. Offer a browser preview; do not open or share without being asked.

## Guardrails (hard rules)
- **Never** post, send, comment, commit, push, or publish the changelog or its contents.
- Only file write permitted is the single HTML changelog (and `changelogs/` if it must be created). Do not edit source code.
- If the source is thin, say so in **Known risks & follow-up** rather than inventing changes or impact.
- Never present open/unmerged work as shipped.

```

## Notes

Nothing special
