# Agentic Capabilities Review Rubric

Use this rubric to think; write findings per `output-format.md`. Do not re-catalog — experience and surface live in the discovery catalog.

Apply the sections below based on each capability's audience in the catalog.

Reviews are a **product and user-experience** exercise. Evaluate what users and operators experience — not architecture.

Use these terms consistently:

- **Capability**: The stable unit being reviewed, identified by a short slug (e.g. `agent-chat`, `background-agent-tasks`)
- **Experience**: How users or operators encounter the capability
- **Surface**: Where the capability appears — screen, panel, widget, report, notification, etc.

## External Capabilities

### Capability Clarity

Users should understand what the agent can do, what it cannot do, and what outcome they should expect.

Look for:

- Clear explanation before first use
- Examples of good inputs
- Boundaries and limitations
- Expected output format
- Clear success state

### First-Run Experience

The first user interaction with the agent should be clear, whether the assistant is open-ended or guided.

Look for:

- A clear starting point
- Minimal setup before value
- One recommended first action
- No empty AI input with no guidance
- No unexplained permissions request

### Trust And Control

Users should feel in control of agent actions.

Look for:

- Explicit approval before consequential actions
- Clear data-use explanation
- Ability to cancel, pause, or edit
- Visible source or reasoning when useful
- Review step before sending, publishing, deleting, buying, or changing data

### Progress And State

Users should know what the agent is doing.

Look for:

- Loading states that name the current step
- Long-running task progress
- Tool-use status
- Clear distinction between thinking, acting, waiting, and done
- Useful partial results when a task takes time

### Failure And Recovery

Agent failures should be recoverable.

Look for:

- Helpful error messages
- Retry paths
- Suggestions for better input
- Partial output preservation
- Safe fallback to manual or human help

### Human Handoff

When the agent cannot help, users need **someone who can unblock them now** — not async product input (see Feedback To Team).

Judge by **user intent** (“help me with this”), not org chart. The handoff target is typically **support, CX, or CS**; also sales, onboarding, account help, or expert review when relevant.

Look for:

- Escalation path for ambiguous or high-risk cases
- Clear handoff to support, CX, CS, sales, expert review, or manual workflow
- No fake certainty when the agent lacks enough context
- Good handling of blocked tasks
- A way to **reach a person for live help** when stuck (chat link, email, in-app contact, scheduled call)
- Agent behavior that **offers** human handoff when it cannot help, not only when the user hunts for it

**Write findings as specific gaps** — e.g. no support/CX path in chat, agent loops without suggesting help, user must leave the product to get unblocked.

### Feedback To Team

Users should be able to **pass product feedback** from the agent surface — bugs, feature asks, “this is wrong”, product confusion. Async input for **PM / eng / design**, not live session help (see Human Handoff).

Direct product intake or **support triage that preserves context and routes feedback** both count. A single contact (e.g. support@) is fine if the user can distinguish “get help” from “send feedback” and thread context is attached.

Look for:

- Route for bug reports, feature asks, or product confusion
- Conversation or session context attached when useful so the team does not need a re-explanation
- Confirmation that the message was received; expected response time if applicable
- Agent behavior that **offers** to send feedback when appropriate, not only a buried link

**Write findings as specific gaps** — e.g. user must copy-paste into email, feedback form drops thread context, no route for “tell the team about this”, help and feedback conflated with no context attached.

### Output Review

Users should be able to inspect and adjust agent output.

Look for:

- Editable outputs
- Confirmation before use
- Explanation of what changed
- Source links or citations when relevant
- Easy regeneration or refinement

### Surface And GUI Context

When the chat panel can open **beside the app UI**, check whether the agent has what it needs to answer questions about **this page, this selection, this view**.

Look for:

- Current route, page, or screen passed into the agent (project, entity IDs, tab, filters)
- Relevant **GUI state**: selection, expanded rows, form values, date range, sort, visible chart or table slice
- Context that updates when the user navigates or changes the UI while chat stays open
- Tools or metadata to fetch on-screen data the user is asking about (“this interaction”, “what I’m looking at”) without making them paste it

**Write findings as specific gaps**, not a generic “detached assistant” label. Compare what the user sees on the open surface to what the agent receives or can load — e.g. missing filter state, selected row ID, active tab, unsaved form field, chart time range, or a column/value visible in the table but not in any tool response.

