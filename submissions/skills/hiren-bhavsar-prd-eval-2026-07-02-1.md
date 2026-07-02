---
contributor: Hiren Bhavsar
team: Other
type: skill
name: prd-eval
filename: SKILL.md
submitted: 2026-07-02
---

# prd-eval — SKILL.md

**Contributor:** Hiren Bhavsar | **Team:** Other
**Type:** skill

## Description

Scores any PRD (Confluence link or pasted/local markdown) across 5 dimensions (Goal Quality, KPI Definition, Metrics Spec, Telemetry, Reporting) 0–25 total, auto-generates missing sections. Classifies each PRD on three independent axes — AI-Native (yes/no), Mobile-First (yes/no, stackable with AI-Native), and Audience (Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid) — so internal care-team tools and member/client-facing tools get held to the evidence bar that actually matters for their users.

## File Contents

```
---
name: prd-eval
description: "Scores PRD requirements quality across 5 measurement-readiness dimensions (Goal
Quality, KPI Definition, Metrics Specification, Telemetry/Instrumentation, Reporting &
Monitoring), 0-5 each, max 25. Classifies each PRD as AI-Native and/or Mobile-First (stackable
flags) and by Audience (Internal Care Team / Member-Facing / Client-ASO-Facing / Hybrid) so the
right evidence bar applies. Auto-generates missing sections. Accepts a Confluence URL or
pasted/downloaded PRD markdown. Use when the user says 'eval this PRD', 'score this PRD', 'is
this PRD ready for sprint planning', 'grade this requirements doc', 'does this have good
KPIs/telemetry/metrics', or shares a PRD together with a request to check requirements quality."
version: "1.0.0"
owner: "Hiren Bhavsar, VP Enterprise Growth PM, Transcarent"
---

# PRD Requirements Quality Evaluator

Scores a PRD's measurement readiness and auto-generates whatever is missing, so PRDs are
actually testable before they hit sprint planning — for both the internal tools Transcarent
care teams use and the member/client-facing tools employees and ASO-employer families use.

## Configuration

```
CONFLUENCE_CLOUD_ID: [SET THIS — find it via the Atlassian MCP `getAccessibleAtlassianResources`
tool, or ask the user once per workspace]
```

If a Confluence URL is given and this value is unset, ask the user for their cloud ID once, then
proceed. Don't ask again later in the same conversation.

## When to Use

Trigger on: "eval this PRD" / "score this PRD" / "review requirements quality" / "is this PRD
ready for sprint planning" / "does this have good KPIs / metrics / telemetry" / "generate the
missing KPI table / event schema / reporting spec" / a Confluence URL paired with any evaluation
intent / a pasted PRD with a question about measurement readiness.

## Step 1 — Acquire PRD Content

**Confluence first.** If the input contains a URL matching
`atlassian.net/wiki/spaces/.*/pages/(\d+)/`:
1. Extract the numeric page ID from the URL path after `/pages/`.
2. Call `getConfluencePage` with `cloudId` (see Configuration above), the extracted `pageId`,
   and `contentFormat: "markdown"`.
3. If it fails, tell the user and ask them to paste the PRD text instead.

**Local/pasted markdown fallback.** If no URL is given, or the fetch fails, use the PRD text
already in the conversation or a provided `.md` file.

**Sub-files — always ask, never guess.** If the PRD references appendices, linked specs, child
Confluence pages, or companion `.md` files, do not auto-fetch or scan for them. Ask the user to
name the exact URL(s) or file path(s) for each one before scoring. Scoring against a PRD you know
is incomplete will misrepresent the eval — say so explicitly if the user declines to provide them.

## Step 2 — Parse PRD Structure

Note presence or absence of each — this is scoring evidence:
- Initiative Overview / Problem Statement
- Goals / Success Criteria
- Business Rationale / OKR Alignment
- Solution / Detailed Requirements / User Stories
- Metrics / KPIs / Measurement section
- Telemetry / Instrumentation / Tracking section
- Reporting / Monitoring section
- Sign-off / DACI
- AI/Agent Architecture section (AI-Native PRDs)
- Accessibility / Health Literacy section (Mobile-First PRDs)
- Learning Loop / Iteration Plan (AI-Native PRDs)

## Step 3 — Classify the PRD

State all three classifications in the output header. They determine which criteria layers
apply in Step 4 — see `references/scoring-rubric.md` for the full detection signals and
per-dimension criteria tables.

| Flag | Values | Stackable? |
|------|--------|------------|
| **AI-Native** | Yes / No | Independent of Mobile-First |
| **Mobile-First** | Yes / No | Independent of AI-Native |
| **Audience** | Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid | Pick exactly one |

A PRD can be neither, either, or both AI-Native and Mobile-First — e.g., an AI care-navigation
agent inside the member app is both. Every PRD gets exactly one Audience label. Read
`references/scoring-rubric.md` before scoring — it has the full detection-signal lists.

## Step 4 — Score Each Dimension (0–5)

Read `references/scoring-rubric.md` for the complete rubric. Each of the 5 dimensions has up to
4 layers of criteria:
1. **Base criteria** — applies to every PRD.
2. **AI-Native layer** — applies only if classified AI-Native: Yes.
3. **Mobile-First layer** — member accessibility & health literacy bar; applies only if classified
   Mobile-First: Yes.
4. **Audience evidence note** — always applies; shifts what evidence counts based on the Audience
   classification.

To score 5/5 on any dimension, a PRD must satisfy **every layer that applies to it**. A PRD that
is both AI-Native and Mobile-First faces a higher bar than a plain infra PRD — this is
intentional, not a bug in the rubric.

## Step 5 — Calculate Score and Status

**Total Score** = sum of 5 dimension scores (max 25, same scale regardless of classification).

| Status | Score | Meaning |
|--------|-------|---------|
| 🟢 Green | 20–25 | Ready for implementation |
| 🟡 Yellow | 14–19 | Needs revision before implementation |
| 🔴 Red | 0–13 | Blocked — cannot advance to sprint planning |

## Step 6 — Auto-Generate Missing Sections

For every dimension scoring ≤2, generate the missing content using
`references/auto-gen-templates.md`. Generate one sub-block per layer that applies (Standard,
plus AI-Native and/or Mobile-First if classified as such). Use `[NEEDS PM INPUT]` for any value
that requires pulling from analytics — never fabricate numbers.

## Step 7 — Format and Deliver Output

Use the exact structure in `references/output-format.md`.

## Gotchas

Read `references/gotchas.md` before scoring — it holds known failure modes (e.g., don't credit
intent language like "leverage AI" or "mobile-friendly" as evidence). **Append new gotchas there**
whenever a real eval run surfaces a failure mode — that's how this skill gets better over time.

## Changelog

See `CHANGELOG.md` for version history and the reasoning behind past design changes.

```

## Notes

Uses new Anthropic skills format including a changelog and versioning, and reference files.  
