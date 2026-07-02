---
contributor: Hiren Bhavsar
team: Other
type: skill
name: prd-eval
filename: auto-gen-templates.md
submitted: 2026-07-02
---

# prd-eval — auto-gen-templates.md

**Contributor:** Hiren Bhavsar | **Team:** Other
**Type:** skill

## Description

Scores any PRD (Confluence link or pasted/local markdown) across 5 dimensions (Goal Quality, KPI Definition, Metrics Spec, Telemetry, Reporting) 0–25 total, auto-generates missing sections. Classifies each PRD on three independent axes — AI-Native (yes/no), Mobile-First (yes/no, stackable with AI-Native), and Audience (Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid) — so internal care-team tools and member/client-facing tools get held to the evidence bar that actually matters for their users.

## File Contents

```
# Auto-Generate Templates — prd-eval

For every dimension scoring ≤2, generate the Standard remediation block, plus one remediation
block per classification flag that applies (AI-Native and/or Mobile-First). Use
`[NEEDS PM INPUT]` for anything requiring real analytics data — never fabricate numbers.

---

## Goals Section (trigger: Goal Quality ≤ 2)

**Standard remediation:**

| # | Goal Statement | Outcome Type | Baseline | Target | Time Horizon | Owner | OKR Link |
|---|----------------|--------------|----------|--------|--------------|-------|----------|
| 1 | [Reframe as "Achieve [outcome] as measured by [metric]" — not "build X"] | Conversion / Retention / Cost / Clinical | [NEEDS PM INPUT] | [NEEDS PM INPUT] | [NEEDS PM INPUT] | [Role from DACI] | [NEEDS PM INPUT] |

**AI-Native remediation (if AI-Native: Yes):**

Rewrite the goal:
> "The [agent/system name] achieves [specific measurable outcome] for [member segment defined by
> signal] within [time horizon], as measured by [KPI with formula]."

Then the prototype hypothesis:
> **Prototype Hypothesis:** We believe that [surfacing/routing/recommending X] to [member
> segment Y identified by signal Z] will result in [outcome W measured by KPI V]. Testable with a
> Claude Code / Figma Make prototype against a cohort of [N] members before a full sprint.
> Validated if [numeric threshold] is achieved within [time window].

**Mobile-First remediation (if Mobile-First: Yes):**

> **Comprehension Target:** [X]% of members in [segment] complete [flow] unassisted, verified via
> a plain-language usability test with a representative sample including [low-literacy / non-
> English-primary / older-device] users. Baseline: [NEEDS PM INPUT]. Measured by: [method].

---

## KPI Table (trigger: KPI Definition ≤ 2)

**Standard remediation:**

| KPI Name | Formula | Data Source | Baseline | Target | Direction | Owner | Cadence | Alert Threshold |
|----------|---------|-------------|----------|--------|-----------|-------|---------|-----------------|
| [Derived from PRD flows] | [numerator / denominator] | [Mixpanel / DynamoDB / EDW] | [NEEDS PM INPUT] | [NEEDS PM INPUT] | ↑/↓ | [DACI Driver] | Weekly | [NEEDS PM INPUT] |

**AI-Native remediation (if AI-Native: Yes):**

**Agentic Work Unit Definition:**
> "One AWU for this PRD = [specific completed agent action that converts reasoning into a member
> health or cost outcome]. Surfacing a recommendation does NOT constitute an AWU. Only
> completion counts."

| AI-Native KPI | Formula | Data Source | Baseline | Target | Why This Matters |
|---------------|---------|-------------|----------|--------|-----------------|
| AWU Completion Rate | `agent_awu_completed` / `agent_recommendation_surfaced` | Mixpanel | [N/A — new] | [NEEDS PM INPUT] | Measures completed outcomes, not vanity engagement |
| Human Override Rate | `human_reviewer_override` / `agent_recommendations_reviewed` | Mixpanel | [N/A — new] | < 15%, declining to < 8% at scale | Measures agent accuracy and human trust over time |
| Model Accuracy Rate | Correct routings (human-validated) / total routings | Human eval log | [N/A — new] | ≥ 85% by sprint 6 | Direct measure of agent intelligence quality |

**Mobile-First remediation (if Mobile-First: Yes):**

| Mobile-First KPI | Formula | Data Source | Baseline | Target | Why This Matters |
|-------------------|---------|-------------|----------|--------|-----------------|
| Accessible Completion Rate | Completions by members flagged screen-reader/low-bandwidth / total completions by that segment | Mixpanel | [NEEDS PM INPUT] | Parity with general population within 10pp | Catches accessibility gaps hidden by a blended average |
| Support-Ticket Confusion Rate | Tickets tagged "flow confusion" for this feature / total sessions | Zendesk/Salesforce + Mixpanel | [NEEDS PM INPUT] | Declining trend | Direct signal of comprehension failures |

---

## Metrics Specification (trigger: Metrics ≤ 2)

**Standard remediation:**

| Metric Name | Definition | Calculation | Data Source | Baseline | Target | Alert Threshold |
|------------|-----------|-------------|-------------|----------|--------|-----------------|
| [Named metric from PRD intent] | [Plain English definition] | [Formula] | [Named system] | [NEEDS PM INPUT] | [NEEDS PM INPUT] | [Threshold] |

**AI-Native remediation (if AI-Native: Yes):**

**Proprietary Data Signal Identification:**
> "The unfair advantage powering this agent is: [specific Databricks table/signal/model output
> that no generic AI tool has access to]. Sourced from [claims data / member behavioral history /
> clinical outcomes / PG performance data]." [NEEDS PM INPUT — identify the specific source with
> data science]

| Agent Performance Metric | Definition | Formula | Source | Target | Alert |
|--------------------------|-----------|---------|--------|--------|-------|
| Recommendation Accuracy Rate | % of recommendations a human reviewer would endorse | Human-validated correct / total reviewed | Human eval log | ≥ 85% | < 75% |
| False Positive Rate | % of recommendations sent to members who aren't good candidates | False positives / total recommendations | Claims + Databricks | < 10% | > 20% |

**Mobile-First remediation (if Mobile-First: Yes):**

| Accessibility Metric | Definition | Formula | Source | Target | Alert |
|-----------------------|-----------|---------|--------|--------|-------|
| Reading Grade Level | Flesch-Kincaid grade level of member-facing copy | Automated readability scan | Content QA tool | ≤ 6th grade | > 8th grade |
| WCAG Audit Pass Rate | % of automated WCAG 2.1 AA checks passing | Passing checks / total checks | Accessibility audit tool | ≥ 95% | < 85% |

---

## Telemetry Event Schema (trigger: Telemetry ≤ 2)

**Standard remediation — user event catalog.** Use snake_case, prefixed with domain (e.g.,
`tpe_`, `tha_`, `find_care_`, `auth_`).

**Universal Required Properties (every event):**

| Property | Type | Description |
|----------|------|--------------|
| `event_name` | string | Snake_case identifier |
| `user_id` | string (UUID) | Transcarent member ID |
| `session_id` | string | Current session |
| `flow_type` | enum | Which product flow triggered this |
| `step_name` | string | Human-readable step |
| `success` | boolean | Did this step complete |
| `error_type` | string or null | Error code if failed |
| `timestamp` | ISO 8601 | UTC |
| `platform` | enum | ios / android / web |

**AI-Native remediation (if AI-Native: Yes) — agent decision events + HITL schema:**

| Event Name | Trigger | Required Properties | Maps to KPI | Priority |
|-----------|---------|---------------------|-------------|----------|
| `[domain]_agent_evaluation_started` | Agent begins reasoning | `member_id`, `signal_source`, `signal_value`, `candidate_count` | — | P0 |
| `[domain]_agent_recommendation_generated` | Agent produces output | `recommendation_id`, `confidence_score`, `recommended_partner_id`, `reasoning_summary`, `data_signals_used[]` | Model Accuracy Rate | P0 |
| `[domain]_agent_recommendation_surfaced` | Recommendation shown to member | `recommendation_id`, `member_id`, `surface_location` | AWU Initiation denominator | P0 |
| `[domain]_agent_awu_completed` | Member completes the full recommended action | `recommendation_id`, `member_id`, `days_since_recommendation`, `completion_type` | AWU Completion Rate numerator | **P0 — defining event** |
| `[domain]_human_reviewer_override` | Reviewer corrects the agent | `recommendation_id`, `reviewer_id`, `original_recommendation`, `corrected_recommendation`, `override_reason` | Human Override Rate; Learning Loop input | **P0 — feeds retraining** |

**Mobile-First remediation (if Mobile-First: Yes) — accessibility & degraded-state events:**

| Event Name | Trigger | Required Properties | Maps to KPI | Priority |
|-----------|---------|---------------------|-------------|----------|
| `[domain]_accessibility_feature_used` | Member uses an assistive-tech feature | `feature_type` (screen_reader/font_scale/voiceover), `session_id` | Accessible Completion Rate | P0 |
| `[domain]_low_bandwidth_fallback_triggered` | App detects and switches to a low-bandwidth mode | `fallback_type`, `original_action` | Support-Ticket Confusion Rate | P1 |
| `[domain]_offline_state_entered` | Device loses connectivity mid-flow | `step_name`, `duration_seconds` | — | P1 |

---

## Reporting & Monitoring Spec (trigger: Reporting ≤ 2)

**Standard remediation:**

| Dashboard Name | Metrics Included | Primary Audience | Cadence | Alert Condition | Alert Channel | Action Owner |
|----------------|-----------------|-----------------|---------|-----------------|---------------|--------------|
| [Derived from PRD] | [KPIs from PRD] | [DACI Driver + PM] | Weekly | [NEEDS PM INPUT] | Slack | [NEEDS PM INPUT] |

**AI-Native remediation (if AI-Native: Yes) — human eval + learning loop + scale criteria:**

> **Human Eval Review Process:** Who reviews: [NEEDS PM INPUT]. Cadence: weekly, reviewing
> [N=25] randomly sampled agent recommendations. What they evaluate: was the recommendation
> correct, would a human expert endorse it. Log: override reason captured in
> `[domain]_human_reviewer_override`. Escalation: if override rate > 20% in any week, pause agent
> recommendations and convene review.
>
> **Learning Loop:** Override events auto-populate a ticket assigned to [NEEDS PM INPUT — data
> science lead]. Weekly review of override patterns. Model retraining or rule update shipped
> within 2 sprints of an override spike.
>
> **Prototype Evaluation Framework:** Validated when AWU Completion Rate ≥ [NEEDS PM INPUT]
> within the first [N] member cohort, human override rate ≤ 20% from the first eval cycle, and no
> patient safety flags raised.
>
> **Scale Criteria:** Advance Prototype → Scale when the prototype hypothesis is validated, human
> override rate ≤ 15% for 2 consecutive eval cycles, AWU Completion Rate stable/improving for 3
> consecutive weeks, and clinical sign-off is obtained.

**Mobile-First remediation (if Mobile-First: Yes) — accessibility review checkpoint:**

> **Accessibility Review Process:** Who reviews: [NEEDS PM INPUT — design/accessibility lead].
> Cadence: monthly (or before every release touching member-facing copy). What they evaluate: a
> screen-reader pass on the primary flow, plus a plain-language readability check (target ≤ 6th
> grade) on all new member-facing copy. Escalation: release is blocked if either check fails.

```

## Notes

Uses new Anthropic skills format including a changelog and versioning, and reference files.  
