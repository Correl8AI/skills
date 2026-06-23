# Agentic Product Review Skills

Open skills for finding, reviewing, and improving **conversational** AI agent capabilities in a codebase (chat, copilot, assistant UIs).

These skills are meant for product and technical teams. They produce plain-language docs that explain what a product's agents can do, where the experience is strong or weak, and what to improve next.

## What's Included


| Skill                                    | Purpose                                                |
| ---------------------------------------- | ------------------------------------------------------ |
| `agentic-product-review`                 | Run the full discovery, review, and recommendations workflow. |
| `discover-agentic-capabilities`          | Find agentic capabilities in a codebase.               |
| `review-agentic-capabilities`            | Review capabilities from a product and UX perspective. |
| `recommend-agentic-product-improvements` | Recommend codebase-grounded product improvements.      |


## Install

```bash
npx skills add Correl8AI/skills
```

## Usage

Run the full workflow (discovery, review, and recommendations):

```text
/agentic-product-review
```

Or run individual skills as needed (e.g. to re-run one phase):

```text
/discover-agentic-capabilities
/review-agentic-capabilities
/recommend-agentic-product-improvements
```

Outputs are written to `agentic-product-review/`, including:


| Output                      | Description                                                                     |
| --------------------------- | ------------------------------------------------------------------------------- |
| `agentic-capabilities.md`   | Inventory of discovered capabilities.                                           |
| `reviews/`                  | Product and UX reviews for each capability.                                     |
| `recommendations/`          | Suggested improvements with implementation context.                             |
| `memory/project-context.md` | Reusable project context (updated when you answer open questions from reviews). |


## Structure

```text
skills/
  agentic-product-review/
  discover-agentic-capabilities/
  recommend-agentic-product-improvements/
  review-agentic-capabilities/
README.md
LICENSE
skills.sh.json
```

## License

MIT