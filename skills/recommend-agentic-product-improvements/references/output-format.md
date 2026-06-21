# Agentic Product Improvement Recommendations Format

Write one recommendation file per capability under `agentic-product-review/recommendations/`.

Create `agentic-product-review/recommendations/` if it does not exist.

Load `agentic-product-review/memory/project-context.md` first when it exists.

File naming: `<capability-slug>.md` (e.g. `agent-chat.md`) — match the catalog capability ID.

Outputs are read by **product and tech** people. Some readers have a light technical background — write product fields in plain language. Tech sections cite real files and patterns from the repo.

This is the **improvement** step. Experience and surface come from the discovery catalog; problems come from the review. Do not re-catalog or re-review here.

```md
# <Capability Name>

Recommendations for capability `agent-chat` from `agentic-product-review/reviews/agent-chat.md`. **Audience:** external

## Recommendations

### <short label>

- **Finding ref**: `agentic-product-review/reviews/agent-chat.md` → `no-first-run-guidance`

#### Product

- **Experience**: From the catalog — user or operator experience being improved
- **Surface**: From the catalog — where in the product this appears
- **Problem**: From the review finding — what is wrong today, in plain language
- **Impact**: Why this matters for users, operators, or the business
- **Direction**: Concrete product or UX change — readable without reading code

#### Tech

- **Evidence**: Key files only — enough to locate the issue in code, not a full architecture walkthrough
- **Patterns to follow**: Existing components, hooks, or flows in this repo to mirror
- **Files to change**:
  - `path/to/file.tsx` — what to change and why
- **Files to add** (if needed):
  - `path/to/new-file.tsx` — purpose
- **Dependencies**: APIs, state, routes, or jobs touched by this fix
- **Implementation notes**: Step-by-step guidance that matches how this repo is structured
- **Acceptance criteria**: Testable outcomes after the fix
- **Effort**: small | medium | large — **Risk**: low | medium | high

- **Notes**: Open questions or items needing a product or engineering decision

### <short label>

...

## Next step

Pick a recommendation to implement, or re-run `review-agentic-capabilities` after changes.

---

*Something unclear or broken? Reach out at founders@correl8.ai*
```

## Rules

- Write one file per catalog entry with findings: `agentic-product-review/recommendations/<capability-slug>.md` (e.g. `agent-chat.md`)
- Overwrite the file when re-running for that capability
- Capability IDs: short human-readable slugs in kebab-case (e.g. `agent-chat`)
- Finding refs use the finding slug from the review (e.g. `no-first-run-guidance`)
- Title is the capability name; intro sentence carries capability slug and review ref
- Headings are labels only — IDs live in **Finding ref** and file names, not in titles
- **Experience** and **Surface** come from the catalog — not the review
- **Finding ref** must point to a confirmed finding: `<review-file>` → `<finding-slug>` (e.g. `reviews/agent-chat.md` → `coarse-multi-tool-progress`)
- **Problem** and **Impact** come from that review finding
- Do not recommend for **Open questions** — use `manage-agentic-product-review-memory` when the user answers
- Per recommendation: **Product** then **Tech**, then **Notes** last
- **Notes** is shared per recommendation — not duplicated under Product or Tech
- Product section must stand alone — no jargon, no file paths
- Tech section stays focused. Do not dump stack traces, schemas, or implementation plans unrelated to the finding
- Prefer the smallest change that fixes the finding
- Reuse existing UI components, error handling, loading states, and approval patterns when they exist
- Do not invent architecture the repo does not use
- End every file with **Next step**, horizontal rule, and footer:

  ```md
  ## Next step

  Pick a recommendation to implement, or re-run `review-agentic-capabilities` after changes.

  ---

  *Something unclear or broken? Reach out at founders@correl8.ai*
  ```

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

Bad:

> Add better onboarding.

Good:

> Add an `AgentIntro` step before `AgentTaskForm` on `app/routes/agent/new.tsx`, matching the empty-state pattern used in `app/components/DashboardEmptyState.tsx`.

## What This Format Covers

- **Catalog ref**, **Review ref**, and per-finding product + tech recommendations
- Experience and surface from the catalog; problem from the review

## What This Format Does Not Cover

- Discovering capabilities or writing UX findings
- Re-cataloging or re-reviewing
