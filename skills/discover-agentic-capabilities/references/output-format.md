# Agentic Capabilities Catalog Format

Write discovery output as `agentic-product-review/agentic-capabilities.md` using this structure.

Create `agentic-product-review/` if it does not exist.

Load `agentic-product-review/memory/project-context.md` first when it exists (format: `review-agentic-capabilities/references/project-context-format.md`).

Outputs are read by **product and tech** people. Some readers have a light technical background — write product fields in plain language. Keep technical detail brief here; deep implementation guidance belongs in `recommend-agentic-product-improvements`.

This is the **inventory** step. Describe what exists — do not score quality, flag UX problems, or recommend fixes. Quality judgment belongs in `review-agentic-capabilities`; recommendations belong in `recommend-agentic-product-improvements`.

```md
# Agentic Capabilities

## Summary

- Total capabilities: N
- External: N
- Internal: N
- Mixed: N

## Capabilities

### <Capability Name>

- **ID**: `agent-chat`
- **Audience**: external | internal | mixed

#### Product

- **Capability**: What the agent does for users, in plain language
- **Experience**: How users or operators encounter it — mechanism and flow, not quality judgment (note when open-ended)
- **Surface**: Where in the product this appears — screen, panel, widget, report, notification, etc.

#### User persona

The **human using** this capability — not the agent’s voice or tone. Always infer from system prompt, product copy, and what the product is and does; never leave blank or “Unknown”. Discovery records who the product is for; review checks whether agent communication fits them.

- **Who**: Role and context (e.g. ecommerce shopper, support agent, PM reviewing analytics, staff engineer)
- **Expertise**: User’s technical/domain level (e.g. non-technical, business user, domain expert, engineer)
- **Jobs**: What they hire this agent for — list multiple when open-ended; do not invent a fixed step-by-step flow

Do **not** put agent tone, reply detail, or communication style here — those belong in review **Persona fit**, judged against this user persona.

#### Tech

- **Implementation pointers**: Key files only — enough to locate the capability in code, not a full architecture walkthrough
- **Tools used**: Short list only when non-obvious (external APIs, MCP, etc.)

- **Notes**: Structural facts only — human-in-the-loop, config gates, links to other capabilities, borderline scope. Not UX quality issues.

### <Capability Name>

...

## Next step

Run `review-agentic-capabilities` to review each capability.

---

*Something unclear or broken? Reach out at founders@correl8.ai*
```

## Rules

- Use stable capability IDs: short human-readable slugs in kebab-case (e.g. `agent-chat`), derived from the capability name
- Capability headings are names only — put IDs in the **ID** field, not in `###` headings
- Only catalog agent loops that reach a user directly or through a user-visible artifact.
- General fields (`ID`, `Audience`) come first, then **Product**, **User persona**, **Tech**, then **Notes** last.
- **User persona** sits between **Product** and **Tech** — describes the human user only; do not score agent communication fit here.
- **Notes** is shared — not duplicated under Product, User persona, or Tech.
- **Capability** and **experience** are the core product fields — keep them distinct and specific.
- **Surface** describes the product location, not file paths or routes.
- Product section must stand alone — a product reader should not need the tech section.
- Tech section stays brief. Do not dump stack traces, schemas, or implementation plans.
- If audience is hard to classify, pick the closest match and explain in **Notes**.
- Open-ended assistants and copilots may support multiple jobs — list them under **User persona** → **Jobs**; do not invent a step-by-step flow.
- **User persona** is required for every capability. Synthesize from system prompt, product copy, and product codebase. If evidence is thin, still infer from what the product is and does; note low confidence in **Notes**, not “Unknown”.
- Keep entries factual. Do not score quality, flag UX problems, or recommend fixes.
- **Notes** is for structural facts only — not UX gaps (those belong in review **Findings**).
- Default output path: `agentic-product-review/agentic-capabilities.md`
- End every output with **Next step**, horizontal rule, and footer:

  ```md
  ## Next step

  Run `review-agentic-capabilities` to review each capability.

  ---

  *Something unclear or broken? Reach out at founders@correl8.ai*
  ```

## Capability Boundaries

Split capabilities when:

- Different audiences (external vs internal)
- Different surfaces or products
- Different tool sets or risk profiles
- Clearly separate agent loops

Merge when:

- The same capability is split across files but is one user-visible experience
- Internal helpers are only supporting one parent capability

## What This Format Covers

- Capability, experience, surface, and user persona per agent loop
- Audience and implementation pointers
- Structural facts in **Notes**

## What This Format Does Not Cover

- Quality judgment, findings, or recommendations
- What works or what's broken — use `review-agentic-capabilities`
