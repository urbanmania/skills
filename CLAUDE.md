# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of Claude Code agent skills — pure Markdown, no build, lint, or test commands. Each skill is a folder containing a `SKILL.md` (YAML frontmatter + instructions) and an optional `references/` folder with templates and supporting docs that are read on demand.

To try a skill locally, copy its folder into `~/.claude/skills/` (or clone the whole repo there).

## Authoring conventions

- **SKILL.md frontmatter** carries `name` and a `description` written for skill-routing: it states what the skill does, lists concrete trigger phrases, and includes explicit "Do NOT use when" guidance. Follow this pattern for new skills.
- **Progressive disclosure**: keep the SKILL.md body lean (workflow, principles, constraints) and push templates, prompt scaffolds, rubrics, and worked examples into `references/`. Each SKILL.md ends with a list of its reference files and when to read them.
- **No per-skill READMEs** — intentional. `SKILL.md` is the skill's documentation; GitHub renders it inline. The top-level `README.md` holds the skill index and install instructions (update its table when adding a skill).
- UK English spelling throughout (synthesise, behaviour, licence).

## Cross-skill architecture

`persona-creator` and `persona-design-review` form a producer/consumer pair with a deliberate contract split:

- **`persona-creator`** emits the on-disk shape: one Markdown file per persona named `NN-slug.md`, display name as the H1, free-prose body with no YAML frontmatter, plus a cohort `README.md` carrying cross-persona synthesis (never itself a persona). The output contract lives in its SKILL.md Stage 3.
- **`persona-design-review`** owns discovery: `references/persona-discovery.md` defines what counts as a persona file vs cohort context, slug derivation, and subset-axis selection. The producer's SKILL.md explicitly defers to it — don't duplicate discovery/slug rules on the producer side.

When changing either skill's file format or naming rules, update both sides of the contract (and `persona-creator/references/persona_template.md`, which owns the persona section structure).

`persona-design-review` references a worked example output (the SJÁ/BankBank kids-banking set under `specs/personas/`) that lives in a consuming project, not in this repo — it is a quality-bar reference, not a path that resolves here.

`agent-character-creator` is standalone; its core invariant is the SOUL/IDENTITY split (decision-making vs presentation), enforced by the persona-swap test described in its SKILL.md.
