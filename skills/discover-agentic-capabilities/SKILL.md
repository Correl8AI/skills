---
name: discover-agentic-capabilities
description: Discover conversational user-facing agentic capabilities in a codebase and write a Markdown catalog of what the repo implements.
---

# Discover Agentic Capabilities

Scan the repository and catalog every **conversational** user-facing agentic capability you can infer from the code — chat panels, copilots, and assistant UIs where the user talks to the agent directly.

Include external and internal user-facing capabilities. This is discovery only — catalog **what exists**, not how good it is.

## What Qualifies

Catalog a capability only when the codebase runs an **agent loop** that reaches a user — directly or through an artifact they consume.

An agent loop iterates, chooses tools or actions, observes results, and continues until done.

**Qualifies:**

- External user-facing agent loops (chat, copilot, assistant UIs)
- Internal user-facing agent loops (admin, operator, or support tools with a chat thread)

**Does not qualify:**

- Background or headless agent loops (queue, status, and results only — no chat thread)
- Agent loops with no user interaction and no user-visible artifact (system-only pipelines, service-to-service jobs)
- MCP/REST tool handlers or integration guides without a conversational UI in this repo
- Fixed workflows that chain LLM calls in a predetermined sequence
- One-shot LLM calls, embeddings, classification, or summarization
- Rule-based automation with no agent loop
- AI mentioned only in docs with no loop in code
- Shared agent infra — fold into the parent capability, not a separate entry

If borderline, include it with a short note in **Notes**.

## When To Use

Use this skill when the user asks to:

- Find user-facing agent loops in a repo
- Map what agentic capabilities exist for external users or operators
- Produce an inventory before a review
- Understand external vs internal user-facing agent capabilities

## What To Look For

Search for signals such as:

- Agent frameworks (Pydantic AI, LangChain agents, CrewAI, OpenAI Agents SDK, etc.)
- Tool definitions, tool registries, or MCP servers wired into a loop
- `while`/`until` loops, step runners, or turn-based agent execution
- External user chat, copilot, or assistant UIs backed by an agent loop
- Internal admin or operator chat/copilot UIs backed by an agent loop
- Human-in-the-loop gates inside a user-facing agent loop
- Tests that describe iterative agent behavior with a user or user-visible outcome
- System prompts and agent factory/config — especially when they name the target user or audience
- Product copy: UI strings, onboarding, empty states, in-repo docs
- What the product is and does — domain, surfaces, and tools imply who uses each capability

Read enough code to trace how each loop reaches a user or user-visible artifact. Prefer evidence from routes, handlers, jobs, tools, and UI — not only README claims.

For each capability, infer **User persona** from all applicable sources above. Record **Who**, **Expertise**, and **Jobs**.

Use **capability** as the stable unit.

## Discovery Process

0. Load `agentic-product-review/memory/project-context.md` if it exists (format: `review-agentic-capabilities/references/project-context-format.md`). Use answered intent when cataloging scope and notes. Do not write memory here — recording answers is in `review-agentic-capabilities`.
1. Scan the repo for agentic signals (grep, file tree, config, dependencies).
2. Group related code into distinct capabilities.
3. Drop loops that never reach a user or user-visible artifact.
4. For each remaining capability, determine **Audience** and infer **User persona** (see `references/output-format.md`).
5. Write `agentic-product-review/agentic-capabilities.md` using `references/output-format.md`. Create the folder if needed. Per capability: general fields (`ID`, `Audience`), then **Product**, **User persona**, **Tech**, then **Notes** last. End the output with **Next step**, horizontal rule, and footer.
6. Tell the user how many capabilities were found.

If nothing qualifies, say that clearly and list what was checked.

Do not implement code unless the user explicitly asks.

## What This Skill Covers

- Which conversational user-facing agent loops exist in the codebase
- Who each capability is for (**Audience**) and inferred **User persona** (who, expertise, jobs)
- What each agent does, how users encounter it, and where it appears in the product
- Where to find each capability in code (implementation pointers, tools)
- Structural facts in **Notes** — human-in-the-loop, config gates, links between capabilities, borderline scope

## What This Skill Does Not Cover

- Whether the experience is good or bad
- What works, what's broken, or what to improve
- Quality scores or overall assessment
- UX findings and quality judgment — use `review-agentic-capabilities`
- Recommendations and improvement guidance — use `recommend-agentic-product-improvements`

## Next Step

Tell the user:

```text
Found N user-facing agentic capabilities. Output written to agentic-product-review/agentic-capabilities.md.

Next step: run review-agentic-capabilities to review each capability.
```

