# Headless Agent Review Rubric

Use when users **never converse** with the agent — only queue, status, results, and errors. Write findings per `output-format.md`. Do not re-catalog; read **Capability**, **Experience**, **Surface**, and **Audience** from the discovery catalog.

Reviews are **product and user-experience** only — not architecture, code quality, or security unless they directly affect what people see.

If the user talks to the agent directly (chat, copilot), use `review-rubric-conversational.md` instead.

**Headless test:** No chat thread → this rubric.

**Cross-capability rule:** Do not flag missing **Human handoff** or **Product feedback** here. Flag those on the conversational capability that queues or triggers work, if one exists.

## Audience — who you are reviewing for

Read **Audience** from the catalog. Choose what to flag based on this guidance.

**Customer- or user-facing** (catalog: `external`, or the user-facing side of `mixed`)

People should understand the queue, see honest status, recover from failures, and find what the agent produced. Typical gaps: hidden failures, opaque “running” state, results disconnected from artifacts, no retry.

Staff-only visibility inside a **customer** product (e.g. failed tab staff-only) is a customer-product UX issue — permissions and visibility.

**Operator-facing** (catalog: `internal`)

Weight purpose, triggers, observability, permission boundaries, and failure handling. Typical gaps: silent failures, ungated writes, no audit trail, unclear run lifecycle.

**Mixed** — review user-visible queue and results with customer expectations.

Default scope: customer-facing unless the user asks to include operator-only capabilities.

---

## Context management

Prefer **on-demand tools** over **large static context** in every turn.

Look for:

- Bulky schemas or dumps copied into the system prompt or resent each step
- Read tools with explicit parameters — and evidence the loop uses them
- Visible cost: failed jobs, truncation, vague result summaries, step-cap hits

**Operator-facing:** whether operators can debug bad context choices.

---

## Completeness

Look for:

- Stub or incomplete implementations
- Missing tests for critical agent behavior
- Ambiguous ownership between capabilities

---

## Purpose and boundaries

People should understand what the queue or job is for, what triggers a run, and what success produces.

Look for:

- Queue purpose and triggers (manual, automatic, from chat elsewhere)
- Empty states that explain what will appear and why

**Operator-facing:** inferable job purpose; clear trigger conditions; scope boundaries.

---

## Trust and control

Look for:

- Cancel or stop in-flight work when supported
- Visibility or approval before autonomous side effects land
- Failed or cancelled work visible — not hidden by role, tab, or filter

**Operator-facing:** least privilege; gated writes; read vs write separation; operator stop or override.

---

## Progress and state

Look for:

- Pending → running → terminal transitions; polling or notifications that reflect reality
- Step or tool activity during long runs — not only a static “running” badge

**Operator-facing:** logs, traces, or audit trail; correlation between triggers and steps.

---

## Failure and recovery

Look for:

- Actionable error messages; retry or requeue; partial output preserved
- Error detail on the task surface — not in-chat support routes

**Operator-facing:** retries with limits; dead-letter handling; safe defaults when completion is impossible.

Do **not** expect human handoff or product-feedback flows on headless surfaces.

---

## Output review

Look for:

- Readable result summary
- Links to artifacts the agent created
- Clear before/after when the run changed data

---

## Data handling

**Operator-facing**, or customer-facing when users see or control what data the agent uses.

Look for:

- What context goes to models; what is stored and for how long
- Sensitive data boundaries in the UX

---

## Findings priority

**Customer-facing:** hidden failures → progress and state → trust and control → failure and recovery → output review → purpose and boundaries → context management → polish

**Operator-facing:** trust and control → progress and state → failure and recovery → purpose and boundaries → data handling → context management → completeness → polish

---

Keep each review focused: three strong, specific findings beat a long generic list.