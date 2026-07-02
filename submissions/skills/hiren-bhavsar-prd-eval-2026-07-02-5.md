---
contributor: Hiren Bhavsar
team: Other
type: skill
name: prd-eval
filename: output-format.md
submitted: 2026-07-02
---

# prd-eval — output-format.md

**Contributor:** Hiren Bhavsar | **Team:** Other
**Type:** skill

## Description

Scores any PRD (Confluence link or pasted/local markdown) across 5 dimensions (Goal Quality, KPI Definition, Metrics Spec, Telemetry, Reporting) 0–25 total, auto-generates missing sections. Classifies each PRD on three independent axes — AI-Native (yes/no), Mobile-First (yes/no, stackable with AI-Native), and Audience (Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid) — so internal care-team tools and member/client-facing tools get held to the evidence bar that actually matters for their users.

## File Contents

```
# Output Format — prd-eval

Deliver the eval in exactly this structure.

```
---

## 📊 PRD Requirements Quality Eval
**PRD Title:** [title]
**Classification:** AI-Native: [Yes/No] · Mobile-First: [Yes/No] · Audience: [Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid]
**Evaluated:** [today's date]
**Source:** [Confluence URL] OR [Pasted/local text]
**Skill Version:** prd-eval v1.0.0

---

### Overall Score: X / 25 — [🔴 Blocked / 🟡 Needs Revision / 🟢 Ready]

**AI-Native Readiness:** [🔴 Not ready / 🟡 Partial / 🟢 Ready] — [N/A if AI-Native: No]
**Mobile-First Readiness:** [🔴 Not ready / 🟡 Partial / 🟢 Ready] — [N/A if Mobile-First: No]

| Dimension | Score | Status | Critical Gap |
|-----------|-------|--------|---------------|
| Goal Quality | X/5 | 🔴/🟡/🟢 | [one-line summary] |
| KPI Definition | X/5 | | |
| Metrics Specification | X/5 | | |
| Telemetry / Instrumentation | X/5 | | |
| Reporting & Monitoring | X/5 | | |

**Immediate Action:** [One sentence naming what blocks this PRD, and who owns fixing it — PM for
standard gaps, data science for AI-Native gaps (e.g., AWU definition), design/accessibility lead
for Mobile-First gaps.]

---

### Dimension 1: Goal Quality — X/5
**Classification applied:** [which layers were scored: Base / + AI-Native / + Mobile-First]
**What was found:** [2–3 sentences quoting directly from the PRD]
**Critical gaps:** [Bulleted list citing specific evidence]
**Why this score:** [1 sentence]

#### 🔧 AUTO-GENERATED: Recommended Goals Section
[Standard goals table]

#### 🤖 AUTO-GENERATED (if AI-Native: Yes): Agent-Framed Goal + Prototype Hypothesis
[Block from auto-gen-templates.md]

#### 📱 AUTO-GENERATED (if Mobile-First: Yes): Comprehension Target
[Block from auto-gen-templates.md]

---

[Repeat this structure for all 5 dimensions]

---

### How to Use This Report
1. PM owns remediation of all 🔴 dimensions.
2. Fill in every `[NEEDS PM INPUT]` field from real analytics/data sources — never guess.
3. If AI-Native: coordinate the AWU definition with data science before finalizing the KPI section.
4. If AI-Native: the prototype hypothesis needs an actual working prototype before it's "done" —
   a written statement is necessary but not sufficient.
5. If Mobile-First: coordinate the accessibility metric targets with design before finalizing.
6. Paste auto-generated sections into the PRD.
7. Re-run prd-eval after revisions; target ≥ 20/25 before sprint planning.
```

```

## Notes

Uses new Anthropic skills format including a changelog and versioning, and reference files.  
