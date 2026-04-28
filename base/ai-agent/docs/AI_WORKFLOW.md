## AI Workflow

This document describes a lightweight, repeatable workflow for AI coding agents working in repositories that follow `AGENTS.md`.

1. Receive Task
- Read the request or issue carefully and identify the explicit objective.
- Confirm scope: determine the minimal set of files or module areas required to complete the task.

2. Prepare Proposal (when required)
- For ambiguous, multi-step, or high-impact tasks, stop and produce a short written proposal that includes:
  - One-paragraph objective summary.
  - File-level edit list (paths to add/modify/remove).
  - Commands and checks to run (linters, tests, build).
  - Risk assessment and rollback steps.
  - Suggested commit/PR title and short description.
- Await explicit human approval before editing.

3. Implement Changes
- Make small, focused commits limited to the agreed scope.
- Update or add tests for the changed behavior when applicable.
- Do not change dependencies, protected areas, or unrelated code unless explicitly requested.

4. Local Verification
- Run linters, formatters, and relevant unit tests for the changed area.
- Record exact commands and results for inclusion in the final summary.

5. Create Pull Request
- Provide a clear PR title and description that includes:
  - What changed and why.
  - Files modified.
  - Commands and checks run and their outcomes.
  - Risks and rollback instructions.
- Request at least one human reviewer for non-trivial changes or changes touching protected areas.

6. Post-Merge Actions
- Document any manual follow-ups (running migrations, updating configuration, notifying stakeholders).
- If a migration or deployment step is required, include a staged rollout plan and monitoring guidance.

7. Final Summary (required)
- After merging or completing the task, produce a final summary containing:
  - One-sentence summary of the change.
  - Modified files list.
  - Commands and checks run and results.
  - Tests run and results.
  - Identified risks and mitigations.
  - Rollback procedure.
  - Manual follow-ups required.

Behavioral notes:
- Always follow `AGENTS.md`.
- Favor minimal, incremental work and explicit human sign-off for high-risk items.
- Do not commit secrets or bypass CI checks.


