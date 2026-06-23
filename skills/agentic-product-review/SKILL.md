---
name: agentic-product-review
description: Discover conversational agentic capabilities, review each external one, and write per-capability review files in Markdown.
---

# Agentic Product Review

Run discovery and review of external user-facing **conversational** agent experiences in the repository (chat, copilot, assistant UIs).

This skill always runs two phases:

1. **Discover** — write `agentic-product-review/agentic-capabilities.md`
2. **Review** — write `agentic-product-review/reviews/<capability-slug>.md` for each external or mixed capability

Do not skip discovery. Do not write a separate combined review document. Do not perform a broad product review outside agentic user experiences.

## When To Use

Use this skill when the user asks to:

- Run a full agentic product review
- Review an AI agent experience from an external user's perspective
- Find gaps in external user agentic flows
- Evaluate onboarding, trust, permissions, handoff, or failure states for external user agents

## Scope

**Discovery** catalogs conversational user-facing agent loops only — external, internal, or mixed. Skip background/headless agents (queue and results without a chat thread).

**Review** covers only conversational capabilities marked `external` or `mixed`. Skip pure `internal` capabilities unless the user asks to include them.

Do not review general code quality, architecture, security, or non-agentic UI unless it directly affects an external user agent interaction.

## Process

### Phase 1 — Discover

Load `agentic-product-review/memory/project-context.md` if it exists, then follow `discover-agentic-capabilities`:

1. Scan the repo for agentic signals.
2. Group into distinct capabilities with stable IDs.
3. Write `agentic-product-review/agentic-capabilities.md` using `discover-agentic-capabilities/references/output-format.md`.

If no capabilities qualify, say what was checked and stop.

### Phase 2 — Review

For every catalog entry with audience `external` or `mixed`, follow `review-agentic-capabilities`:

1. Read implementation pointers from the catalog.
2. Apply `review-agentic-capabilities/references/review-rubric-conversational.md`. Read **Audience** from the catalog and apply matching sections.
3. Write one file per capability at `agentic-product-review/reviews/<capability-slug>.md` using `review-agentic-capabilities/references/output-format.md`.

Review every external conversational capability one by one. Do not skip entries unless the user passes a capability slug as a positional arg (e.g. `/agentic-product-review agent-chat`).

Do not implement code unless the user explicitly asks.

## Open question answers

When the user answers an open question from a review, follow **Recording open question answers** in `review-agentic-capabilities`.

## Re-Review

Pass a capability ID as a positional arg to re-review one capability:

```text
/agentic-product-review agent-chat
```

Re-run discovery only if the catalog may be stale. Update only `agentic-product-review/reviews/<capability-slug>.md`.

## What This Skill Covers

- Full discovery catalog of conversational user-facing agent loops
- Per-capability UX review for external and mixed audiences
- Confirmed findings (e.g. `no-first-run-guidance`), open questions, and assessments (no recommendations)

## What This Skill Does Not Cover

- Reviewing pure internal capabilities (unless asked)
- Background or headless agent loops — out of scope for these skills
- Recommendations or codebase-grounded implementation plans — use `recommend-agentic-product-improvements`
- Implementing code unless the user explicitly asks

## Next Step

Tell the user:

```text
Agentic product review complete.

Outputs:
- agentic-product-review/agentic-capabilities.md
- agentic-product-review/reviews/agent-chat.md (one per reviewed capability)

Next step: run recommend-agentic-product-improvements to turn findings into codebase-grounded recommendations.
```
