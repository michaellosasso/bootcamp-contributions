---
contributor: Michael Lo Sasso
team: Not Skynet
type: command
name: Product Problem Brief
filename: problem-brief-README.md
submitted: 2026-06-29
---

# Product Problem Brief — problem-brief-README.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** command

## Description

Turns a messy PM **input packet** (notes, customer/field quotes, support snippets, meeting notes, or a rough idea) into a **product problem brief** as a single self-contained HTML report you can open in a browser and hand to a designer or prototyper. It's topic-agnostic — point it at any packet.

## File Contents

```
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

```

## Notes

Use Claude to prepare input packet; run /product-problem-brief as slash command, point to brief and any other useful artifacts, and view output
