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

Stress-tests designs, specs, and screens built for the Transcarent React clickable demo framework against presenter configuration, live-demo flow integrity, content volatility, component and token drift, and brand-template conformance. Use when a Figma frame or link, screenshot, written spec, PR, or component from the demo framework is shared and the request is a design review, critique, buildability or feasibility check, edge-case pass, pre-build check, or an ask to "grill" a design. Do not use for reviews of the production member-facing app.

## File Contents

```
---
name: demo-design-stress-test
description: Stress-tests designs, specs, and screens built for the Transcarent React clickable demo framework against presenter configuration, live-demo flow integrity, content volatility, component and token drift, and brand-template conformance. Use when a Figma frame or link, screenshot, written spec, PR, or component from the demo framework is shared and the request is a design review, critique, buildability or feasibility check, edge-case pass, pre-build check, or an ask to "grill" a design. Do not use for reviews of the production member-facing app.
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
| `artifact_fidelity` | Detect from what was shared: Figma link, static image, written spec, or code/PR | Detect; never assume code access |
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

Never assert a runtime defect (leak, thrash, re-render storm) from a design artifact.

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

### D. Component and token drift
- Is this a genuinely new component, or a near-variant of something already in the
  framework? Name the existing component if one exists.
- Can it be built from existing tokens and primitives, or does it require bespoke CSS
  that no one will maintain?
- Does it duplicate a pattern that appears elsewhere with slightly different spacing,
  radius, or type scale? Divergence here compounds fast across demo screens.

### E. Brand and template conformance
- Type, color, spacing, and logo treatment against the current Transcarent brand system.
- Does anything read as placeholder, stock, or off-brand in a way a client would notice
  on a shared screen?

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

### Assumptions andmissing inputs
What was inferred because the artifact could not answer it, and what to share for a
sharper pass.

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

- Never invent a finding to fill a section. Volume is not value.
- Never assert a defect the artifact cannot evidence. Say what is unknown instead.
- Attribute severity to demo consequence, not to general engineering purity.
- Name specific elements, screens, and components. "The card layout is fragile" is
  unusable; "the featured-program card sizes to a two-line title and the third slot has
  no defined empty state" is actionable.

```

