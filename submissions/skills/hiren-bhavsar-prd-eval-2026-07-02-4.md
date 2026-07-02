---
contributor: Hiren Bhavsar
team: Other
type: skill
name: prd-eval
filename: scoring-rubric.md
submitted: 2026-07-02
---

# prd-eval — scoring-rubric.md

**Contributor:** Hiren Bhavsar | **Team:** Other
**Type:** skill

## Description

Scores any PRD (Confluence link or pasted/local markdown) across 5 dimensions (Goal Quality, KPI Definition, Metrics Spec, Telemetry, Reporting) 0–25 total, auto-generates missing sections. Classifies each PRD on three independent axes — AI-Native (yes/no), Mobile-First (yes/no, stackable with AI-Native), and Audience (Internal Care Team Tool / Member-Facing / Client-ASO-Facing / Hybrid) — so internal care-team tools and member/client-facing tools get held to the evidence bar that actually matters for their users.

## File Contents

```
# Scoring Rubric — prd-eval

Full per-dimension criteria for all 4 layers: Base, AI-Native, Mobile-First, Audience.
Read this before scoring any PRD.

**How to read the layers:** AI-Native and Mobile-First layers only raise the *ceiling* — they
add requirements a PRD must meet to reach a 5 (or 4) on that dimension. If the Base score is
already below where a layer would apply (e.g., Base = 1 or 2), don't subtract further for an
unmet AI-Native or Mobile-First layer — the Base score already reflects the gap. Likewise, the
Audience evidence note's caps (e.g., "caps at 3") are ceilings, not floors: they only pull a score
down when the Base/layer scoring would otherwise land higher than the cap allows.

---

## Classification Detection Signals

### AI-Native: Yes
Recommendation engines, care navigation agents, personalization systems, agentic workflows, AI
care assistants, clinical decision support, intelligent member journey orchestration,
THA/WayFinding intelligence, Find Care intelligent steerage, CLaRA agent, TPE matching.
Keywords: recommendation, personalization, agent, AI, ML, prediction, smart routing, care
navigation, propensity score, Databricks signal, agentic, orchestration, adaptive.

### Mobile-First: Yes
Member mobile app features, employee/family-facing flows, any experience where the primary
surface is a phone and the primary audience is a non-technical member population.
Keywords: member app, mobile, iOS/Android, push notification, employee, family, dependent,
on-the-go, home screen, app store.

### Audience
- **Internal Care Team Tool** — used by Transcarent care advocates, clinicians, CSRs, nurses, or
  internal ops staff. Keywords: care advocate, internal dashboard, CSR, clinician workflow,
  agent console, back-office, queue management.
- **Member-Facing** — used directly by employees/dependents of client companies. Keywords:
  member app, member portal, employee, family, dependent, self-service.
- **Client-ASO-Facing** — used by the self-insured employer (the client) itself, e.g. benefits
  admin, HR, or employer reporting tools. Keywords: employer dashboard, client reporting, HR
  admin, benefits admin portal, ASO client.
- **Hybrid** — genuinely serves two+ of the above as primary users (e.g., a care-team dashboard
  that surfaces member-authored data and drives member-visible outcomes). Use sparingly — default
  to the single dominant primary user if unclear, and note the ambiguity in the eval output.

If a PRD shows both AI-Native and Mobile-First signals, classify it as both (they're independent).
If none of the AI-Native or Mobile-First signals appear, both flags are No — this is a standard
PRD scored on Base criteria only.

---

## DIMENSION 1: Goal Quality

**What this measures:** Are goals outcome-oriented, time-bound, baselined, and traceable to an
OKR?

### Base Criteria

| Score | Criteria |
|-------|----------|
| 5 | Every goal: (a) outcome/impact, not output; (b) time-bound with explicit deadline; (c) linked to OKR or North Star; (d) numeric baseline; (e) specific numeric target |
| 4 | Outcome-oriented with targets, missing one of: time-bound, OKR link, or baseline |
| 3 | Attempts measurement but baselines or targets are absent or vague |
| 2 | Output/delivery-focused ("build X", "migrate to Y", "ship the new UI") |
| 1 | Goals exist but contain placeholder content OR are entirely qualitative |
| 0 | No goals or success criteria section exists |

### AI-Native Layer (applies only if AI-Native: Yes)

At score 5, ALSO require: (a) goal framed as what the agent achieves for the member, not what
the team builds ("The recommendation agent routes members with [signal] to [partner/provider]
within 48 hours" not "Build a recommendation engine"); (b) a prototype-first hypothesis:
"We believe [agent action X] for [member segment Y with signal Z] will produce [outcome W] —
testable in Claude Code / Figma Make before a full sprint"; (c) which AI-Native Model phase
applies (Prototype / Learn / Scale). At score 4: agent-framed goal present, no hypothesis. At
score 3: outcome-oriented but still waterfall-framed, no agent target, no prototype thinking.

**Green flag:** "Increase AWU completion rate for MSK-flagged members from 0 to 15% by end of
Q3", with a stated prototype hypothesis.
**Red flag:** "Build a smarter recommendation engine", "Leverage AI to enhance the member
experience" — intent without an agent-framed target.

### Mobile-First Layer (applies only if Mobile-First: Yes)

At score 5, ALSO require: goals state a plain-language comprehension target for the primary
audience (e.g., "member understands the recommended action without contacting support, measured
by a post-interaction comprehension survey ≥ 90%") — not just a usage or adoption number. At
score 4: usage/adoption goal present but no comprehension or literacy target. At score 3 and
below: no explicit accessibility or literacy consideration in goals at all.

**Green flag:** "80% of members complete the enrollment flow unassisted, verified via a plain-
language usability test with a representative member sample."
**Red flag:** "Increase mobile app engagement" with no comprehension, accessibility, or literacy
angle — engagement alone doesn't tell you whether the member actually understood the flow.

### Audience Evidence Note (always applies)

- **Internal Care Team Tool** — goals must cite care-team workflow evidence: time saved per case,
  reduction in manual lookups, fewer escalations. A goal with no workflow-friction evidence caps
  at 3, regardless of other criteria.
- **Member-Facing** — goals must show a health-equity/disparate-impact consideration (e.g., does
  this improve or worsen outcomes for lower-income, non-English-primary, or high-risk cohorts?).
- **Client-ASO-Facing** — goals must tie to an employer-reported outcome the client cares about
  (PMPM, utilization, absenteeism, NPS from the employer relationship, not just member metrics).
- **Hybrid** — must show evidence for at least two of the above; note which two in the eval output.

---

## DIMENSION 2: KPI Definition

**What this measures:** Are KPIs formally defined with formula, baseline, target, owner, cadence?

The **Agentic Work Unit (AWU)** is the unit of business value for agentic systems: *a single unit
of completed work where an AI agent converts reasoning into an action that results in a
measurable health or cost outcome for a member.* A successful AWU is not a chatbot answering a
question — it's an agent completing a booking, an enrollment, or a care pathway navigation for a
higher-quality, lower-cost provider.

### Base Criteria

| Score | Criteria |
|-------|----------|
| 5 | KPIs: (a) formal name; (b) calculation formula; (c) baseline with source; (d) numeric target; (e) owner; (f) measurement cadence |
| 4 | Formula and target present, missing owner or cadence |
| 3 | KPIs implied from success criteria; no formulas |
| 2 | Category-level only ("conversion rates", "engagement") |
| 1 | No KPI section; metrics referenced elsewhere |
| 0 | No KPIs anywhere |

### AI-Native Layer

At score 5, ALSO require: (a) AWU explicitly defined ("One AWU = [specific completed agent
action]"); (b) AWU Completion Rate KPI (completed AWUs / initiated AWUs), not just surface-level
engagement; (c) a Learning Efficiency KPI showing how the agent improves over time (declining
human override rate, improving model accuracy, rising AWU completion per session); (d) KPIs do
NOT measure only tokens processed, AI calls made, or recommendations surfaced. At score 4: AWU
defined + completion KPI, no learning-efficiency KPI. At score 3: outcome-oriented KPIs but no
AWU concept — measuring clicks/impressions, not completions. At score 2: purely engagement/vanity
KPIs (surfaced, clicked, opened).

**Green flag:** "AWU = member accepted care navigation recommendation AND completed provider
booking within 7 days | AWU Completion Rate = completed_bookings / recommendations_accepted |
Target: 18% by sprint 6 | Owner: [name] | Cadence: weekly."
**Red flag:** KPIs that only measure "THA impressions", "recommendation CTR", "AI suggestions
generated" — these measure the agent doing something, not completing something of value.

### Mobile-First Layer

At score 5, ALSO require a KPI that measures accessibility/comprehension outcomes directly, not
just usage volume — e.g., "% of support-ticket volume attributable to confusion about mobile
flow" trending down, or "task completion rate for members using assistive tech" tracked
separately from the general population. At score 4: usage KPI present, no accessibility-specific
KPI. At score 3 and below: no distinction between general usage and accessible-usage outcomes.

**Green flag:** "Accessible Completion Rate = completions by members flagged as using
screen-reader or low-bandwidth mode / total completions by that segment | Target: parity with
general population within 10pp."
**Red flag:** A single blended completion-rate KPI with no visibility into whether it holds up
for members with accessibility needs or low digital literacy.

### Audience Evidence Note

- **Internal Care Team Tool** — KPI set must include an efficiency metric owned by care
  operations (average handle time, cases resolved per shift), not just a product-team vanity metric.
- **Member-Facing** — KPI set must be segmentable by member cohort (age, language, risk tier) to
  catch disparate impact, not just reported in aggregate.
- **Client-ASO-Facing** — KPI set must map to something reportable back to the employer (a metric
  that would appear in a client QBR), not just an internal product metric.
- **Hybrid** — needs at least one KPI satisfying two of the above; call out which in the eval.

---

## DIMENSION 3: Metrics Specification

**What this measures:** Are specific metrics defined with formula, data source, baseline,
target, and alert thresholds?

### Base Criteria

| Score | Criteria |
|-------|----------|
| 5 | Each metric: (a) precise name; (b) calculation formula; (c) named data source (Mixpanel, DynamoDB, claims, EDW, etc.); (d) baseline; (e) numeric target; (f) alert threshold |
| 4 | Named metrics with source and baseline; missing alert thresholds |
| 3 | Named metrics with source; no baselines or targets |
| 2 | Category-level only; no formula, no source identification |
| 1 | Only implicit metrics referenced in goals |
| 0 | No metrics referenced |

### AI-Native Layer

At score 5, ALSO require: (a) the proprietary data signal powering the agent is named — a
specific Databricks table, claims signal, or behavioral pattern, not just "member data" (this is
the unfair advantage — see Gotchas); (b) agent performance metrics alongside user metrics: model
accuracy rate, human override rate, false positive rate, confidence threshold; (c) a learning
loop metric showing how the metric improves as the agent learns. At score 4: proprietary signal
+ agent performance metrics, no learning loop metric. At score 3: agent metrics present but
grounded in generic data only. At score 2: only user-facing funnel metrics, no agent performance
metrics — could be powered by any generic model.

**Green flag:** "Signal source: Databricks `high_cost_member_propensity_score` ≥ 0.7 AND
primary_condition = 'MSK' | Agent accuracy rate = correct routing / total routings | Target ≥ 85%."
**Red flag:** "The AI model will use member health data to make recommendations" — generic
framing that provides no proprietary moat and would score identically for any competitor.

### Mobile-First Layer

At score 5, ALSO require a named accessibility/readability metric with a formula and target —
e.g., content reading-grade-level score, WCAG audit pass rate, or crash/error rate on
low-end/older devices — tracked as a first-class metric, not an afterthought. At score 4: metric
named but no formal target. At score 3 and below: no accessibility metric at all.

**Green flag:** "Flesch-Kincaid reading grade level of all member-facing copy ≤ 6th grade,
audited quarterly | WCAG 2.1 AA automated audit pass rate ≥ 95%."
**Red flag:** No metric addresses whether content is comprehensible or usable on older/low-end
devices common among the member population.

### Audience Evidence Note

- **Internal Care Team Tool** — metrics should include a data source the care-ops team already
  trusts (their existing case-management system), not just a new product analytics tool nobody
  on that team monitors.
- **Member-Facing** — metrics must be capable of being sliced by demographic/equity cohort.
- **Client-ASO-Facing** — at least one metric must be sourced from data the client can see or
  receive (claims, utilization), not purely internal product telemetry.
- **Hybrid** — needs metrics satisfying two of the above; call out which in the eval.

---

## DIMENSION 4: Telemetry / Instrumentation

**What this measures:** Are specific event names, property schemas, and KPI mappings defined?

### Base Criteria

| Score | Criteria |
|-------|----------|
| 5 | (a) Snake_case event names for every user story step; (b) property schema (fields, types, enums); (c) event → KPI mapping; (d) error/edge case events; (e) implementation tickets linked |
| 4 | Named events with properties; KPI mapping missing or some error events absent |
| 3 | Event categories defined but not specific snake_case names |
| 2 | Category-level only ("each step triggers an event"); no event names, no schema |
| 1 | Tracking mentioned as a goal; zero specification |
| 0 | No telemetry specification |

### AI-Native Layer

At score 5, ALSO require: (a) agent decision events instrumented, not just user actions — when
did the agent evaluate, what confidence score, what signals fed the decision, what output; (b) an
AWU completion event marking the moment the agent's action results in a member outcome, not just
a recommendation surfaced; (c) human-in-the-loop events: when a reviewer sees agent output, when
they accept/override/reject, and what the correction was (feeds the learning loop); (d) agent
observability — no black-box outputs. At score 4: agent events + AWU completion event, human
override events absent. At score 3: AWU completion event defined, no agent reasoning or HITL
events. At score 2: only user events, no agent decision events, no human override events.

**Green flag events:** `agent_recommendation_evaluated` (confidence_score, signal_source),
`agent_awu_completed` (the defining event, maps to AWU Completion Rate),
`human_reviewer_override` (original_recommendation, override_reason — feeds learning loop).
**Red flag:** Only user-facing events; no event distinguishes "recommendation shown" from
"recommendation acted upon"; no human override instrumentation (treats the agent as fully
autonomous, which produces worse outcomes without oversight).

### Mobile-First Layer

At score 5, ALSO require events that capture assistive-tech usage and degraded-condition
behavior — e.g., `accessibility_feature_used` (screen_reader, font_scale, voiceover),
`low_bandwidth_fallback_triggered`, `offline_state_entered` — so the team can see whether the
accessible path actually gets used and whether it breaks under real member conditions. At score
4: some of these present but incomplete. At score 3 and below: no accessibility/degraded-state
events at all.

**Green flag events:** `accessibility_feature_used` (feature_type, session_id),
`low_bandwidth_fallback_triggered` (fallback_type, original_action).
**Red flag:** Standard happy-path events only — no way to tell whether the flow works for a
member on an older device or using a screen reader.

### Audience Evidence Note

- **Internal Care Team Tool** — telemetry should capture care-team time-on-task per event, not
  just completion, so workflow-efficiency claims in Goals/KPIs are actually measurable.
- **Member-Facing** — telemetry must be able to segment by member cohort without collecting new
  PHI beyond what's already governed (flag if new PHI collection isn't addressed).
- **Client-ASO-Facing** — telemetry should map cleanly to whatever the client-facing report/
  dashboard will show, so there's no gap between what's tracked and what's promised to the client.
- **Hybrid** — needs telemetry satisfying two of the above; call out which in the eval.

---

## DIMENSION 5: Reporting & Monitoring

**What this measures:** Is there a defined plan for dashboards, audiences, cadence, alerts, and
action protocols?

### Base Criteria

| Score | Criteria |
|-------|----------|
| 5 | (a) Dashboard name and structure; (b) stakeholder audiences named; (c) reporting cadence; (d) alert conditions with numeric thresholds; (e) escalation/action protocol |
| 4 | Dashboard intent clear, stakeholders named, cadence defined; alert conditions absent |
| 3 | Reporting mentioned with some stakeholder context; no cadence or dashboard structure |
| 2 | Monitoring implied through success criteria; no explicit reporting plan |
| 1 | No reporting section; data collection mentioned elsewhere |
| 0 | No monitoring or reporting anywhere |

### AI-Native Layer

At score 5, ALSO require: (a) a human eval review process — who reviews agent outputs, at what
cadence, against what criteria, what "good" vs "bad" looks like; (b) a learning loop — a defined
process (not just a dashboard) routing agent outcome data back to model retraining or rule
updates; (c) a prototype evaluation framework defining what "validated" means quantitatively;
(d) scale criteria — the numeric threshold for advancing Prototype → Learn → Scale. At score 4:
human eval process + learning loop present, no prototype evaluation framework or scale criteria.
At score 3: monitoring plan with stakeholder context, no human eval process, no learning loop.

**Green flag:** "Weekly Human Eval Review: PM + clinical stakeholder review 25 random agent
recommendations against ground truth; log override rate | Learning Loop: override events feed
weekly retrain ticket | Scale Trigger: validated prototype + override rate < 15% → production."
**Red flag:** A dashboard with no human review process; monitoring alerts with no feedback
mechanism to improve the model.

### Mobile-First Layer

At score 5, ALSO require an accessibility review checkpoint alongside (or inside) the human eval
process — who reviews accessibility/comprehension on a defined cadence, using what criteria
(e.g., a plain-language readability check, an assistive-tech usability pass), and what happens
when it fails. At score 4: accessibility mentioned but no defined cadence or reviewer. At score 3
and below: no accessibility review process at all.

**Green flag:** "Monthly Accessibility Review: design lead runs a screen-reader pass and a
6th-grade readability check on all new member-facing copy before release; blocks release if
either fails."
**Red flag:** Reporting plan covers engagement metrics only — no one is ever explicitly
responsible for checking whether the experience is actually accessible.

### Audience Evidence Note

- **Internal Care Team Tool** — reporting audience must include a care-ops manager who can act on
  workflow-friction findings, not just the product team.
- **Member-Facing** — reporting must include an equity-lens review (are outcomes holding up
  across demographic cohorts), not just an aggregate dashboard.
- **Client-ASO-Facing** — reporting must define what, if anything, gets shared back to the client
  and on what cadence (client QBR, monthly report) — a purely internal dashboard is insufficient.
- **Hybrid** — needs reporting satisfying two of the above; call out which in the eval.

```

## Notes

Uses new Anthropic skills format including a changelog and versioning, and reference files.  
