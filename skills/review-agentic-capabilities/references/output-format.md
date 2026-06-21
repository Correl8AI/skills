# Agentic Capabilities Review Format

Write one review file per capability under `agentic-product-review/reviews/`.

Create `agentic-product-review/reviews/` if it does not exist.

File naming: `<capability-slug>.md` (e.g. `agent-chat.md`) — match the catalog capability ID.

Before writing, load `agentic-product-review/memory/project-context.md` if it exists. Use answered intent to avoid re-raising resolved questions and to inform findings.

Outputs are read by **product and tech** people. Some readers have a light technical background — write product fields in plain language. Keep this document product-focused; codebase-grounded improvement guidance belongs in `recommend-agentic-product-improvements`.

This is the **judgment** step. Reference the discovery catalog — do not re-catalog.

```md
# <Capability Name>

Review of capability `agent-chat` from `agentic-product-review/agentic-capabilities.md`. **Audience:** external · **Assessment:** weak

## What works

What users or operators can rely on today.

## Findings

Confirmed UX problems grounded in what the product does today.

### <short label>

- **ID**: `no-first-run-guidance`
- **What we observed**: What the product actually does today — behavior users see, not file paths
- **Impact**: Why this matters for users, operators, or the business

## Open questions

Behaviors that may be intentional. Do not list these under **Findings**. Use `manage-agentic-product-review-memory` when the user answers.

### <short label>

- **ID**: `failed-tasks-hidden-non-staff`
- **What we observed**: What the product does today — behavior users see, not file paths
- **Question**: What needs human judgment to decide if this is a problem

## Notes

Review-specific caveats only — e.g. could not verify a flow, catalog entry was incomplete. Not structural facts already in the catalog.

## Next step

- Answer open questions with `manage-agentic-product-review-memory`
- Run `recommend-agentic-product-improvements` to turn findings into codebase-grounded recommendations

---

*Something unclear or broken? Reach out at founders@correl8.ai*
```

## Rules

- Write one file per catalog entry: `agentic-product-review/reviews/<capability-slug>.md` (e.g. `agent-chat.md`)
- Load `agentic-product-review/memory/project-context.md` first when it exists
- Overwrite the file when re-reviewing that capability
- **Catalog ref** must point to the matching entry in `agentic-product-review/agentic-capabilities.md`
- General fields come first: title, intro sentence, then **What works**, **Findings**, **Open questions**, **Notes** — all as `##` sections
- Do not repeat **ID** or **Catalog ref** as separate bullets — the intro sentence covers both
- **What works** — top-level `##` section after the intro; plain prose, no bullet label
- Capability IDs: short human-readable slugs in kebab-case, matching the catalog (e.g. `agent-chat`)
- Finding and open-question IDs: short human-readable slugs in kebab-case, derived from the entry label (e.g. `no-first-run-guidance`, `failed-tasks-hidden-non-staff`)
- Slugs must be unique within each review file
- Headings are labels only — put IDs in the **ID** field, never in titles or `###` headings
- **Findings** — only confirmed problems. Each entry has **What we observed** and **Impact**
- **Open questions** — may-be-intentional behaviors. Each entry has **What we observed** and **Question** — not **Impact**
- Do not duplicate an open question under **Findings**
- Skip open questions already answered in `project-context.md`
- Do not repeat **Experience** or **Surface** — readers get those from the catalog
- **Notes** is a top-level `##` section
- Write in plain language — a product reader should not need any tech detail
- Do not recommend fixes — that belongs in `recommend-agentic-product-improvements`
- End every file with **Next step** (answer open questions first, then recommendations), horizontal rule, and footer

## Depth

- 2–5 confirmed findings for weak capabilities
- 0–2 confirmed findings for strong capabilities with a short **What works**
- Add **Open questions** when intent is unclear and not already in project context
- Open-ended assistants may support multiple jobs — do not invent a single user flow

## Good vs Bad

Bad:

> The agentic experience could be better.

Good (confirmed):

> ### No progress during long runs
> - **ID**: `no-progress-during-long-runs`
> - **What we observed**: Operators only see a static “running” badge with no step detail.

Good (open question):

> ### Failed tab hidden from members
> - **ID**: `failed-tab-hidden-from-members`
> - **What we observed**: Non-staff users cannot open the failed queue.
> - **Question:** Is staff-only visibility intentional for dogfooding?

## What This Format Covers

- Assessment, what works, confirmed findings, open questions
- Review-specific caveats in **Notes**

## What This Format Does Not Cover

- Answering open questions — use `manage-agentic-product-review-memory`
- Capability, experience, or surface — reference the discovery catalog
- Recommendations — use `recommend-agentic-product-improvements`
