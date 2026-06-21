---

## name: review-agentic-capabilities

description: Review each agentic capability from a discovery catalog and write per-capability findings in Markdown.

# Review Agentic Capabilities

Review every capability in the discovery catalog from a **product and user-experience** perspective.

Read the code to understand behavior, but write findings in plain language — no file paths or implementation detail in the output.

Requires a discovery catalog. Each review file references its catalog entry.

## When To Use

Use this skill when the user asks to:

- Review discovered agentic capabilities
- Audit each agent flow in the repo
- Evaluate internal and external agents after a discovery pass
- Produce per-capability findings from the capabilities catalog

If no catalog exists, ask the user to run `discover-agentic-capabilities` first or provide a catalog path.

## Input

Default input: `agentic-product-review/agentic-capabilities.md`

Read each catalog entry by capability slug (e.g. `agent-chat`) and the implementation pointers listed for it.

## What To Review

For each capability, read enough code to understand what users and operators actually experience:

- Routes, handlers, jobs, and UI that expose the capability
- Onboarding, empty states, and first-run flows
- Progress, loading, and status visibility
- Error handling and recovery paths
- Approval gates, permissions, and human-in-the-loop steps
- Output review, editing, and confirmation flows

Apply `references/review-rubric.md` based on each capability's audience. Use **capability** as the stable unit.

## Review Process

1. Load `agentic-product-review/memory/project-context.md` if it exists.
2. Load the capabilities catalog.
3. Review each capability one by one — do not skip entries unless the user passes a capability ID.
4. Apply the rubric for that capability's audience.
5. Write one file per capability at `agentic-product-review/reviews/<capability-slug>.md` (e.g. `agent-chat.md`) using `references/output-format.md`. Create the folder if needed. Per file: capability name as title, intro sentence, then **What works**, **Findings**, **Open questions**, **Notes** — each a top-level `##` section. End every file with **Next step**, horizontal rule, and footer.
6. Tell the user how many review files were written.

If the catalog is empty or stale, say so and suggest re-running discovery.

## Answering open questions

When the user answers an open question from a review, use `manage-agentic-product-review-memory` — do not update memory inline.

That skill will:

1. Remove the answered entry from **Open questions** in the review file
2. Update `agentic-product-review/memory/project-context.md` with distilled intent

If the answer confirms a real UX problem, add a **Findings** entry in the review instead of leaving it unresolved.

## Focused Re-Review

Pass a capability ID as a positional arg:

```text
/review-agentic-capabilities background-agent-tasks
```

Update only `agentic-product-review/reviews/<capability-slug>.md`. Note what improved, what remains, and any new risks.

Do not implement code unless the user explicitly asks.

## What This Skill Covers

- Whether each capability works well for users and operators
- **What works** — what users can rely on today
- **Findings** — confirmed UX problems with stable slugs (e.g. `no-first-run-guidance`), what was observed, and impact (no recommendations)
- **Open questions** — behaviors that may be intentional, each with a slug ID, **What we observed**, and **Question**
- **Assessment** — strong, acceptable, weak, or incomplete (on the intro line)
- Review-specific caveats in **Notes**

## What This Skill Does Not Cover

- Cataloging what exists — that is `discover-agentic-capabilities`
- Repeating **Capability**, **Experience**, or **Surface** — the intro sentence and catalog cover identity
- Structural facts already in the catalog (HITL, tools, scope)
- Answering open questions — use `manage-agentic-product-review-memory` to remove them from the review and update `project-context.md`

## Next Step

Tell the user:

```text
Reviewed N capabilities. Output written to agentic-product-review/reviews/.

Next step:
- Answer open questions with manage-agentic-product-review-memory
- Run recommend-agentic-product-improvements to turn findings into codebase-grounded recommendations
```

