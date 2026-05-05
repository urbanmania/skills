# Skills

A collection of skills for building and shaping AI agents.

---

## Skills in this repo

| Skill | What it does |
|---|---|
| [`agent-character-creator`](agent-character-creator/) | Interviews you, then produces a complete agent definition — `SOUL.md`, `IDENTITY.md`, `USER.md`, `TOOLS.md`, `ROUTINES.md` — for any AI platform. Handles fictional, real-world, or neutral personas. |

---

## Install

Clone into your skills directory:

```bash
git clone https://github.com/<your-username>/skills.git ~/.claude/skills
```

Or copy a single skill folder into an existing skills directory:

```bash
cp -r agent-character-creator ~/.claude/skills/
```

For other Claude harnesses (Claude Desktop, Cowork, custom runtimes), follow that platform's instructions for installing skill directories.

---

## Repo structure

```
skills/
├── README.md                       — this file
├── LICENSE
└── <skill-name>/
    ├── SKILL.md                    — the skill itself (frontmatter + instructions)
    └── references/                 — optional: templates, examples, supporting docs
```

Per-skill READMEs are intentionally omitted. `SKILL.md` documents the skill — GitHub renders it inline when you click into the folder.

---

## Licence

MIT. See [LICENSE](LICENSE).
