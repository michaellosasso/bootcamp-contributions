---
contributor: Hiren Bhavsar
team: Other
type: skill
name: prd-eval
filename: CHANGELOG.md
submitted: 2026-07-02
---

# prd-eval — CHANGELOG.md

**Contributor:** Hiren Bhavsar | **Team:** Other
**Type:** skill

## Description

Scores any PRD (Confluence link or pasted/local markdown) across 5 dimensions (Goal Quality, KPI Definition, Metrics Spec, Telemetry, Reporting) 0–25 total, auto-generates missing sections. Classifies each PRD on three independent axes — AI-Native (yes/no), Mobile-First (yes/no, stackable with AI-Native), and Audience (Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid) — so internal care-team tools and member/client-facing tools get held to the evidence bar that actually matters for their users.

## File Contents

```
# prd-eval Changelog

## 1.0.0 — 2026-07-02

Initial build. Design decisions:
- AI-Native and Mobile-First are independent, stackable flags — a PRD can be neither, either, or
  both — rather than a single either/or TYPE A/B pick.
- Added an Audience axis (Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid)
  as a 3rd, always-required classification, so internal-tool PRDs and member/client-facing PRDs
  are held to the evidence bar that actually matters for their users.
- Mobile-First's extra bar is member accessibility & health literacy (plain-language content,
  WCAG/accessibility, low-bandwidth/older-device support) — not app-store mechanics.
- Sub-files and child Confluence pages are never auto-fetched; the skill always asks the user to
  name them explicitly, to avoid silently mis-scoping a multi-document PRD.
- Confluence cloud ID is left as a Configuration placeholder in SKILL.md, not hardcoded.
- Source spec: `cc_build_prd_eval_skill.md` (originally framed as a v2.0 update to a prior TYPE
  A/B skill that doesn't exist in this skills folder — renumbered to 1.0.0 as this is a new skill
  here).

```

## Notes

Uses new Anthropic skills format including a changelog and versioning, and reference files.  
