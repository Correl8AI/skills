---
name: manage-agentic-product-review-memory
description: Record answers to review open questions in project context for agentic product review.
---

# Manage Agentic Product Review Memory

Record user answers to **Open questions** from capability reviews. Update `project-context.md` so discovery, review, and recommendation skills can use resolved intent.

## When To Use

Use this skill when the user:

- Answers an open question from a capability review
- Clarifies whether a reviewed behavior is intentional
- Wants project context updated after a product decision

## Inputs

Required:

- The user's answer (in the message or a follow-up)
- Which open question — pass `background-agent-tasks/no-direct-task-creation-ui` as a positional arg, or name the capability slug and question slug

Load before writing:

- `agentic-product-review/memory/project-context.md`
- The matching review: `agentic-product-review/reviews/<capability-slug>.md`

## Process

1. Load `agentic-product-review/memory/project-context.md`. Create `agentic-product-review/memory/` and the starter file from `references/output-format.md` if missing.
2. Locate the open question in the review file by slug under **Open questions**.
3. Update `agentic-product-review/memory/project-context.md` — add or extend the capability section with a short distilled bullet from the answer.
4. Remove the answered entry from **Open questions** in the review file. Re-read the review; if the answer confirms a real UX problem, add a **Findings** entry instead. If it confirms intentional design, leave it out of findings.
5. Tell the user which files were updated.

Do not implement code unless the user explicitly asks.

## What This Skill Covers

- Persisting answered intent in `project-context.md`
- Removing resolved open questions from reviews

## What This Skill Does Not Cover

- Writing new reviews or findings — use `review-agentic-capabilities`
- Recommendations — use `recommend-agentic-product-improvements`

## Next Step

Tell the user:

```text
Recorded answer for background-agent-tasks/no-direct-task-creation-ui.

Updated:
- agentic-product-review/memory/project-context.md
- agentic-product-review/reviews/background-agent-tasks.md
```
