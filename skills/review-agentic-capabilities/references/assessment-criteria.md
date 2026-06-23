# Assessment Criteria

Set **Assessment** on the review intro line: `strong`, `acceptable`, `weak`, or `incomplete`.

Pick one level per capability after applying the rubric. Use confirmed findings and **What works** together — assessment is a summary judgment, not a count of findings alone.

## strong

- Users or operators can complete the main jobs the capability supports without getting stuck
- Trust and control are clear: approvals, cancel/stop, and permission boundaries match expectations
- Failures are visible and recoverable; long runs show honest progress or partial output
- First-run empty states orient people
- No confirmed findings, or only minor polish gaps that do not block core use

## acceptable

- Core flows work but one or two meaningful gaps remain (e.g. weak empty state, coarse progress, agent communication mismatch for catalog user persona)
- Users can still get value with workarounds or patience
- Typically 1–2 confirmed findings; none are blockers for the primary job
- Open questions may exist but do not dominate the picture

## weak

- Multiple rubric gaps that erode trust, block recovery, or hide failures from the people who need them
- Typical pattern: blank first open, opaque long runs, missing cancel/approve, or broken handoff to related work
- Usually 2–5 confirmed findings; at least one affects trust, failure recovery, or permission visibility
- Users may abandon or distrust the capability even when backend logic works

## incomplete

- Capability is stubbed, behind a flag with no user path, or catalog entry describes more than the product ships
- Critical surfaces missing (chat UI with no send path, approval gate with no review UI)
- Do not use **weak** when the product simply is not finished — use **incomplete**
- Note in **Notes** what could not be verified end-to-end

## Re-review

When re-reviewing after fixes, bump assessment only when observed behavior changed — not when recommendations exist but code did not.