Only flag surface-context issues when you can name **concrete information** the agent lacks for questions users would reasonably ask from that screen.

### GUI Action Parity

When chat sits beside the GUI, users should be able to **automate manual work** by asking the agent to do what they would click or type themselves.

Look for:

- Agent tools or actions that mirror operations available in the UI on that page (create, edit, filter, navigate, export, etc.)
- Clear scope: what the agent can and cannot drive on the current surface
- User-visible confirmation or approval before consequential GUI-driven changes (ties to Trust And Control)
- The UI updating when the agent acts so the user sees the same outcome as if they had done it manually

**Write findings as specific missing actions**, not “no GUI parity” in the abstract. List UI controls or workflows on the current surface that the user can perform but the agent cannot — e.g. apply a filter, open a detail panel, save an edit, run an export, toggle a setting. Note when the agent can only **describe** those steps.

Prefer parity on the **current page** first; broader cross-app automation is a plus, not a substitute for the screen the user has open.

### Findings Priority (External)

1. Trust, safety, or permission issues
2. Broken or confusing first-run agent experience
3. Missing failure recovery
4. No human handoff to support/CX/CS (or equivalent) when the agent cannot help
5. No way to pass product feedback to the team — direct or triaged via support — with context preserved
6. Unclear capability boundaries
7. Specific surface or GUI state the agent cannot see or load on a co-located chat (named field, selection, filter, etc.)
8. Specific UI actions on the current page the agent cannot perform (named control or workflow)
9. Context stuffed into prompts instead of loaded via tools (when it hurts answer quality or reliability)
10. Weak progress visibility
11. Missing output review or editing
12. Smaller wording or polish issues

## Internal Capabilities

### Purpose Clarity

Operators or the system should have a clear job for this agent.

Look for:

- Documented or inferable purpose
- Clear trigger conditions
- Obvious scope of action

### Trigger And Scope

Look for:

- When the agent runs and why
- What data and systems it can touch
- Boundaries that prevent runaway behavior

### Tool And Permission Boundaries

Look for:

- Least privilege for tools and APIs
- Dangerous actions gated behind approval
- Separation between read and write actions

### Observability

Look for:

- Logs, traces, or audit trail for agent actions
- Enough context to debug failed runs
- Correlation between user actions and agent steps

### Failure Handling

Look for:

- Retries with limits
- Dead-letter or failed-job handling
- Safe defaults when the agent cannot complete

### Human Oversight

Look for:

- When operators must approve or intervene
- Escalation for ambiguous or high-risk cases
- Clear operator controls to stop or override

### Data Handling

Look for:

- What context is passed to models
- What is stored and for how long
- Sensitive data boundaries

### Findings Priority (Internal)

1. Ungated dangerous actions
2. Missing observability for consequential runs
3. Weak failure handling or silent failures
4. Over-broad tool or data access
5. Heavy static context instead of on-demand read tools (cost, truncation, or missed fetches)
6. Missing human oversight for high-risk flows
7. Stub or incomplete implementations

## All Capabilities

### Context Management

Prefer **on-demand loading via tools** over **large static context** in every agent turn.

The agent should receive a lean system prompt (role, boundaries, task metadata) and **tools to fetch** what it needs — interactions, issues, observations, codebase slices, etc. Avoid inlining long resources up front “just in case.”

Look for:

- Large schemas, file trees, conversation dumps, or datasets copied into the system prompt or first user message
- The same bulky blob resent on every step of the agent loop
- Read tools with explicit parameters (IDs, date ranges) so the agent can pull scoped data when relevant — and evidence the agent loop actually uses them
- Missing tools for data the agent clearly needs but that only exists if pre-stuffed into the prompt
- User- or operator-visible symptoms: vague or incomplete answers, step-cap hits, slow turns, or failures when context limits are approached

When reviewing, note whether the product follows the preferred strategy (tools to load) or relies on stuffed context — and whether users or operators pay the cost (quality, latency, opacity).

Also note:

- Incomplete or stub implementations
- Missing tests for critical agent behavior
- Ambiguous ownership between capabilities

Keep each capability review focused. A useful review with three strong findings is better than a broad list of generic observations.