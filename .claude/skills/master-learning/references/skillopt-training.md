# SkillOpt-Inspired Training Protocol

Microsoft SkillOpt treats a natural-language skill document as trainable external state for a frozen agent. The target model, tools, and harness stay fixed; the skill text changes through scored rollouts, reflection, bounded edits, and held-out validation gates.

This Claude Code skill applies the method at a practical repository level:

1. Define benchmark scenarios that represent expected user tasks.
2. Roll out the current skill against the scenarios using static checks and manual review.
3. Reflect on failures: missing trigger guidance, weak source coverage, vague outputs, unsafe implementation jumps, or unclear fork/main-session boundaries.
4. Apply bounded edits: add, delete, or replace small sections instead of rewriting the entire skill.
5. Validate on held-out scenarios. Accept only changes that improve measured coverage without adding bloat or contradictions.
6. Export the accepted skill as the deployable version.

## Local Benchmark Signals

The included `scripts/skillopt_train.py` uses deterministic checks for:

- Trigger coverage for unfamiliar, latest-docs, GitHub, paper, and local-code tasks.
- Output contract coverage for Learning Brief sections.
- Validation gate coverage: source audit, confidence, risk, acceptance criteria, and unresolved questions.
- Claude Code harness fit: `/master-learning`, `$ARGUMENTS`, `context: fork`, and no implementation in the skill run.
- Resource routing coverage for references and scripts.

This is not a full Microsoft SkillOpt run with model rollouts. It is a reproducible local optimization harness that follows the same bounded-edit and validation-gated discipline for this public skill repository.

## Acceptance Rule

A release candidate must:

- Score at least 0.90 overall on the local benchmark.
- Preserve Claude Code frontmatter.
- Compile all helper scripts.
- Avoid adding unverifiable claims or source fabrication.
- Keep the deployed skill compact enough to return a useful brief to the main session.
