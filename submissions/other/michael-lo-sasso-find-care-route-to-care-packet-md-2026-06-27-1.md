---
contributor: Michael Lo Sasso
team: Not Skynet
type: other
name: find-care-route-to-care-packet.md
filename: find-care-route-to-care-packet.md
submitted: 2026-06-27
---

# find-care-route-to-care-packet.md — find-care-route-to-care-packet.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** other

## Description

Packet for product problem brief command

## File Contents

```
# Input packet — Find Care: route results into care (Transcarent member portal)

> **Framing — read first.** A member product problem in the Transcarent member portal; the `transcarent-member` app is the prototyping substrate. Evidence is real and **triangulated**: member call analysis (Gong) + internal product/UX/analytics/incident docs (Glean). **Internal/confidential — keep in the local brief only.** The rough idea below is the chosen Day-2 prototype direction (one of five evidenced Find Care problems); the others are context, deferred.

## Rough idea (one-liner)
Find Care is a directory, not a path to care: a member who finds a provider can't easily take the next step. Connect Find Care results into a care action — primarily the care navigator ("health guide") — so members actually get to care instead of dropping out.

## The problem (member-facing)
Find Care returns a list of providers but offers little help acting on it. There is no in-app route from a result into care; the member self-serves or falls back to a phone call / human. The product's own strategy frames the fix as moving Find Care from a "passive provider directory" to an "intelligent care navigation system."

## Evidence — triangulated across two independent sources

**Member calls (Gong):**
- Self-service vs. human: members still need/prefer human help for complex or sensitive issues; the app's safety valve is literally "connect with your health guide." [Gong · issue 3]
- Provider-search gaps appear too (only a few results; couldn't find a specific surgeon in an area) — upstream of, and compounding, the dead-end. [Gong · issue 2]

**Product / UX / analytics / incident docs (Glean):**
- Member quote: "This tool (find care) is really hard to use… nothing tells me which provider is better for me." [Glean · 4]
- Client expectation: "FindCare needs stronger provider steerage toward quality… actively guiding them to the best option, not just an eligible one." [Glean · 4]
- Strategy: transform Find Care from "passive provider directory" → "intelligent care navigation system that proactively guides members," with NPS/CSAT as success. [Glean · 4]
- Chat/directory disconnect: the Care Assistant can't perform Find Care/coverage requests and redirects to the self-service tool, breaking the journey; one member couldn't find the in-network doctor list after a chat handoff. [Glean · 4]
- Conversion drop-off, search → visit: a 2025 campaign saw 0.6% register → 0.22% book → 0.155% complete a visit; ~20k members/mo use Find Care but ~12/mo click the PlushCare tile (~0.05%) and ~3/mo complete a virtual visit. [Glean · 4]

**Convergence:** both independent sources land on the same gap — results don't route members into care, and humans/navigators are the fallback.

## Build substrate (the member app)
- `transcarent-member` — consumer portal. `/find-care` is a single screen: search + specialty chips + result count + provider cards. The only per-result action is a `tel:` phone link. [`FindCare.tsx`]
- A care-navigator chat already exists at `/care` (navigator "Sarah Mitchell") — the natural "connect with your health guide" destination — but Find Care does not link to it. [`App.tsx`, `memberData.ts`]
- Seeded member: James Hartwell (TC-100001), Austin TX. Providers carry specialty / network / rating / distance / accepting.

## Adjacent problems (context — NOT this slice)
Search robustness/taxonomy, discoverability/wayfinding, network accuracy, performance/reliability. All evidenced in the Glean + Gong analyses; deferred so the slice stays small.

## Constraints
- Bootcamp prototype, not production. Local mock data only.
- Build on `transcarent-member`; reuse its components + the existing `/care` chat. No new backend.

## Open questions
- Which care action is the route: navigator chat (exists today), a video visit, or scheduling?
- What context should transfer into the chat (provider name/specialty)? New thread vs. existing?
- Evidence is real, but the member app is a simplified substrate — the slice demonstrates the direction, not production behavior.

## Sources
- Gong call analysis — member-standpoint top issues, Find Care focus.
- Glean analysis — UX research, analytics, incident reports, product strategy docs.
- Internal/confidential — local brief only; do not publish or share externally.

```

## Notes

Just a test
