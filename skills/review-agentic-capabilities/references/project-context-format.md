# Project Context Memory Format

Maintain memory in `agentic-product-review/memory/project-context.md` only.

Create `agentic-product-review/memory/` and the starter file if missing.

## `project-context.md`

```md
# Project context

Condensed product intent from answered open questions. Load this before discovery, review, or recommendations.

## <Capability name>

- **ID**: `agent-chat`
- <Distilled fact from an answered open question — one line, plain language>

## <Capability name>

- **ID**: `background-agent-tasks`
- …

---

*Updated when open questions are answered.*
```

## Rules

- **project-context.md** is the only memory file
- Headings are capability names only — IDs live in the **ID** field
- Capability IDs are short human-readable slugs in kebab-case, matching the catalog
- Keep bullets short — distilled intent, not full Q&A transcripts
- After answering, remove the open question from the review's **Open questions** section
- Add or extend the capability section in project context; do not duplicate the same fact

## Starter file (when empty)

```md
# Project context

Condensed product intent from answered open questions. Load this before discovery, review, or recommendations.

_No answered open questions yet._

---

*Updated when open questions are answered.*
```
