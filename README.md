# Master Learning for Claude Code

`master-learning` is a Claude Code skill that runs a pre-project learning pass before implementation. It helps Claude Code study official docs, papers, standards, GitHub repositories, examples, issues, and local code conventions before planning or editing.

The idea: a master keeps the mind of an apprentice.

## Install

### Personal Install

Copy the skill folder to your personal Claude Code skills directory:

```powershell
git clone https://github.com/GzmSTAR/master-learning-claude-code-skill.git
Copy-Item -Recurse -Force .\master-learning-claude-code-skill\.claude\skills\master-learning "$env:USERPROFILE\.claude\skills\master-learning"
```

### Project Install

Copy the skill into a project so the whole repository can use it:

```powershell
git clone https://github.com/GzmSTAR/master-learning-claude-code-skill.git
Copy-Item -Recurse -Force .\master-learning-claude-code-skill\.claude\skills\master-learning .\.claude\skills\master-learning
```

Restart Claude Code if the skill list does not refresh automatically.

## Usage

Invoke it explicitly:

```text
/master-learning Build a robot vision prototype. Study official docs, GitHub examples, papers, and local project constraints before planning.
```

```text
/master-learning Learn the current best implementation pattern for this new framework and produce a Learning Brief before coding.
```

The skill is configured with `context: fork` and `agent: general-purpose`, so the learning pass runs in an isolated context and returns a concise brief to the main session.

## Output

The skill returns a Learning Brief with:

- Task and research depth
- Source table
- Domain model
- Local code lessons
- GitHub/code lessons
- Paper/standard lessons
- Implementation patterns
- Risks and anti-patterns
- Recommendation and acceptance criteria
- Open questions

## SkillOpt-Style Optimization

This release includes a Microsoft SkillOpt-inspired optimization protocol. It treats `SKILL.md` as the trainable artifact, applies bounded text edits, and accepts a candidate only after a validation gate. See:

- `.claude/skills/master-learning/references/skillopt-training.md`
- `.claude/skills/master-learning/scripts/skillopt_train.py`
- `.claude/skills/master-learning/training/skillopt-run-2026-06-21.md`

## Structure

```text
.claude/
  skills/
    master-learning/
      SKILL.md
      references/
      scripts/
```

The helper scripts use only Python standard library.

## License

MIT
