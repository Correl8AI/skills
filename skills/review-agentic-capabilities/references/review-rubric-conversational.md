# Conversational Agent Review Rubric

Use when the user **talks to the agent directly** — chat panel, copilot, assistant UI. Write findings per `output-format.md`. Do not re-catalog; read **Capability**, **Experience**, **Surface**, **Audience**, and **User persona** from the discovery catalog.

Also read `assessment-criteria.md` before setting **Assessment**.

Reviews are **product and user-experience** only — not architecture, code quality, or security unless they directly affect what people see.

## Audience — who you are reviewing for

Read **Audience** from the catalog. Choose what to flag based on this guidance — the sections below do not repeat audience on every line.

**Customer- or user-facing** (catalog: `external`, or the user-facing side of `mixed`)

The person should understand the agent, trust it, recover from errors, and get value quickly. Typical gaps: blank chat, unclear limits, missing cancel/approve, no path to support when stuck.

Staff-only UI inside a **customer** product (e.g. a log visible only to `is_staff`) is still a customer-product UX issue — see **Permission visibility** under Trust and control.

**Operator-facing** (catalog: `internal`)

Onboarding matters less than purpose, observability, permission boundaries, and override/stop. Skip **First run and onboarding** unless operators are genuinely lost on first use. Weight **Trust and control**, **Progress and state**, and **Data handling** more heavily.

**Mixed** — review user-facing paths with customer expectations.

Default scope: customer-facing unless the user asks to include operator-only capabilities.

## Agent identity and behavior

Review whether the system prompt and configuration give the agent enough context about **who it is** and **how it should behave** — distinct from **Purpose and boundaries** (what it can do) and **Persona fit** (how it talks to a specific human user).

Read the system prompt from implementation pointers. Look for:

- **Identity**: role in the product, name or persona if any, relationship to the user (advisor, operator copilot, support agent, …)
- **Behavior**: when to ask vs infer, proactive vs reactive, how to handle ambiguity, honesty about limits, when to escalate or defer
- **Constraints**: what it must not do or say, tone boundaries beyond generic “be helpful”
- **Consistency**: enough definition for repeatable behavior — not only model defaults or a one-line “you are an assistant”

Typical findings:

- Generic assistant with no product-specific identity or behavioral rules
- Missing guidance on escalation, approvals, or admitting uncertainty — behavior varies turn to turn
- Identity or behavior in the prompt conflicts with catalog **Capability** or **Experience**

Load `project-context.md` for overrides.

---

## User and channel context

Review what the agent **actually receives or can load at runtime** about the human and their situation — from the implementation only. Do **not** use catalog **User persona** here; that field describes who discovery thinks uses the capability and belongs in **Persona fit**.

Read implementation pointers: what is injected per turn, available via tools, or derivable from session state.

Look for:

- **Who the user is**: role, account type, permissions, expertise signals passed to the agent — not only free-text the user types in the thread
- **Where they are coming from**: entry point, prior screen or workflow step, deep link, handoff from another capability, failure or success state that triggered the conversation
- **Communication medium**: whether runtime context reflects how users reach the agent — synchronous chat panel, embedded copilot, async thread, notification reply, operator console — and whether prompt and UI match that mode

Typical findings:

- Product has distinct roles or permission levels but the agent receives no user identity beyond the thread
- User opens the agent from a specific workflow moment but nothing about origin or intent is passed on first turn
- Prompt or UX assume live back-and-forth chat but the surface is async or one-shot; or copilot beside the UI but no page or session context (see also **GUI context**)

Load `project-context.md` for overrides.

---

## Persona fit

Uses catalog **User persona** only — **Who**, **Expertise**, and **Jobs**. Review whether the **agent’s communication** (system prompt + observed behavior) fits that documented user. This is separate from **User and channel context**, which checks runtime facts the agent can see, not the catalog persona record.

Read the system prompt from implementation pointers. Check agent **tone**, **detail level**, and **technicality** of replies against the user’s **Expertise** and **Jobs**:

- Non-technical **Who** — plain language, no tool names or implementation jargon; numbered steps when the agent does complex work on their behalf
- Domain expert **Who** — appropriate domain terms; enough depth to act without hand-holding
- **Jobs** that involve multi-tool or technical work — prompt should instruct how to explain outcomes to this user, not raw dumps or model defaults

Typical findings:

- System prompt does not adapt communication to catalog **Expertise** — generic “be concise” only
- Agent performs complex technical tasks but replies at the wrong level for **Who** (too shallow or too technical)
- Prompt targets a different user than catalog **User persona** implies

Load `project-context.md` for overrides; prefer catalog **User persona** when both exist.

---

## Discoverability

How users **find and open** the agent — distinct from **First run and onboarding** (what they see after open).

Look for:

