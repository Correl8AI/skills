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

The product should know when the agent should stop.

Look for:

- Escalation path for ambiguous or high-risk cases
- Clear handoff to support, sales, expert review, or manual workflow
- No fake certainty when the agent lacks enough context
- Good handling of blocked tasks

### Output Review

Users should be able to inspect and adjust agent output.

Look for:

- Editable outputs
- Confirmation before use
- Explanation of what changed
- Source links or citations when relevant
- Easy regeneration or refinement

### Findings Priority (External)

1. Trust, safety, or permission issues
2. Broken or confusing first-run agent experience
3. Missing failure recovery
4. Unclear capability boundaries
5. Weak progress visibility
6. Missing output review or editing
7. Smaller wording or polish issues

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
5. Missing human oversight for high-risk flows
6. Stub or incomplete implementations

## All Capabilities

Also note:

- Incomplete or stub implementations
- Missing tests for critical agent behavior
- Ambiguous ownership between capabilities

Keep each capability review focused. A useful review with three strong findings is better than a broad list of generic observations.
