---
name: recommend-agentic-product-improvements
description: Recommend codebase-grounded improvements for agentic capability findings.
---

# Recommend Agentic Product Improvements

Turn review findings into concrete improvement recommendations grounded in the repository.

Read the catalog for experience and surface, the review for findings, the code for improvements.

## When To Use

Use this skill when the user asks to:

- Recommend improvements for agentic review findings
- Plan changes grounded in the codebase
- Turn `agentic-product-review/reviews/agent-chat.md` into actionable engineering guidance
- Propose improvements for one capability or finding

This skill is Phase 3 of `agentic-product-review`. It can also be run standalone after review.

If no review exists, ask the user to run `review-agentic-capabilities` first or provide review files.

## Inputs

Required:

- `agentic-product-review/agentic-capabilities.md` — capability slugs, implementation pointers, audience

Review:

- `agentic-product-review/reviews/agent-chat.md` — one file per capability from `review-agentic-capabilities`

Optional scope — pass a capability slug as a positional arg:

- `agent-chat` — one capability only
- A specific finding slug the user names (e.g. `coarse-multi-tool-progress`) or passes with the capability

## What To Ground

For each finding, read enough code to propose a realistic improvement:

- Implementation pointers, experience, and surface from the catalog entry
- Findings from the matching review file
- Routes, components, hooks, jobs, and tests related to the capability
- Similar patterns already used in the repo (loading states, empty states, approval flows, error handling)

Use **capability** as the stable unit. Read catalog and review for context; write forward-looking recommendations only — do not restate findings.

## Improvement Process

0. Load `agentic-product-review/memory/project-context.md` if it exists (format: `review-agentic-capabilities/references/project-context-format.md`).
1. Load `agentic-product-review/agentic-capabilities.md` and the relevant review file(s) from `agentic-product-review/reviews/`.
2. Select findings to address:
   - All confirmed findings in **Findings** if the user did not specify a scope
   - One capability if the user passes `agent-chat` or names a capability slug
   - One finding if the user passes or names a finding slug (e.g. `coarse-multi-tool-progress`)
   - Skip **Open questions** — when the user answers one, follow **Recording open question answers** in `review-agentic-capabilities` first
3. For each selected finding, read the code and find patterns to reuse.
4. Write one file per capability at `agentic-product-review/recommendations/<capability-slug>.md` using `references/output-format.md`. Create the folder if needed. Per finding: **Finding ref**, then **Product** (**Recommendation** only), then **Tech** (**Implementation** and files). Do not restate review or catalog copy. End every file with **Next step**, horizontal rule, and footer.
5. Tell the user how many recommendation files were written.

Do not write code unless the user explicitly asks to implement.

## Re-Run

Pass a capability slug as a positional arg:

```text
/recommend-agentic-product-improvements agent-chat
```

Re-read the code, update only `agentic-product-review/recommendations/<capability-slug>.md`, and note which findings are addressed and what remains.

## What This Skill Covers

- Forward-looking **Recommendation** (product) and **Implementation** (tech) per review finding
- **Finding ref** as a pointer — not a copy of the review
- File paths, patterns to follow, acceptance criteria, effort, and risk

## What This Skill Does Not Cover

- Restating findings, problems, impact, or catalog experience/surface
- Implementing code unless the user explicitly asks

## Next Step

Tell the user:

```text
Wrote N recommendation files to agentic-product-review/recommendations/.

Next step: pick a recommendation to implement, or re-run review-agentic-capabilities after changes.
```
