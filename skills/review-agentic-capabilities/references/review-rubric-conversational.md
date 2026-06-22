# Conversational Agent Review Rubric

Use when the user **talks to the agent directly** — chat panel, copilot, assistant UI. Write findings per `output-format.md`. Do not re-catalog; read **Capability**, **Experience**, **Surface**, and **Audience** from the discovery catalog.

Reviews are **product and user-experience** only — not architecture, code quality, or security unless they directly affect what people see.

If the capability is headless (queue, status, results only), use `review-rubric-headless.md` instead.

## Audience — who you are reviewing for

Read **Audience** from the catalog. Choose what to flag based on this guidance — the sections below do not repeat audience on every line.

**Customer- or user-facing** (catalog: `external`, or the user-facing side of `mixed`)

The person should understand the agent, trust it, recover from errors, and get value quickly. Typical gaps: blank chat, unclear limits, missing cancel/approve, no path to support when stuck.

Staff-only UI inside a **customer** product (e.g. a log visible only to `is_staff`) is still a customer-product UX issue — permissions and visibility.

**Operator-facing** (catalog: `internal`)

Onboarding matters less than purpose, observability, permission boundaries, and override/stop. Skip **First run and onboarding** unless operators are genuinely lost on first use. Weight **Trust and control**, **Progress and state**, and **Data handling** more heavily.

**Mixed** — review user-facing paths with customer expectations.

Default scope: customer-facing unless the user asks to include operator-only capabilities.

---

## Context management

Prefer **on-demand tools** over **large static context** in every turn.

Look for:

- Bulky schemas, dumps, or datasets copied into the system prompt or resent each step
- Read tools with explicit parameters (IDs, date ranges) — and evidence the loop uses them
- Data only available because it was pre-stuffed into the prompt
- Visible cost: vague answers, step-cap hits, slow turns, limit failures

**Operator-facing:** whether operators can debug bad context choices.

---

## Completeness

Look for:

- Stub or incomplete implementations
- Missing tests for critical agent behavior
- Ambiguous ownership between capabilities

---

## Purpose and boundaries

People should understand what the agent can do, what it cannot do, and what “done” looks like.

Look for:

- Capability explanation; example inputs; limitations; expected output format

**Operator-facing:** inferable purpose, clear triggers, scope boundaries.

---

## First run and onboarding

Skip for operator-facing capabilities unless operators are lost on first use.

The first open should orient the user — not a blank input. Distinct from **Purpose and boundaries** (first screen vs ongoing mental model).

Look for:

- Starting point, minimal setup before value, suggested first actions
- No unexplained permission prompts

---

## Trust and control

Look for:

- Approval before writes, publishes, deletes, or other irreversible actions
- Cancel, pause, or stop a running turn
- Clear data-use explanation when relevant; visible reasoning or sources when useful

**Operator-facing:** least privilege; gated dangerous actions; read vs write separation; stop/override.

---

## Progress and state

Look for:

- Thinking vs acting vs done; tool-step lines; partial results on long turns

**Operator-facing:** logs or audit trail; enough to debug failed runs.

---

## Failure and recovery

Look for:

- Actionable error messages; retry or rephrase paths; partial output preserved
- Fallback to manual workflow or **Human handoff** when stuck — not only a dead error state

**Operator-facing:** retries with limits; safe defaults when completion is impossible.

---

## Output review

Look for:

- Edit, confirm, regenerate; citations or source links when relevant

---

## Human handoff

**Customer-facing capabilities only.**

Live help when blocked — support, CX, CS, onboarding, expert review. Not **Product feedback**.

Look for:

- Escalation when blocked or high-risk; agent **offers** handoff
- No false certainty when context is insufficient

---

## Product feedback

**Customer-facing capabilities only.**

Async input to the product team — bugs, wrong answers, feature asks. Not live help.

Look for:

- Route from the agent surface (not copy-paste email as primary path)
- Session context attached; confirmation received; distinct from handoff

---

## GUI context

When chat sits **beside** the app UI, the agent should know what the person is looking at.

Look for:

- Route, entity IDs, tabs, filters, date range, selection passed or loadable via tools
- Context updates when they navigate while chat stays open

Flag **specific** missing fields — not a generic “detached assistant.”

---

## GUI action parity

When chat sits beside the UI, the agent should do what they could click — not only describe steps.

Look for:

- Tools mirroring key UI operations (create, edit, filter, export, …)
- UI updates when the agent acts; confirmation before consequential changes

List **specific** missing actions.

---

## Data handling

**Operator-facing**, or customer-facing when users see or control what data the agent uses.

Look for:

- What context goes to models; what is stored and for how long
- Sensitive data boundaries in the UX

---

## Findings priority

**Customer-facing:** trust and control → first run → failure and recovery → human handoff → product feedback → purpose and boundaries → GUI context → GUI action parity → context management → progress and state → output review → polish

**Operator-facing:** trust and control → progress and state → failure and recovery → purpose and boundaries → data handling → context management → completeness → polish

---

Keep each review focused: three strong, specific findings beat a long generic list.
