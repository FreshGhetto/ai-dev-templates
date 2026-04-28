# AI_PROMPTS.md

This file contains reusable prompt templates for AI coding agents. Each prompt must be executed in English and must include the required final summary (modified files, checks run, risks, follow-up actions). Always follow the repository's `AGENTS.md` before performing work.

---

## 1. Safe implementation (feature / small enhancement)
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Implement the requested feature described below: {{SHORT_FEATURE_DESCRIPTION}}.

Scope:
- Limit changes to these paths: {{COMMA_SEPARATED_PATHS}} (or a single directory: {{DIR}}).
- Make only the smallest, focused changes necessary to implement the feature.
- Do not rename or move files, change unrelated modules, or change public APIs unless explicitly authorized.

Constraints:
- Do not modify dependencies, CI, production deployment configuration, or protected areas.
- Do not create, store, or commit any secrets.

Tasks:
1. Produce a brief written proposal (one-paragraph objective + file-level edit list).
   - If the task is large or ambiguous, obtain explicit human approval before editing.
2. Implement the changes with small, focused commits.
3. Add or update tests covering the new behavior.
4. Run the relevant checks listed below.

Checks to run (include exact commands and results):
- Linters and formatters (e.g., `npm run lint`, `flake8`, `gofmt`)
- Unit tests (e.g., `npm test`, `pytest`)

Final summary (required in PR description or commit):
- Summary: one-sentence description.
- Modified files: list paths added/modified/removed.
- Commands and checks run and results.
- Tests and results (unit/integration).
- Risks and impact.
- Rollback steps.
- Manual follow-ups required.

Do not make unrelated changes. If anything is ambiguous, stop and produce the required written proposal first.
```

---

## 2. Bug fix
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Fix the bug described: {{BUG_DESCRIPTION}} and add a regression test.

Scope:
- Limit changes to the minimum set of files required: {{COMMA_SEPARATED_PATHS}}.
- Do not change unrelated files or perform large refactors.
- Do not change dependencies or protected areas.

Steps:
1. Reproduce the bug locally and document the reproduction steps.
2. Add a failing test that demonstrates the bug (unit or integration).
3. Implement the minimal fix so the test passes.
4. Run linters and the full test suite relevant to the changed area.

Checks to run and include:
- Command to reproduce bug and output.
- Test commands (e.g., `pytest -q`) and results.
- Linter and formatter output.

Final summary (required):
- Summary: one-sentence description of the bug and fix.
- Reproduction steps used and their output.
- Modified files.
- Tests added/updated and results.
- Commands and checks run and results.
- Risks and potential side effects.
- Rollback steps and follow-up actions.

If the cause is unclear, stop and provide a short diagnostic report with suggested next steps instead of implementing changes.
```

---

## 3. Refactor (local, behavior-preserving)
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Perform a local refactor to improve readability or maintainability for {{CODE_AREA}} while preserving behavior.

Scope:
- Restrict edits to these files: {{COMMA_SEPARATED_PATHS}}.
- Preserve public API and observable behavior.
- Do not introduce dependency changes or alter protected areas.

Requirements:
1. Provide a short pre-edit summary describing the intended changes and why they are safe.
2. Make small commits, each addressing a single concern.
3. Add or update tests to verify unchanged behavior.
4. Run and include linter and tests output.

Final summary (required):
- Summary: what was refactored and why.
- Modified files.
- Commands and checks run and results.
- Tests and verification showing behavior preserved.
- Risks and suggested follow-ups.

Do not perform unrelated formatting-only mass changes or cross-module refactoring without explicit approval.
```

---

## 4. Code review (analysis only)
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Perform a code review for the provided diff or set of files: {{DIFF_OR_FILE_LIST}}.

Scope:
- Review only the supplied diff/files.
- Do not modify the code in this task. Provide review comments and suggested changes instead.

Deliverables:
- High-level summary of code quality and maintainability.
- Specific, actionable review comments (file:path and line references) grouped by severity (critical, major, minor).
- Missing tests or documentation notes.
- Security, performance, and compatibility concerns, if any.

Required final summary:
- Summary: one-sentence verdict.
- Files reviewed.
- Top 3 risks or blockers.
- Suggested fixes and example code snippets where helpful.
- Suggested test cases to add.

Do not open PRs or modify files; this task is for review only.
```

---

## 5. Test generation
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Write tests for {{TARGET_FILES_OR_FEATURE}} to improve coverage and prevent regressions.

Scope:
- Add tests only under the test directory or alongside existing tests in the same module.
- Do not modify production source code except to add non-invasive, test-only hooks if absolutely necessary and documented.

Requirements:
1. Provide a brief test plan listing the behaviors to cover.
2. Implement unit/integration tests following repository conventions.
3. Run the test suite for the changed area and include results.

Checks to run:
- Test command (e.g., `pytest -q`, `npm test`) and output.
- Coverage report if available.

Final summary (required):
- Summary: what tests were added and why.
- Modified files (tests only).
- Commands and checks run and results.
- Coverage changes (if applicable).
- Risks and follow-ups.

