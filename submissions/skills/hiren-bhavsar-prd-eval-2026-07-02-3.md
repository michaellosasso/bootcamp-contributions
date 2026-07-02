---
contributor: Hiren Bhavsar
team: Other
type: skill
name: prd-eval
filename: gotchas.md
submitted: 2026-07-02
---

# prd-eval — gotchas.md

**Contributor:** Hiren Bhavsar | **Team:** Other
**Type:** skill

## Description

Scores any PRD (Confluence link or pasted/local markdown) across 5 dimensions (Goal Quality, KPI Definition, Metrics Spec, Telemetry, Reporting) 0–25 total, auto-generates missing sections. Classifies each PRD on three independent axes — AI-Native (yes/no), Mobile-First (yes/no, stackable with AI-Native), and Audience (Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid) — so internal care-team tools and member/client-facing tools get held to the evidence bar that actually matters for their users.

## File Contents

```
# Gotchas — prd-eval

Add new gotchas here as real evals surface failure modes — don't let this list go stale. This is
how the skill improves over time without re-litigating past mistakes.

- **Score AI-Native and Mobile-First criteria conservatively.** Give credit only for explicitly
  stated agent-framed goals, AWU definitions, human eval processes, or accessibility targets —
  not for intent language like "leverage AI", "intelligent recommendations", or "mobile-friendly".
- **"Your Data Is the Unfair Advantage" requires a named signal.** A specific Databricks table,
  claims field, or behavioral pattern — "member health data" is too generic to earn AI-Native
  credit on the Metrics Specification dimension.
- **Never fabricate `[NEEDS PM INPUT]` values.** If a baseline or target isn't in the PRD, leave
  the placeholder — don't invent a plausible-sounding number.
- **Don't auto-fetch sub-pages, appendices, or child Confluence pages, even if the PRD references
  them.** Always ask the user to name the exact URL or file path. Silently scoping a multi-doc
  PRD down to just the main page produces a misleadingly high or low score.
- **The Confluence cloud ID isn't hardcoded.** Check the Configuration block in SKILL.md first;
  if unset, ask the user once per conversation — don't ask again on every subsequent PRD in the
  same session.
- **A PRD can be both AI-Native and Mobile-First.** Don't force a single either/or pick — check
  both flags independently, and score against every layer that applies.
- **The prototype hypothesis is a written deliverable, not a completed one.** Note in the output
  that it requires an actual working Claude Code / Figma Make prototype before AI-Native
  readiness can be called Green — the written statement alone is necessary but not sufficient.
- **Watch for generic-data placeholder phrases as an active anti-pattern, not neutral filler.**
  "The AI will use member data to make recommendations" isn't a partial-credit statement — it's
  the rubric's literal Metrics Specification red-flag example and should score 1–2, same as if
  nothing were written. Don't let confident-sounding prose read as more complete than it is.
- **Layers only raise the ceiling, they don't lower the floor.** If a PRD's Base score on a
  dimension is already 1 or 2, an unmet AI-Native or Mobile-First layer doesn't subtract further
  — the Base score already captures the gap. See the "How to read the layers" note at the top of
  `scoring-rubric.md`.
- **Audience classification defaults matter.** If a PRD is ambiguous between Internal Care Team
  Tool and Hybrid, default to the single dominant primary user and flag the ambiguity in the
  output rather than silently picking Hybrid (which lowers the bar less than it should).

```

## Notes

Uses new Anthropic skills format including a changelog and versioning, and reference files.  
