---
contributor: Michael Lo Sasso
team: Not Skynet
type: skill
name: demo-design-stress-test
submitted: 2026-08-21
---

# demo-design-stress-test

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** skill

## Description

Stress-tests designs, specs, and screens built for the Transcarent React clickable demo framework against presenter configuration, live-demo flow integrity, content volatility, component and token drift, and brand-template conformance. Use when a Figma frame or link, screenshot, written spec, PR, component, or a Figma Make zip export / built code from the demo framework is shared and the request is a design review, critique, buildability or feasibility check, post-build verification pass, edge-case pass, pre-build check, or an ask to "grill" a design. Do not use for reviews of the production member-facing app.

## File Contents

```
---
name: demo-design-stress-test
description: Stress-tests designs, specs, and screens built for the Transcarent React clickable demo framework against presenter configuration, live-demo flow integrity, content volatility, component and token drift, and brand-template conformance. Use when a Figma frame or link, screenshot, written spec, PR, component, or a Figma Make zip export / built code from the demo framework is shared and the request is a design review, critique, buildability or feasibility check, post-build verification pass, edge-case pass, pre-build check, or an ask to "grill" a design. Do not use for reviews of the production member-facing app.
---

# Demo Design Stress-Test

Review designs destined for the clickable demo framework: a configurable React app that
sales presenters drive live, on screen share, in front of prospects and clients. Optimize
findings for that context. A finding is only worth raising if it could plausibly cause a
bad build, a bad configuration, or a bad moment in a live client demo.

## 1. Scope check — do this first

Confirm the artifact is a demo-framework surface. If it is production member-facing app
work, a marketing asset, or an unrelated internal tool, say so in one line and stop.
Several pillars below are deliberately mis-calibrated for production and will generate
misleading findings there.

## 2. Inputs

These are not arguments. Infer each from the request; fall back to the default. State the
resolved values in one line at the top of the review.

| Input | How to resolve | Default |
| --- | --- | --- |
| `artifact_fidelity` | Detect from what was shared: Figma link, static image, written spec, code/PR, or Make zip export | Detect; never assume code access |
| `intensity` | Honor an explicit ask ("go hard", "be gentle") | `standard` |
| `focus` | Honor an explicit narrowing ("just the config risk") | All six pillars |

`intensity` controls tone and directness only. It must never change which findings appear
or how they are severity-rated. A blocker at `collaborative` is the same blocker at `grill`.

- `collaborative` — plain, partnering, assumes shared goals.
- `standard` — direct senior-engineer register. Blunt about risk, not about people.
- `grill` — adversarial interrogation. Opt-in only; never the default.

## 3. Respect artifact fidelity

Match claims to what the input can actually support. State the limit rather than guessing.

- **Static image** — layout, hierarchy, and content-volatility risk are visible. Truncation
  behavior, container reservation, transition timing, and token usage are not. Ask.
- **Figma link/frame** — add constraints, auto-layout, and variant structure. Runtime
  behavior is still unknown.
- **Written spec** — configuration surface and flow logic are reviewable. Visual density is not.
- **Code/PR** — everything is reviewable. Only here may claims be made about implementation
  behavior.
- **Make zip export** — highest fidelity. Verify rather than ask. See section 3.5.

Never assert a runtime defect (leak, thrash, re-render storm) from a design artifact.

### Repo ground truth

When running inside the framework repo, two files serve different purposes. Both outrank
any assumption in this skill.

- `presenter-cheat-sheet.md` — the real presenter-editable configuration surface. Use it to
  ground pillar A. If it contradicts a specific named in pillar A, it wins.
- `guidelines/Guidelines.md` (the Make instruction rules — dos and don'ts) — the constraints Make was
  already told to follow. Not a config reference. Use it two ways: as a finding source when
  built output violates a stated rule, and as the format the Next Make prompt must comply
  with. Never propose prompt language that contradicts a standing guideline.

## 3.5 Make zip export mode

A Figma Make zip is post-build output, not a pre-build design. Reframe accordingly:
findings cannot gate a build that already ran, so they must convert into the next Make
prompt. Produce prompt language, never patches.

### Constraints

- Unpack to a scratch directory outside the repo. Never unpack into `src/`, and never
  commit zip contents.
- Reading `src/` is expected. Editing it is forbidden — all React changes go through Make
  prompts. Do not write, patch, or "fix" built code under any circumstance.

### Orient before reading

List the file tree first. Locate the config or data module holding presenter-editable
content, the component directory, and the screen/route entry points. Read those, not
everything.

### Verify instead of asking

With code present, most of pillar A and C is checkable. A verified finding beats a
question. Downgrade to a question only when the code genuinely does not settle it.

- Enumerate the real config fields and defaults, then compare against what screens consume.
- Flag hard-coded strings that should be configurable, and config fields no screen reads.
- Check what the featured-program layout actually does at 0, 1, 2, and more than 3.
- Check CTA label rendering: fixed width, truncation, wrap.
- Trace every click target and route for dead ends and missing back paths.
- Enumerate the theme/token definitions, then grep for literal colors, font stacks, and
  spacing values in component code. Every literal that has a defined token is a finding.
- Inventory components and count usages. Single-use components, near-duplicate names, and
  repeated inline blocks are the componentization findings for pillar D. Report counts.
- Check built output against the standing Make guidelines. A rule that was stated and then
  not followed is a high-confidence finding: cite the guideline, then the code that departs
  from it. Repeat offenders are worth flagging as a guideline that needs rewording, not just
  a one-off fix.
- If a previous zip or the current repo `src/` is available, diff against it and report what
  changed rather than re-reviewing the whole app.

## 4. The six pillars

### A. Presenter configuration integrity
The highest-value pillar. Presenter-configurable content is the framework's core
capability and its main source of breakage.

- Featured programs default to and cap at 3. What does this layout do at 2, at 1, at 0?
- Detail-screen CTA text is variable, not fixed to "Visit Website". Does the button
  survive a long label, and is the wrap/truncate behavior specified?
- Program and category names are configured strings. What is the character budget before
  the card, tile, or nav label breaks containment?
- What renders for a benefit category a presenter has left with zero programs?
- Which fields on this screen are configurable versus hard-coded, and is that split
  written down anywhere a presenter would find it?

### B. Live-demo flow integrity
The demo is driven manually, in real time, by someone talking to a client.

- Every interactive element in frame: does it go somewhere, or is it a dead click a
  presenter will hit on stage? Dead ends are blockers here, not nits.
- Can the presenter get back out? Is back/close behavior defined for each entry path?
- If a screen is reachable from more than one entry point, does it render correctly from
  each, including a configured start point that skips earlier steps?
- Does the path still read correctly when clicked out of the intended order?
- Programs may land on a generic detail page and optionally link onward into a program
  flow. Which behavior does this screen assume, and is the onward link conditional?

### C. Content volatility in fixed layouts
- Longest realistic configured string versus the mockup's happy-path string.
- Long unbroken tokens: plan names, member names, program titles with no spaces.
- Values that grow: claim amounts, spending figures, counts. Is the container elastic or
  is it sized to the sample data?
- Truncation versus wrapping — specified, or left to the implementer to invent?

### D. Componentization and drift
Make generates working code, not factored code. It will reproduce a pattern inline on six
screens rather than extract it once. That is the dominant maintenance cost in this codebase,
so treat extraction opportunities as first-class findings, not cleanup notes.

**Componentization opportunities.** For each, name the duplicate sites, the proposed
component, and the props it needs. Rank by number of duplicate sites — that is the payoff.

- Repeated JSX blocks that differ only in content or a single variant flag.
- Near-identical components with divergent names, or one component copied and lightly edited.
- Repeated literal values (spacing, radius, color, type size) appearing across files, which
  signal a missing token as much as a missing component.
- Layout scaffolding — card shells, list rows, section headers, sheet/modal chrome — rebuilt
  per screen instead of shared.
- One-off components used exactly once that could collapse into an existing variant.

Severity here is usually **define before build**. Escalate to blocker only when duplication
means a presenter-configurable value has to be edited in more than one place to stay
consistent — that is a live-demo correctness risk, not a tidiness issue.

**Drift.**
- Is this a genuinely new component, or a near-variant of something already in the
  framework? Name the existing component if one exists.
- Can it be built from existing tokens and primitives, or does it require bespoke CSS
  that no one will maintain?
- Does it duplicate a pattern that appears elsewhere with slightly different spacing,
  radius, or type scale? Divergence here compounds fast across demo screens.

### E. Brand and template conformance
This skill carries no brand values. The codebase is the source of truth. Resolve one before
reviewing and name it in the review header.

1. **The framework's own token definitions** — theme file, Tailwind config, CSS custom
   properties, or a tokens module in the repo or zip. Authoritative for what the demo
   actually renders. Enumerate the defined tokens before judging any screen.
2. `guidelines/Guidelines.md`, if it states brand rules.

With tokens resolved, the reviewable question is conformance to them, not correctness of
them. Do not judge whether a defined token is the right brand value — that is not knowable
from the codebase and is out of scope.

If neither resolves, say so and skip this pillar. Do not assert a hex value, font name, or
spacing scale from memory, and do not infer brand intent from what the artifact happens
to contain — the artifact is what is under review.

With a source resolved:
- Internal consistency: does every screen use the same resolved tokens, or has one screen
  drifted to a near-miss value?
- Hard-coded values that bypass the token system, which is drift regardless of whether the
  value is correct. In a Make export this is the most common and most checkable violation.
- Does anything read as placeholder, stock, or off-brand in a way a client would notice on
  a shared screen?

### F. Demo-surface performance and perception
Narrow on purpose. Only raise what a viewer on a screen share would perceive.

- Transitions or animations heavy enough to stutter while screen sharing.
- Layout jump on load that reads as a bug to a watching client.
- Asset weight that could stall on conference or VPN wifi.

Do not raise mobile frame rates, bundle-size budgets, or micro-optimizations.

## 5. Severity tiers

Every finding carries exactly one tier. Do not inflate to fill space.

- **Blocker** — will break the build or the live demo. Must be resolved before build.
- **Define before build** — reasonable design, missing operational detail an implementer
  would otherwise invent. Most findings land here.
- **Accepted risk** — real but acceptable at demo-surface stakes. Note once, move on.

## 6. Output format

### Resolved inputs
One line: fidelity, intensity, pillars in scope.

### Blockers
Only true blockers. **If there are none, write "None." and mean it.** An empty Blockers
section is a legitimate and valuable outcome.

### Define before build
Grouped by pillar. Each item: the risk, then the specific decision needed.

### Open questions
Three to five targeted questions, only where a real decision is genuinely undefined. Fewer
is better than padded. Skip entirely if nothing is open.

### Holds up well
Name what is specifically sound and why, in one or two lines. Not praise for balance —
this is the signal that the critical sections were selective.

### Assumptions and missing inputs
What was inferred because the artifact could not answer it, and what to share for a
sharper pass.

### Next Make prompt — zip mode only
Minimal, credit-efficient prompt language addressing the blockers, conforming to the
standing rules in `guidelines/Guidelines.md`. Smallest effective change, not a rewrite. Omit this
section entirely when there are no blockers.

## 7. Deliberately out of scope

Do not raise these. They are correct for production and wrong here; raising them buries
real findings in noise.

- Network error states, permission-denied states, timeout handling. Demo data is local
  and deterministic; loading states are intentional simulation, not gaps.
- Production accessibility conformance. Note only a genuine keyboard trap that would
  strand a presenter mid-demo.
- Internationalization and translation-expansion. The demo surface is English.
- Real user uploads and arbitrary user-generated media.
- SEO, analytics instrumentation, cookie and consent handling.

## 8. Hard rules

- Never edit built React code. Output findings and prompt language only.
- Never invent a finding to fill a section. Volume is not value.
- Never assert a defect the artifact cannot evidence. Say what is unknown instead.
- Attribute severity to demo consequence, not to general engineering purity.
- Name specific elements, screens, and components. "The card layout is fragile" is
  unusable; "the featured-program card sizes to a two-line title and the third slot has
  no defined empty state" is actionable.

```

