# Agentic Skills

Open agent skills for product and technical teams discovering, reviewing, and improving agentic capabilities in a codebase.

Outputs are written for **product and tech** readers in `agentic-product-review/`:

| File | Skill |
| ---- | ----- |
| `agentic-capabilities.md` | `discover-agentic-capabilities` |
| `reviews/agent-chat.md`, `reviews/background-agent-tasks.md`, … | `review-agentic-capabilities` |
| `recommendations/agent-chat.md`, `recommendations/background-agent-tasks.md`, … | `recommend-agentic-product-improvements` |
| `memory/project-context.md` | `manage-agentic-product-review-memory` |

Load `memory/project-context.md` before discovery, review, or recommendations when it exists.

Discovery and review focus on product and user experience in plain language. `recommend-agentic-product-improvements` adds codebase-grounded implementation detail.

Use **capability** as the stable inventory unit. Each capability can also describe the user **experience** and the product or system **surface** where it appears. General assistants and copilots may be open-ended and may support multiple jobs.

## Skills


| Skill                           | What it does                                                                                                                  |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `discover-agentic-capabilities` | Scan the repo → `agentic-product-review/agentic-capabilities.md` |
| `review-agentic-capabilities`   | Review each catalog entry → `agentic-product-review/reviews/agent-chat.md` |
| `recommend-agentic-product-improvements` | Codebase-grounded improvements → `agentic-product-review/recommendations/agent-chat.md` |
| `manage-agentic-product-review-memory`    | Answer open questions → `memory/project-context.md` |
| `agentic-product-review`        | Discover + review external capabilities → `agentic-capabilities.md` + `reviews/agent-chat.md` |


Typical workflow:

```text
/agentic-product-review
```

Or step by step:

```text
/discover-agentic-capabilities
/review-agentic-capabilities
/recommend-agentic-product-improvements
/manage-agentic-product-review-memory background-agent-tasks/no-direct-task-creation-ui
```

## Install

Claude Code first:

```bash
npx skills add your-org/agentic-product-review -g -a claude-code -y
```

Project install:

```bash
npx skills add your-org/agentic-product-review -a claude-code
```

Try without installing:

```bash
npx skills use your-org/agentic-product-review --agent claude-code
```

Future targets:

```bash
npx skills add your-org/agentic-product-review -a codex
npx skills add your-org/agentic-product-review -a cursor
```

## Structure

```text
skills/
  discover-agentic-capabilities/
    SKILL.md
    references/
      output-format.md
  review-agentic-capabilities/
    SKILL.md
    references/
      output-format.md
      review-rubric.md
  recommend-agentic-product-improvements/
    SKILL.md
    references/
      output-format.md
  manage-agentic-product-review-memory/
    SKILL.md
    references/
      output-format.md
  agentic-product-review/
    SKILL.md
README.md
LICENSE
skills.sh.json
```

## License

MIT