# Agentic Capabilities Review Format

Write one review file per capability under `agentic-product-review/reviews/`.

Create `agentic-product-review/reviews/` if it does not exist.

File naming: `<capability-slug>.md` (e.g. `agent-chat.md`) — match the catalog capability ID.

Before writing, load `agentic-product-review/memory/project-context.md` if it exists (format: `references/project-context-format.md`). Use answered intent to avoid re-raising resolved questions and to inform findings.

Set **Assessment** using `assessment-criteria.md` (`strong` | `acceptable` | `weak` | `incomplete`).

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

Behaviors that may be intentional. Do not list these under **Findings**.

### <short label>

- **ID**: `empty-state-no-examples`
- **What we observed**: What the product does today — behavior users see, not file paths
- **Question**: What needs human judgment to decide if this is a problem

## Notes

Review-specific caveats only — e.g. could not verify a flow, catalog entry was incomplete. Not structural facts already in the catalog.

## Next step

Run `recommend-agentic-product-improvements` to turn findings into codebase-grounded recommendations.

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
- Finding and open-question IDs: short human-readable slugs in kebab-case, derived from the entry label (e.g. `no-first-run-guidance`, `empty-state-no-examples`)
- Slugs must be unique within each review file
- Headings are labels only — put IDs in the **ID** field, never in titles or `###` headings
- **Findings** — only confirmed problems. Each entry has **What we observed** and **Impact**
- **Open questions** — may-be-intentional behaviors. Each entry has **What we observed** and **Question** — not **Impact**
- Do not duplicate an open question under **Findings**
- Skip open questions already answered in `project-context.md`
- Do not repeat **Experience**, **Surface**, or **User persona** — readers get those from the catalog
- **Notes** is a top-level `##` section
- Write in plain language — a product reader should not need any tech detail
- Do not recommend fixes — that belongs in `recommend-agentic-product-improvements`
- End every file with **Next step**, horizontal rule, and footer — do not mention memory workflow in output
- When the user answers an open question in conversation, follow **Recording open question answers** in `review-agentic-capabilities/SKILL.md` (update `project-context.md` and the review file; never describe this as a separate command in chat or written outputs)

## Assessment

See `assessment-criteria.md` for when to use each level:

| Level | Typical signal |
|---|---|
| **strong** | Core jobs work; no meaningful blockers |
| **acceptable** | Works with gaps; 1–2 findings, none blocking |
| **weak** | Trust, recovery, or visibility problems; 2–5 findings |
| **incomplete** | Stub, unreachable, or missing critical surfaces |

Assessment is a summary judgment — not finding count alone.

## Depth

- Match finding count to assessment (see `assessment-criteria.md`)
- Add **Open questions** when intent is unclear; skip if already in project context
- Apply **Agent identity and behavior** — flag when the system prompt lacks a clear agent role, behavioral rules, or constraints beyond generic assistant defaults
- Apply **User and channel context** — flag when the implementation passes no user identity, entry origin, or medium context the agent could use at runtime
- Apply **Persona fit** — flag when system prompt or replies use the wrong tone, detail, or technicality vs catalog **User persona**; weight heavily when **Jobs** include complex technical work

## Good vs Bad

Bad:

> The agentic experience could be better.

Good (confirmed):

> ### No progress during long runs
> - **ID**: `no-progress-during-long-runs`
> - **What we observed**: Users only see a generic “Thinking…” line with no tool-step detail during multi-minute chat turns.

Good (open question):

> ### Generic empty state on all pages
> - **ID**: `empty-state-no-examples`
> - **What we observed**: Every page shows the same “No messages yet.” with no context-specific starter prompts.
> - **Question:** Is a single generic empty state intentional to keep the panel simple?

Good (persona fit):

> ### Agent replies too technical for user
> - **ID**: `agent-communication-mismatch`
> - **What we observed**: Catalog user persona is non-technical PMs; system prompt only says “Markdown, concise” with no plain-language guidance; replies expose tool names and query-shaped reasoning.
> - **Impact**: Users cannot act on complex analysis the agent performs on their behalf.

Good (agent identity):

> ### No defined agent role or behavior
> - **ID**: `generic-agent-identity`
> - **What we observed**: System prompt is a single line (“helpful assistant”); no product role, escalation rules, or guidance on when to ask vs infer.
> - **Impact**: Replies feel interchangeable with any chatbot; users cannot tell what this agent is for in the product.

Good (user and channel context):

> ### Agent unaware of user entry point
> - **ID**: `no-entry-context`
> - **What we observed**: Users open chat from a failed export screen; nothing about the failure or current page is passed to the agent on first turn.
> - **Impact**: Users must re-explain what they were doing before the agent can help.

## What This Format Covers

- Assessment, what works, confirmed findings, open questions
- Review-specific caveats in **Notes**

## What This Format Does Not Cover

- Recording open question answers — see `review-agentic-capabilities/SKILL.md`; not user-facing workflow copy
- Capability, experience, or surface — reference the discovery catalog
- Recommendations — use `recommend-agentic-product-improvements`
