# Agentic Product Review Skills

Open skills for finding, reviewing, and improving AI agent capabilities in a codebase.

These skills are meant for product and technical teams. They produce plain-language docs that explain what a product's agents can do, where the experience is strong or weak, and what to improve next.

## What's Included

| Skill | Purpose |
| --- | --- |
| `agentic-product-review` | Run the main discovery and review workflow. |
| `discover-agentic-capabilities` | Find agentic capabilities in a codebase. |
| `review-agentic-capabilities` | Review capabilities from a product and UX perspective. |
| `recommend-agentic-product-improvements` | Recommend codebase-grounded product improvements. |
| `manage-agentic-product-review-memory` | Track project context and open questions. |

## Usage

Run the full workflow:

```text
/agentic-product-review
```

Or run individual skills as needed:

```text
/discover-agentic-capabilities
/review-agentic-capabilities
/recommend-agentic-product-improvements
```

Outputs are written to `agentic-product-review/`, including:

| Output | Description |
| --- | --- |
| `agentic-capabilities.md` | Inventory of discovered capabilities. |
| `reviews/` | Product and UX reviews for each capability. |
| `recommendations/` | Suggested improvements with implementation context. |
| `memory/project-context.md` | Reusable project context and answered questions. |

If `memory/project-context.md` exists, load it before running discovery, review, or recommendation skills.

## Structure

```text
skills/
  agentic-product-review/
  discover-agentic-capabilities/
  manage-agentic-product-review-memory/
  recommend-agentic-product-improvements/
  review-agentic-capabilities/
README.md
LICENSE
skills.sh.json
```

## License

MIT