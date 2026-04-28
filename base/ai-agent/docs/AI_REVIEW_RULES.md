## AI Review Rules

These review rules guide both automated agents and human reviewers when evaluating changes produced by AI assistants. Follow `AGENTS.md` for policy constraints and required summaries.

Reviewer checklist (high level):
- Correctness: Does the change implement the intended behavior and handle edge cases?
- Scope: Are only the necessary files modified? Are unrelated areas untouched?
- Tests: Are there appropriate tests (unit/integration) and do they pass?
- Safety: Does the change avoid secrets, destructive operations, or protected areas?
- Style: Does the change follow repository coding and documentation conventions?
- Performance and security: Any obvious regressions or vulnerabilities introduced?

Severity levels for issues:
- Critical: Breaks build, causes data loss, introduces security vulnerability, or touches protected areas incorrectly. Requires immediate fix and human approval.
- Major: Functional regression, missing tests, or dependency/security concerns that must be addressed before merge.
- Minor: Style, documentation, or non-blocking maintainability issues that should be fixed but do not prevent merging.

Automated checks to run for reviews:
- Linters and formatters (language-specific).
- Unit and integration tests relevant to the changed area.
- Static analysis and security scans (SAST, dependency audit) when applicable.

How to review AI-produced changes:
1. Verify the final summary produced by the agent matches the actual changes.
2. Run the listed commands locally or inspect CI results.
3. Confirm tests added or updated actually cover the change surface and regressions.
4. Check for accidental inclusion of secrets or environment changes.
5. Validate that any `AGENTS.append.md` fragments applied are documented in `AGENTS.md` and do not declare `override: true` without human approval.

Handling disagreements or unclear edits:
- If the change is ambiguous or risky, request the agent to produce the short proposal required by `AGENTS.md` and wait for human approval.
- For critical issues, block the PR and request an explicit fix or rollback.
- For non-critical items, add review comments and request targeted follow-up commits.

Security and incident response:
- If a reviewer discovers a high-severity vulnerability or secret exposure, immediately notify maintainers and follow the repository incident process.
- Do not attempt to remediate secrets or sensitive issues by committing fixes that contain new secrets; always use approved secrets management processes.

Approval criteria:
- Tests for the changed area pass and are included in the PR or linked CI.
- No critical or major blockers remain unresolved.
- The change is within scope and follows `AGENTS.md` constraints.
- At least one human reviewer has approved the PR for non-trivial changes.

Merge guidance:
- Prefer squash or merge strategies consistent with repository policies.
- Ensure the PR description includes the agent's final summary checklist (modified files, commands run, risks, rollback).
- If an install/merge script updated `AGENTS.md`, verify the generated metadata and appended fragments are documented and do not include unauthorized overrides.

Post-merge verification:
- Ensure any manual follow-ups are tracked and completed.
- Monitor CI and error tracking systems for regressions related to the change.


