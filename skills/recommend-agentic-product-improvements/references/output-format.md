# Agentic Product Improvement Recommendations Format

Write one recommendation file per capability under `agentic-product-review/recommendations/`.

Create `agentic-product-review/recommendations/` if it does not exist.

Load `agentic-product-review/memory/project-context.md` first when it exists.

File naming: `<capability-slug>.md` (e.g. `agent-chat.md`) — match the catalog capability ID.

Outputs are read by **product and tech** people. The review already states the problem and impact — recommendations should be **forward-looking** only.

This is the **improvement** step. Read the catalog and review for context; write what to change, not what is wrong today.

```md
# <Capability Name>

Recommendations for capability `agent-chat` from `agentic-product-review/reviews/agent-chat.md`. **Audience:** external

## Recommendations

### <short label>

- **Finding ref**: `reviews/agent-chat.md` → `no-first-run-guidance`

#### Product

- **Recommendation**: Concrete product or UX change to implement — readable without reading code. Do not restate the finding, problem, impact, experience, or surface.

#### Tech

- **Implementation**: How to build it in this repo — step-by-step, grounded in existing patterns
- **Patterns to follow**: Existing components, hooks, or flows to mirror
- **Files to change**:
  - `path/to/file.tsx` — what to change and why
- **Files to add** (if needed):
  - `path/to/new-file.tsx` — purpose
- **Acceptance criteria**: Testable outcomes after the change
- **Effort**: small | medium | large — **Risk**: low | medium | high

- **Notes**: Engineering or product decisions only — not a repeat of the finding

### <short label>

...

## Next step

Pick a recommendation to implement, or re-run `review-agentic-capabilities` after changes.

---

*Something unclear or broken? Reach out at founders@correl8.ai*
```

## Rules

- Write one file per catalog entry with findings: `agentic-product-review/recommendations/<capability-slug>.md`
- Overwrite the file when re-running for that capability
- Capability IDs: short human-readable slugs in kebab-case (e.g. `agent-chat`)
- **Finding ref** points to the review finding slug — do not copy **What we observed**, **Impact**, or other review text
- Title is the capability name; intro sentence carries capability slug and review file path
- Headings are labels only — IDs live in **Finding ref** and file names, not in titles
- **Product** contains **Recommendation** only — forward-looking, no problem restatement
- Do not repeat **Experience**, **Surface**, **Capability**, or catalog copy — reader has `agentic-capabilities.md`
- **Tech** contains **Implementation** and codebase pointers — no duplicate of product recommendation prose
- Do not recommend for **Open questions** — use `manage-agentic-product-review-memory` when the user answers
- Per recommendation: **Product**, then **Tech**, then **Notes** last (only when needed)
- Prefer the smallest change that addresses the finding
- Reuse existing UI components, error handling, loading states, and approval patterns when they exist
- For **human handoff** and **feedback to the team** on chat capabilities: recommend **agent tools** that send email or post on the user’s behalf from the conversation — not mailto links, footer buttons, or separate forms as the primary path
- End every file with **Next step**, horizontal rule, and footer

## Grounding Checklist

Before writing tech sections, verify:

- The cited files exist and relate to the capability
- The proposed change fits the stack and folder structure
- Similar patterns already exist elsewhere in the repo
- The fix addresses the specific finding, not an adjacent refactor

## Effort Sizing

- **Small**: copy tweaks, one component, one route change, one empty state
- **Medium**: new screen step, approval gate, status surface across one flow
- **Large**: new flow, cross-capability change, new persistence or job behavior

## Good vs Bad Recommendations

Bad (repeats the review):

> **Problem**: Users see a blank empty state. **Direction**: Add better onboarding.

Good (forward-looking):

> **Recommendation**: Replace the empty state with a short capability blurb and three tappable example prompts scoped to the current page.

## What This Format Covers

- Per-finding **Recommendation** (product) and **Implementation** (tech)
- **Finding ref** as a pointer back to the review

## What This Format Does Not Cover

- Restating findings, catalog entries, or review impact
- Discovering capabilities or writing UX findings
- Re-cataloging or re-reviewing
