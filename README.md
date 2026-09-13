# verify-budget

A lightweight Agent Skill for choosing the smallest verification set that gives
credible evidence for a change, without repeating checks that already passed.
The skill is named `minimal-verification`.

## When to use

Use after implementation, before running tests, lint, formatting checks, builds,
or reporting completion or creating a PR. It favors focused checks and respects
verification required by project instructions or acceptance criteria.

This is guidance for an agent, not an automated test runner. It adds no scripts,
dependencies, or build system.

## Local installation (Codex)

Clone the repository and copy the skill into your personal skills directory:

```sh
git clone https://github.com/LiuZhaoyan/verify-budget.git
cd verify-budget
mkdir -p ~/.agents/skills
cp -R skills/minimal-verification ~/.agents/skills/
cp LICENSE ~/.agents/skills/minimal-verification/LICENSE
```

If that skill is already installed, review local edits before replacing its files.
To update, run `git pull --ff-only` in this clone and repeat the copy commands.
You can also download the repository ZIP and copy the same directory and license.

Codex discovers `~/.agents/skills/` automatically. If the skill does not appear,
restart Codex. See the [Codex skills documentation](https://developers.openai.com/codex/skills/).

Example prompt:

```text
Use $minimal-verification to verify this change before creating the PR.
```

For example, after a focused test passes, creating the PR alone should not cause
it to run again. A later relevant code edit should trigger the focused check again.

## Directory structure

```text
verify-budget/
├── README.md
├── LICENSE
└── skills/
    └── minimal-verification/
        └── SKILL.md
```

## Maintenance

Edit `skills/minimal-verification/SKILL.md` and submit a PR describing the behavior
being changed. Keep the directory and frontmatter `name` aligned, and keep the
`description` specific about purpose and triggers. Follow the
[Agent Skills specification](https://agentskills.io/specification).

## License

[MIT](LICENSE). Keep the license notice when copying or redistributing the skill.
