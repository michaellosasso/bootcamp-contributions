---
contributor: Michael Lo Sasso
team: Not Skynet
type: other
name: find-care-route-to-care-packet.md
filename: context-management-one-pager2.md
submitted: 2026-06-27
---

# find-care-route-to-care-packet.md — context-management-one-pager2.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** other

## Description

Packet for product problem brief command

## File Contents

```
# Working with Claude: Managing Context

*Product & Design AI Uplevel Workshop*
*Michael Lo Sasso — [date]*

---

How much Claude remembers between sessions depends on which product you're in — and the answer is different for each one.

**Claude Chat** (the browser or app) generates memory summaries from your past conversations and surfaces them in future ones. It's on by default and can be managed in Settings. It's not a live feed of prior chats — it's AI-generated context, and it only covers what's been summarized from your history.

**Claude Cowork** is a project and folder-driven environment where Claude has a native tool to retrieve past sessions within that same environment. More persistent than Chat, but still scoped to Cowork.

**Claude Code** (the terminal agent) has no cross-session memory by default. Close a session and you start from zero — unless you've deliberately written something somewhere it can find again.

For most people on the team, Claude Code is where the context problem bites hardest. The rest of this page focuses there.

---

## The short version

There are three Claude products most of us use: Claude Chat, Cowork, and Claude Code. They each handle context differently, but Claude Code is where deliberate context management matters most — and where this guide focuses.

**In Claude Code**, the main tool is a file called `CLAUDE.md` — a plain text file that loads automatically at the start of every session. Put your role, your preferences, your project rules there, and you don't have to re-explain yourself every time.

**In claude.ai**, the equivalent is a **Project** with instructions. Same idea — set it once, and every conversation in that project starts in the right context.

If you're doing work in both places (and most of us are), a shared reference document — a `context.md` in a private repo, synced to Confluence — keeps the two in sync without maintaining two separate sources of truth.

---

## Why it matters for the team

The more elaborate your workflow, the more this matters. But even for straightforward use:

- A rubric or eval you type into a chat is gone when the chat closes. Baked into a command, it runs the same way every time.
- Context you re-explain in every session is wasted effort. Written down once, it's available everywhere.
- Work you build alone stays with you. Structured as a shared command or skill, it's available to the team.

The gap between a useful personal tool and a reusable team asset is mostly about whether you wrote the context down.

---

## Want the full picture?

The detailed reference — covering CLAUDE.md structure, persistence layers, the claude.ai Project setup, cross-environment portability, and a proposed governance model for shared resources — is here:

→ **[Claude Context Management & AI Resource Governance](#)** *(link once published)*

Questions or additions: ping Michael Lo Sasso in Slack.

```

## Notes

Just a test
