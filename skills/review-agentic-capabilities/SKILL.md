---
name: review-agentic-capabilities
description: Review each agentic capability from a discovery catalog and write per-capability findings in Markdown.
---

# Review Agentic Capabilities

Review every capability in the discovery catalog from a **product and user-experience** perspective.

Read the code to understand behavior, but write findings in plain language — no file paths or implementation detail in the output.

Requires a discovery catalog. Each review file references its catalog entry.

## When To Use

Use this skill when the user asks to:

- Review discovered agentic capabilities
- Audit each agent flow in the repo
- Evaluate agents after a discovery pass
- Produce per-capability findings from the capabilities catalog

If no catalog exists, ask the user to run `discover-agentic-capabilities` first or provide a catalog path.

## Input

Default input: `agentic-product-review/agentic-capabilities.md`

Read each catalog entry by capability slug (e.g. `agent-chat`) and the implementation pointers listed for it.

## Rubric

Pick **one** rubric from **Experience** and **Surface**:

| Interaction | Rubric file |
|---|---|
| User talks to the agent (chat, copilot, assistant UI) | `references/review-rubric-conversational.md` |
| User only sees queue, status, results, errors | `references/review-rubric-headless.md` |

**Headless test:** No chat thread → headless rubric.

Read **Audience** from the catalog; use the audience guidance at the top of the chosen rubric to decide which sections apply.

## What To Review

For each capability, read enough code to understand what people actually experience:

- Routes, handlers, jobs, and UI that expose the capability
- Onboarding, empty states, and first-run flows (conversational)
- Progress, loading, and status visibility
- Error handling and recovery paths
- Approval gates, permissions, and human-in-the-loop steps
- Output review, editing, and confirmation flows

## Review Process

1. Load `agentic-product-review/memory/project-context.md` if it exists.
2. Load the capabilities catalog.
3. Review each capability one by one — do not skip entries unless the user passes a capability ID.
4. Choose `review-rubric-conversational.md` or `review-rubric-headless.md`; read **Audience** from the catalog and apply matching sections.
5. Write one file per capability at `agentic-product-review/reviews/<capability-slug>.md` (e.g. `agent-chat.md`) using `references/output-format.md`. Create the folder if needed. Per file: capability name as title, intro sentence, then **What works**, **Findings**, **Open questions**, **Notes** — each a top-level `##` section. End every file with **Next step**, horizontal rule, and footer.
6. Tell the user how many review files were written.

If the catalog is empty or stale, say so and suggest re-running discovery.

## Recording open question answers

When the user answers an open question from a review — in conversation, without naming a workflow — update memory inline. Do not describe this as a separate skill or command.

Required inputs:

- The user's answer (in the message or a follow-up)
- Which open question — capability slug and question slug (e.g. `background-agent-tasks` / `auto-tasks-no-user-context`)

Process:

1. Load `agentic-product-review/memory/project-context.md`. Create `agentic-product-review/memory/` and the starter file from `references/project-context-format.md` if missing.
2. Load the matching review: `agentic-product-review/reviews/<capability-slug>.md`. Locate the open question by slug under **Open questions**.
3. Update `agentic-product-review/memory/project-context.md` — add or extend the capability section with a short distilled bullet from the answer.
4. Remove the answered entry from **Open questions** in the review file. Re-read the review; if the answer confirms a real UX problem, add a **Findings** entry instead. If it confirms intentional design, leave it out of findings.
5. Tell the user which files were updated (paths only — no workflow jargon).

Example user message:

```text
Recorded answer for background-agent-tasks/auto-tasks-no-user-context.

Updated:
- agentic-product-review/memory/project-context.md
- agentic-product-review/reviews/background-agent-tasks.md
```

## Focused Re-Review

Pass a capability ID as a positional arg:

```text
/review-agentic-capabilities background-agent-tasks
```

Update only `agentic-product-review/reviews/<capability-slug>.md`. Note what improved, what remains, and any new risks.

Do not implement code unless the user explicitly asks.

## What This Skill Covers

- Whether each capability works well for its users
- **What works** — what people can rely on today
- **Findings** — confirmed UX problems with stable slugs (e.g. `no-first-run-guidance`), what was observed, and impact (no recommendations)
- **Open questions** — behaviors that may be intentional, each with a slug ID, **What we observed**, and **Question**
- **Assessment** — strong, acceptable, weak, or incomplete (on the intro line)
- Review-specific caveats in **Notes**

## What This Skill Does Not Cover

- Cataloging what exists — that is `discover-agentic-capabilities`
- Repeating **Capability**, **Experience**, or **Surface** — the intro sentence and catalog cover identity
- Structural facts already in the catalog (HITL, tools, scope)
- Recording open question answers — see **Recording open question answers** above

## Next Step

Tell the user:

```text
Reviewed N capabilities. Output written to agentic-product-review/reviews/.

Next step: run recommend-agentic-product-improvements to turn findings into codebase-grounded recommendations.
```
