---
contributor: Michael Lo Sasso
team: Not Skynet
type: skill
name: Technical Issue Breakdown
filename: Technical Issue Breakdown.md
submitted: 2026-07-20
---

# Technical Issue Breakdown — Technical Issue Breakdown.md

**Contributor:** Michael Lo Sasso | **Team:** Not Skynet
**Type:** skill

## Description

Translate high-level product feature ideas and design mockups into micro-scoped, actionable development tasks that software engineers can pick up instantly.

## File Contents

```
# Skill: Technical Issue Breakdown
## Triggers: "create tickets", "break this down", "to issues", "generate tasks"

## Purpose
Translate high-level product feature ideas and design mockups into micro-scoped, actionable development tasks that software engineers can pick up instantly.

## Execution Pipeline
1. **Analyze Requirements:** Review the provided PRD or feature brief. Identify the frontend layer, backend API modifications, and database schema changes required.
2. **Isolate Dependency Chains:** Order the tasks logically (e.g., Database migrations -> API endpoints -> Frontend UI).
3. **Draft the Issue:** For each task, output a structured Markdown template containing:
   - **Context:** Why we are building this.
   - **Technical Approach:** Hints for the engineer (endpoints to touch, data schemas to modify).
   - **Acceptance Criteria (Gherkin format):** Given/When/Then scenarios.
   - **Definition of Done:** Testing and compliance steps.

## Output Format
Return a series of distinct Markdown blocks labeled `[TICKET-XX]: Title` ready to be copied into Jira, GitHub Issues, or Azure DevOps.

```

