---
contributor: Clara
team: LLM Cool J
type: skill
name: /writing-review
filename: SKILL.md
submitted: 2026-06-29
---

# /writing-review — SKILL.md

**Contributor:** Clara | **Team:** LLM Cool J
**Type:** skill

## Description

writing review to eliminate Claud's strange writing style. Meant to used with a hook called "Writing review" where the trigger is the user (me) working on the output for a shareable document, for example confluence documentation. The subagent then checks the output against my style rules automatically. 


## File Contents

```
---
name: writing-review
description: Clean and tighten a written DELIVERABLE that Claude produced at the user's request (research write-ups, Confluence documentation, summaries, specs, notes). Applies house style (no em dashes, no "actually/genuinely", plain concise language, no camel case) and returns the result in paste-safe formatting for Confluence or Figma. Do NOT use on Care Assistant mock responses, member utterances or member-facing copy, or the user's own writing.
---

# Writing review

Take a written deliverable Claude generated for the user and return it cleaned to house style and ready to paste into Confluence or Figma. This fixes and returns the corrected text. It is not a critique-only report.

## Use this on
- Research write-ups and analysis Claude produced
- Confluence-bound documentation and summaries
- Utilitarian docs Claude produced (specs, catalogs, notes)

## Do NOT use this on
- Care Assistant mock responses or suggested-response copy (those follow the Inform response rules, not this skill)
- Member utterances or any member-facing message content
- The user's own writing. This cleans Claude's output, it does not proofread the user.

## Rules to apply
- Remove every em dash. Use a comma, period, parentheses, or a colon instead.
- Never use "actually" or "genuinely." Cut filler intensifiers.
- Plain language. No jargon. If a technical term is unavoidable, translate it.
- Concise. Cut wordiness, throat-clearing, and hedging. Short sentences. Say it once.
- Never use camel case.
- Keep the meaning and the facts intact. Tighten, do not water down.

## Paste-safe formatting
The output must keep its formatting when copied from the chat preview and pasted into Confluence, Figma, or a similar surface.
- Use literal line breaks, with a blank line between paragraphs.
- Use simple structure only: plain headings, hyphen bullets, numbered lists.
- Avoid anything that breaks on paste: tables, blockquotes, vertical-bar formatting, nested or exotic markdown, and em dashes.
- If the target is Figma or another plain-text surface, present the text so the raw line breaks copy through cleanly, as plain text the user can copy verbatim.

## Output
Return the cleaned deliverable, ready to paste. Below it, add a short note listing what changed, for example "removed 4 em dashes, cut 3 filler phrases, flattened a table to a list." Keep the note brief.

```

