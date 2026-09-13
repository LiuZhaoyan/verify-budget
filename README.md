# verify-budget

A lightweight Agent Skill that keeps verification proportional to the change.

Coding agents often over-verify after implementation: rerunning tests that already passed, launching repo-wide lint or typechecks for small edits, or repeating the same checks before commit, push, and PR creation.

`verify-budget` gives the agent a simple rule:

> Run the smallest set of checks that provides credible evidence for the change.

It does not reduce required verification. It avoids redundant verification.

## What it changes

Without a verification budget, an agent may do this:

```text
focused test
→ implementation
→ focused test
→ larger test suite
→ lint
→ formatter check
→ repeat tests before commit
→ repeat again before PR
```

With `minimal-verification`:

```text
implementation
→ relevant focused tests
→ necessary changed-file checks
→ done
```

Expensive repository-wide checks can be delegated to CI or a subagent when they are not required in the main workflow.

## Principles

The skill encourages agents to:

* run directly related focused tests after the final relevant edit;
* avoid rerunning passing tests when the covered code has not changed;
* prefer changed-file lint and formatting checks over repo-wide commands;
* avoid full test suites, builds, typechecks, or E2E unless they are actually required;
* delegate expensive verification to CI or subagents when appropriate;
* avoid duplicating verification already completed by a trusted subagent.

Project instructions and explicit acceptance criteria always take precedence.

## Install

Clone the repository:

```sh
git clone https://github.com/LiuZhaoyan/verify-budget.git
```

Install the skill into the cross-runtime Agent Skills directory:

```sh
mkdir -p ~/.agents/skills
cp -R verify-budget/skills/minimal-verification ~/.agents/skills/
```

Codex and other Agent Skills-compatible tools can discover skills from this directory.

## Use

The skill is designed to be loaded when implementation is complete and the agent is about to begin verification.

You can also invoke it explicitly:

```text
Use $minimal-verification to verify this change.
```

The agent should then choose the smallest credible verification set before running commands.

## Example

Suppose a focused test already passed after the final implementation edit.

Later, the agent stages the files and prepares a PR.

Without this skill, it may rerun the same test suite simply because it reached a new workflow stage.

With `minimal-verification`, staging, committing, pushing, or creating a PR are not themselves reasons to repeat an unchanged verification.

If relevant code changes again, the corresponding focused test should run again.

## Repository structure

```text
verify-budget/
├── README.md
├── LICENSE
└── skills/
    └── minimal-verification/
        └── SKILL.md
```

The project intentionally contains no runtime, dependencies, build system, or test framework. The behavior is defined entirely by the Agent Skill.

## Why a Skill?

This policy is useful across repositories, but it is also personal workflow guidance rather than a project-specific engineering requirement.

Keeping it as a Skill allows it to be injected when verification begins without adding verification preferences to every repository's `AGENTS.md`.

## License

MIT