- Entry points: nav item, floating button, page-only embed, keyboard shortcut, command palette
- Consistency: same agent reachable from screens where context matters, or explicit reason it is not
- Affordance: icon-only or hidden triggers with no label; agent absent from places users expect help
- Discoverability vs scope: intentional single-screen copilot is fine — flag only when audience expects broader access

**Operator-facing:** admin nav, ops links, or buried config-only entry.

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

The first open should orient the user — not a blank input. Distinct from **Discoverability** (reach the panel) and **Purpose and boundaries** (ongoing mental model).

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

### Permission visibility

For **customer** or **mixed** products where some users have elevated roles:

- Role-gated tabs, queues, logs, or error detail (e.g. failed work visible only to staff)
- Users who trigger failures but cannot see status, errors, or retry paths
- Mismatch: customer-facing agent promises outcomes that only staff can inspect or fix

Undocumented role gates → **Open question** unless impact is clearly harmful. Documented intentional gates in catalog **Notes** or project context → skip.

---

## Progress and state

Look for:

- Thinking vs acting vs done; tool-step lines; partial results on long turns

**Operator-facing:** logs or audit trail; enough to debug failed runs.

### Async agent patterns

Many conversational agents return immediately and finish in a worker (HTTP 202, poll until idle, websocket optional). Review what the **user sees** during that gap — not the job system name.

Look for:

- Generic spinner or “thinking” with no tool-step or phase detail for multi-minute runs
- Poll-based UI with no partial assistant text, streamed tokens, or incremental action log
- Run appears stuck: no elapsed time, queue position, or “still working” signal
- Turn ends with empty or broken bubble after cancel — no explicit cancelled state or preserved partial output
- User cannot tell whether the run failed, was cancelled, or is still in progress

Flag **specific** gaps (e.g. “only static ThinkingText during 24 tool steps”) — not “needs better UX.”

---

## Failure and recovery

Look for:

- Actionable error messages; retry or rephrase paths; partial output preserved
- Fallback to manual workflow or **Human handoff** when stuck — not only a dead error state

**Operator-facing:** retries with limits; safe defaults when completion is impossible.

---

## Cross-capability handoff

When this chat capability **queues, triggers, or creates work** handled elsewhere (email, shared drafts, other surfaces):

Look for:

- User told clearly that work was queued and where to follow it
- Link, deep link, or in-product navigation to the artifact — not only prose (“check elsewhere”)
- Status or completion reachable without asking the agent again

If handoff is intentionally chat-only → **Open question** unless catalog **Notes** say so.

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

## Memory (user, session, project)

Assess whether **remembering context at the right scope** would materially help — then whether each level is implemented. Three scopes:

| Level | Scope | Examples |
|---|---|---|
| **Session** | One conversation or visit | Thread history, in-thread drafts, constraints stated this turn, GUI state while chat stays open |
| **User** | Same person across sessions | Communication prefs, personal defaults, profile fields injected into the agent |
| **Project** | Shared workspace (project, team, org) | Project config, date-range presets, domain glossary, standing filters — shared by collaborators, not only one thread |

Consider catalog **User persona**, **Jobs**, and **Experience**. Memory often matters when:

- **Session** — multi-turn work; agent should not re-ask settled questions in the same thread
- **User** — returning visitors with personal prefs or role-specific defaults
- **Project** — B2B or multi-user products where setup lives at project/workspace level and should persist for all sessions

If no level would meaningfully help (stateless one-shot, fully live-scoped by GUI only), say N/A in **Notes** — do not invent findings.

### What to look for

**Session** — prior messages and tool results; pending approvals; facts from earlier in the thread; page context updates without re-stating.

**User** — persisted prefs or profile across logins; user can see, edit, or reset what is stored.

**Project** — project-scoped config, metadata, or state in the agent context across threads and users; not re-entered each time someone opens the agent on the same project.

**Gaps to flag:**

- User repeats project-level setup (filters, range, taxonomy) every session though **Jobs** are project-scoped
- Thread forgets decisions mid-session without clear reset
- Personal prefs would help but only ephemeral thread history exists
- Project context exists in the UI but is not available to the agent across sessions

Name **which level** is missing or partial — not “add memory” generically.

**Operator-facing:** run history may cover session-like needs; weight user prefs and project-scoped operator config.

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

**Customer-facing:** agent identity and behavior → user and channel context → persona fit → trust and control (incl. permission visibility) → discoverability → first run → async progress → failure and recovery → cross-capability handoff → human handoff → product feedback → purpose and boundaries → GUI context → memory (user, session, project) → GUI action parity → context management → output review → polish

**Operator-facing:** agent identity and behavior → user and channel context → persona fit → trust and control → progress and state (incl. async) → failure and recovery → purpose and boundaries → memory (user, session, project) → data handling → context management → completeness → polish

---

Keep each review focused: three strong, specific findings beat a long generic list.
