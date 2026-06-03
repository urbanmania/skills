# Skills

A collection of skills for building and shaping AI agents.

---

## Skills in this repo

| Skill | What it does |
|---|---|
| [`persona-creator`](persona-creator/) | Generates research-grounded user personas for any product domain through a clarify → research → synthesise → guide workflow. |
| [`persona-design-review`](persona-design-review/) | Runs a parallel, in-character persona review of specs, mockups, or live apps and produces per-persona plus combined HTML reports. |
| [`agent-character-creator`](agent-character-creator/) | Interviews you, then produces a complete agent definition — `SOUL.md`, `IDENTITY.md`, `USER.md`, `TOOLS.md`, `ROUTINES.md` — for agent systems such as OpenClaw. |

`persona-creator` and `persona-design-review` are a producer/consumer pair: the first writes a persona set to disk, the second loads that set and reviews artifacts against it. Each also works on its own.

---

## persona-creator

Produces research-grounded user personas for design, prioritisation, user testing, or stakeholder alignment — in any product domain (fintech, healthcare, B2B, consumer). It enforces a four-stage workflow:

1. **Clarify** — pins down the product, target demographic, language availability, and intended use before anything is written
2. **Research** — investigates persona best practice, the product domain, and the local context of the target demographic
3. **Synthesise** — writes the personas, labelling every claim as evidence, assumption, or invention
4. **Guide** — adds cross-persona themes, differences, product opportunities, risks, and suggested next research steps

The defining feature is the evidence/assumption/invention separation: invented details are never presented as fact, and the research basis is always visible. Sensitive groups (children, patients, vulnerable users) get explicit consent, safety, and accessibility dimensions.

Output is one Markdown file per persona (`NN-slug.md`) plus a cohort `README.md` carrying the cross-persona synthesis — the exact on-disk shape `persona-design-review` consumes.

Use it when you need new personas created. Editing or critiquing personas you already have is out of scope.

---

## persona-design-review

Dispatches one parallel sub-agent per persona to review a user-facing artifact in character, then synthesises a sponsor-grade combined report. It handles three input modes:

| Mode | Input | Output emphasis |
|---|---|---|
| **Spec** | Written PRD / feature brief / RFC | Gap register with Blocker / Major / Minor severity — what the spec didn't say |
| **Visual** | PDFs, PNGs, HTML mockups, screenshots | Comparative ranking, comprehension table, hybrid recommendation |
| **Live** | Running web page or simulator app | Task-completion table from a captured screenshot walkthrough |

Each persona reviews the artifacts in a counter-balanced order to reduce primacy bias, answers a question battery tailored to the review goal at intake, and writes its own HTML report in its own voice (and language). The orchestrator then clusters the findings into a single self-contained combined HTML report plus a short in-chat summary.

It is a simulation, not real user research — use it as a first-pass sense check before booking real participants. Personas come from `persona-creator`; if no set exists yet, run that skill first. Live mode additionally pairs with a `drive-sim` skill (not included in this repo) to capture screenshots.

---

## agent-character-creator

Builds a fully formed AI agent definition through a structured interview — made for agent systems such as [OpenClaw](https://openclaw.ai) that read their character and configuration from markdown workspace files. It asks about purpose, persona, tools, and recurring workflows in two or three rounds of multiple-choice questions, researches any known fictional or real-world character before writing, then delivers up to five markdown files ready to drop into any agent framework:

- **`SOUL.md`** — decision-making values and hard limits: what the agent will and won't do
- **`IDENTITY.md`** — character presentation: voice, speech patterns, signature phrases, response checklist
- **`USER.md`** — who the agent serves: context, preferences, standing instructions
- **`TOOLS.md`** — what tools the agent can use, when, and the non-negotiable prohibitions
- **`ROUTINES.md`** — recurring procedures such as daily briefings or weekly reports

The core discipline is the SOUL/IDENTITY split: decision logic and character flavour are kept strictly apart, tested line by line with a persona-swap test. Signature phrases are sourced from research or supplied by you — never invented. Output is platform-agnostic (Claude, GPT, Gemini, custom runtimes).

Use it when you want to build a new agent or assistant, give an AI a persona, or document an agent's tools and constraints.

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