Do not add tests that require network access or secrets unless mocks or test doubles are used. Document any external dependencies required to run tests.
```

---

## 6. Documentation update
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Update documentation to reflect the following: {{DOCUMENTATION_GOAL}}.

Scope:
- Limit edits to documentation files: {{COMMA_SEPARATED_DOC_PATHS}}.
- Do not change source code, dependencies, or CI configuration.

Requirements:
1. Keep language clear, concise, and in English.
2. Add examples and usage snippets where helpful.
3. Update any README, changelog, or module-level docs that are directly relevant.

Final summary (required):
- Summary: what documentation was updated.
- Modified files.
- Commands/checks run (spellcheck, markdown linter).
- Risks (outdated examples, broken links).
- Follow-up actions (link checks, example validations).

Do not introduce content in other languages unless accompanied by an English canonical file.
```

---

## 7. Pull request summary (write PR title and description)
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Compose a concise PR title and a comprehensive PR description for these changes: {{MODIFIED_FILES_OR_DIFF}}.

Scope:
- Use only the provided changes; do not add or remove files.
- Do not edit code; only produce PR metadata content.

Required PR description sections:
- Title: one-line summary.
- Summary: one-paragraph description of the change and intent.
- Modified files: bullet list of changed paths.
- Commands and checks run: exact commands and results.
- Tests: tests run and results or link to CI.
- Risks and impact: short list.
- Rollback steps.
- Manual follow-ups required.

Deliverable:
- A ready-to-paste PR title and description following the repository’s conventions.

Do not include unrelated commentary or modify files when creating the PR summary.
```

---

## 8. Architecture review (analysis only)
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Provide an architecture review for {{MODULE_OR_SYSTEM}}. Deliver design observations, trade-offs, and recommended improvements.

Scope:
- Analysis only: do not change code or configuration.
- Focus on the specified module or system boundaries.

Deliverables:
- High-level diagram (textual) of components and interactions.
- Key strengths and weaknesses.
- Concise list of recommended changes (prioritized: quick wins, medium, long-term).
- Migration and compatibility considerations for each recommendation.

Final summary (required):
- Summary: one-sentence assessment.
- Files or areas considered.
- Top 3 recommended actions with rationale.
- Risks and rollback considerations for each recommendation.
- Suggested next steps (including specific small tickets).

Do not propose invasive changes without a clear migration plan. For any recommended code changes, produce a separate proposal first.
```

---

## 9. Performance review
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Review performance characteristics of {{TARGET_AREA}} and recommend improvements.

Scope:
- Analysis and suggestions only unless explicit permission is given to implement changes.
- Do not change production configuration or infrastructure.

Deliverables:
- Suggested profiling or benchmark commands to run and how to collect results.
- Identified hotspots and concrete optimization suggestions (with estimated impact).
- Safe, incremental refactoring options and tests to validate improvements.

Final summary (required):
- Summary: one-sentence result of the review.
- Commands to run, sample outputs, and interpretation.
- Modified files (if any — note: this task is analysis-first).
- Performance risks and trade-offs.
- Recommended follow-ups (benchmarks, monitoring, staging rollout).

Do not implement speculative changes that could alter behavior without a separate approval and test plan.
```

---

## 10. Security review
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Perform a security review of {{TARGET_FILES_OR_MODULE}} focusing on secrets, injection risks, dependency vulnerabilities, and configuration issues.

Scope:
- Analysis and reporting only. Do not commit secrets or change secret-handling behavior.
- Do not modify production credentials or environment files.

Deliverables:
- Static checks and commands to run (e.g., secret scanning, SAST, `npm audit`, `safety`).
- List of findings prioritized by severity with concrete remediation suggestions.
- Dependency vulnerabilities found and recommended mitigation steps (do not upgrade automatically).

Final summary (required):
- Summary: high-level security posture.
- Files reviewed.
- Commands and checks run and results.
- Findings with severity and remediation.
- Risks if left unaddressed.
- Suggested follow-up actions and required approvals.

If a critical vulnerability is discovered that requires immediate attention, stop and notify the human maintainers per the repository’s incident process.
```

---

## 11. Dependency review (audit and recommendation)
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Audit project dependencies for security, licensing, and maintenance risks and provide recommendations.

Scope:
- Analysis and recommendations only. Do not change dependencies or lockfiles automatically.
- Include direct and transitive dependency checks.

Deliverables:
- Commands run (e.g., `npm audit`, `yarn audit`, `safety check`, `mvn dependency:tree`) and outputs.
- List of risky or unmaintained packages with severity and suggested actions (patch, upgrade, replace).
- Testing and migration plan for each suggested change.

Final summary (required):
- Summary: top dependency risks.
- Commands and checks run and results.
- Proposed dependency changes and justification (do not apply them).
- Risk assessment and test plan for each proposed change.
- Required approvals and rollout guidance.

Do not perform automatic upgrades without explicit human approval and a test plan.
```

---

## 12. Plan only (discovery and approval)
Prompt:
```
You must follow `AGENTS.md` for all behavior and approvals.

Goal: Produce a focused implementation plan for the requested work: {{HIGH_LEVEL_REQUEST}}. Do not modify code in this task.

Scope:
- Analysis and planning only. No code changes.

Required plan content:
- One-paragraph objective summary.
- File-level edit list (paths to add/modify/remove).
- Exact commands and checks you will run to implement and verify (linters, builds, tests).
- Test plan and acceptance criteria.
- Risk assessment with mitigations.
- Rollback procedure and manual follow-ups.
- Estimated size (number of commits, effort estimate).

Final deliverable (required):
- A plan document ready for human review that includes the items above and a recommended next action (approve and implement or request more information).

Do not proceed to implement until explicit human approval is provided.
```

---


