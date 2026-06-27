---
contributor: Michael Lo Sasso
team: Not Skynet
type: skill
name: product-problem-brief
filename: product-problem-brief.md
submitted: 2026-06-27
---

# product-problem-brief — product-problem-brief.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** skill

## Description

# `/product-problem-brief` — Claude Code skill

Turns a messy PM **input packet** (notes, customer/field quotes, support snippets, meeting notes, or a rough idea) into a **product problem brief** as a single self-contained HTML report you can open in a browser and hand to a designer or prototyper. It's topic-agnostic — point it at any packet.

## Install (pick one)

You're given one file: `product-problem-brief.md`.

- **Personal (works in every project):** save it to `~/.claude/commands/product-problem-brief.md`
- **One project only:** save it to that project's `.claude/commands/product-problem-brief.md`

That's it — no dependencies, no secrets, no setup. Restart Claude Code if it doesn't appear, then type `/` to confirm `/product-problem-brief` is listed.

## Use it

```
/product-problem-brief                                # it asks which packet to use
/product-problem-brief path/to/your-packet.md         # runs on that packet
/product-problem-brief Surgery Care path/to/packet.md  # optional topic label + packet
```

**You bring the packet.** It can be a markdown/text file or pasted text — however messy. After you give it the packet, it will **ask if there's anything beyond the file** — screenshots/mockups (image paths) or links (Figma frames, Gong clips, Confluence, tickets). Screenshots get embedded and cited as evidence; links are recorded as source references (it won't try to open anything login-gated). The skill only reports what your inputs support; anything unverified (e.g. an unconfirmed quote) is moved to "Open questions," not stated as fact.

## What you get

An HTML file saved to `briefs/product-problem-brief-<topic>-<date>.html` in whatever folder you ran it from, with these sections:

1. Problem statement
2. Target user & context
3. Current pain & evidence (each point cited back to your inputs)
4. Goal & success criteria
5. **Solution direction & MVP slice to prototype** (the buildable next-step target)
6. Out of scope & constraints
7. Open questions & assumptions to validate
8. Source references (links + screenshots used, when provided)

## Guardrails

The skill writes **one local HTML file and nothing else**. It never posts, sends, commits, pushes, or publishes anything, and it won't edit your source code. Sharing the report anywhere is always your manual step.


## File Contents

```
---
description: Product problem brief — turn a messy PM input packet (notes, quotes, support/meeting snippets, a rough idea) plus any screenshots/links into a self-contained HTML brief ready to prototype from (never auto-publishes)
argument-hint: "[topic label + packet path(s), optional]"
---
Turn a messy PM **input packet** into a **product problem brief** as a single self-contained HTML report — the kind a designer or Figma Make can prototype from next. Reusable across topics: it is driven entirely by the inputs you point it at, not hardcoded to any product area.

## 1. Resolve inputs (ask only for what's missing)
- **`$ARGUMENTS` may contain a packet file path, a topic label, or both** — e.g. `/product-problem-brief Find Care briefs/_packets/find-care-packet.md`. Parse both out of it; a token that looks like a path is the packet.
- **Input packet:** the file path from `$ARGUMENTS`, one or more files the user points to, or pasted text — any mix of notes, customer/field quotes, support snippets, meeting notes, or a rough idea. If no packet is given, **ask for the path or text** — do not invent the source.
- **Topic label:** from `$ARGUMENTS` if given; otherwise derive a short label from the packet's title/first lines, or ask.
- **Additional materials — always ask** (unless the user already supplied them): once you have the packet, ask whether there's anything *beyond the markdown file* to factor in. Specifically prompt for:
  - **Screenshots / mockups** (image file paths) — read them and use what they actually show as evidence; cite them. Embed any referenced image inline as base64 so the report stays a single self-contained file.
  - **Links** (Figma frames, Gong clips, Confluence pages, tickets, or public URLs) — record them as source references. Do NOT try to fetch auth-gated URLs (Figma/Gong/Confluence/Jira); cite them by label. Fetch a public URL only if it adds grounding.
  - **Other docs** — treat as additional packet input.
  - If the user says there's nothing else, proceed with the packet alone.

## 2. Extract facts, drop unsupported claims
- Every factual claim in the brief must trace to a line in the packet, a supplied screenshot, or a cited link. Tag it.
- Unverified quotes, hearsay, or "we think" statements are NOT facts — move them to **Open questions & assumptions to validate**, not the problem statement or evidence.
- Distinguish what the inputs *say* from what you infer. Don't smuggle in product opinions the inputs don't support.

## 3. Build the brief (prototype-oriented sections)
Write ONE self-contained `.html` file (all CSS inline in a `<style>` block, no external assets, no JS required; any images embedded as base64). The brief looks FORWARD (what to build), not backward. Sections in order:
1. **Header** — topic label, date, and every input used (packet file, screenshots, links).
2. **Problem statement** — 1–2 sentences a stakeholder and a prototyper both understand.
3. **Target user & context** — who has this problem, and when/where in their journey.
4. **Current pain & evidence** — what's broken today; each point carries a source tag back to the packet/screenshot/link. Weave in supplied screenshots here as cited (inline) evidence.
5. **Goal & success criteria** — what "better" looks like; make it observable where the inputs support it.
6. **Solution direction & MVP slice to prototype** — the bounded, buildable target for the next step. THIS is the section the prototype is built from — be concrete about the slice (which screen/flow, what's in, what's deferred).
7. **Out of scope & constraints** — what this explicitly does not cover; known technical/design constraints from the inputs.
8. **Open questions & assumptions to validate** — unresolved decisions, unverified quotes, things to confirm before/while prototyping.

If screenshots or links were provided, also include a compact **Source references** block (in the header or just before Open questions) listing every link by label and screenshot used.

Styling: system font stack, generous whitespace, one accent (`#5B2A86`), subtle card borders, muted source-tag chips, print-friendly. Make the MVP-slice section visually prominent — it's the handoff.

## 4. Save & report
- Save to `briefs/product-problem-brief-<topic-slug>-<YYYY-MM-DD>.html` relative to the cwd (create `briefs/` if missing). Slugify the topic.
- Print the **absolute path** and note it's intended as the next-step (prototype) input. Offer to open it in a browser preview; do not open or share without being asked.

## Guardrails (hard rules)
- **Never** post, send, email, commit, push, or publish the brief or its contents.
- Only file write permitted is the single HTML brief (and `briefs/` if it must be created). Do not edit product source.
- If the inputs are thin or contradictory, say so in Open questions rather than padding the brief with invented detail.

```

## Notes

Can also be made into a Command, for invocation with optional parameters.
