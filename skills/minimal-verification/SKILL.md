---
name: minimal-verification
description: Choose the smallest credible verification set and avoid redundant checks. Use when implementation is complete and the agent is about to run tests, lint, builds, or other verification before reporting completion or creating a PR.
license: MIT
---

# Minimal Verification

Use the smallest verification set that gives credible evidence for the change.

- Run directly related focused tests once after the final relevant edit.
- Do not rerun passing tests unless related code changed.
- Prefer changed-file lint/format checks over repo-wide commands.
- Do not run full test suites, full typechecks, builds, or E2E unless required by project instructions or acceptance criteria.
- Delegate expensive verification to a subagent or CI when possible.
- Do not duplicate verification already completed by a trusted subagent.
- Environment-blocked tests should be retried at most once in an appropriate environment.
- PR creation, commit, push, or staging are not reasons to rerun unchanged tests.

Before running any verification command, ask:
1. What specific risk does this command cover?
2. Has that risk already been checked?
3. Can a smaller focused command cover it?
4. Can CI or a subagent own it instead?
