---
name: persona-design-review
description: Dispatches one parallel sub-agent per persona for an in-character UX review of any user-facing artifact — written specs/PRDs, design mockups (PDF/PNG/HTML), screenshot sets, or live web/simulator runs — producing a per-persona HTML report plus a sponsor-grade combined HTML report. Domain-agnostic; review goal, question battery, and optional task script are decided at intake. Use when the user wants in-character persona reactions to anything user-facing — phrases like "review this spec with the personas", "have the personas review these designs", "run a persona-based design review", "persona-test this PRD", "stress-test these mockups against the personas", "what would these users think of this flow", "have the personas try to complete this task", or `/persona-design-review`. Do NOT use for engineering critique (architecture, data model, ADRs), code review, or automated accessibility audits done by tooling.
---

# Persona design review

Drive a parallel persona-led review of any user-facing artifact — a spec, a set of mockups, a screenshot batch, or a live running app. Each persona reads its profile, evaluates the artifacts in a counter-balanced order in character, and writes a structured HTML review. The orchestrator then synthesises a sponsor-grade combined HTML report.

This is a simulation, not real user research. Use as a first-pass sense check before booking real participants.

## When to use

- The user has a written spec / PRD / feature brief and wants to know what user-side gaps exist.
- The user has 2+ design variants (PDF, PNG, HTML, mockup) and wants comparative persona reactions.
- The user has a single screen or screenshot batch and wants comprehension/trust feedback.
- The user has a running app or web page they want personas to walk a task on.
- The user wants a sponsor-ready document recommending a direction.

Personas are produced by the `persona-creator` skill, which writes one Markdown file per persona plus a cohort `README.md`. If no persona set exists yet, run `persona-creator` first.

## Input modes

The skill picks one of three modes from the artifact set. Mode shapes the dispatch, the question battery shape, and the combined-report emphasis.

| Mode | Artifact | Output emphasis |
|---|---|---|
| **Spec** | `.md` PRD / feature brief / RFC / implementation plan | Gap register with Blocker / Major / Minor severity. Personas surface what the spec didn't say. |
| **Visual** | PDFs, PNGs, HTML mockups, design exports | Comparative ranking, comprehension table, hybrid recommendation. Sponsor-grade HTML. |
| **Live** | Running web page (URL) or simulator/emulator app | Pair with `drive-sim` to capture a task screenshot sequence, then run Visual mode on the captures. |

Detection rule: if every input file is `.md` and the persona file paths are not amongst them, treat as Spec. If inputs are PDFs / images / HTML, treat as Visual. If the user names a URL or asks personas to drive a running app, treat as Live and start with `drive-sim` capture. Mixed sets are allowed — the orchestrator picks the dominant mode and notes the secondary inputs as context.

## Intake — what the skill asks before running

The orchestrator runs **two `AskUserQuestion` rounds**. Round 1 settles inputs and scope; Round 2 settles what the personas should do. Do not collapse the two — Round 2's framing depends on Round 1's domain. If the user has pre-supplied any of these in the invocation, skip the corresponding question.

### Round 1 — inputs and scope

1. **Where are the personas stored?** Folder of `.md` files (and optional `README.md`), an explicit list, or a glob. Default suggestion: `specs/personas/`.
2. **What's being reviewed?** A folder, a single file, an explicit list, a glob, or a URL/simulator app description. (Free text — the orchestrator detects the mode from this answer.) No assumed default — ask plainly.
3. **Persona subset.** Multi-select. Offer "All personas" and "Custom pick" always, plus subset axes **derived from the discovered set** (the dimensions it actually varies on — life-stage/role, language, location, household, etc.). Do not present a fixed menu. See `references/persona-discovery.md`.
4. **Report scope.** Two options:
   - Per-persona HTML reports **plus** combined HTML (recommended; default).
   - Combined HTML only.
5. **Output folder.** Default suggestion: a sibling `review/` folder next to the inputs. Create it if missing. Re-running the same persona set against a different artifact batch into the same folder overwrites the prior reports — when past runs matter, give each session its own folder (e.g. `review/<artifact-set>/`).

### Round 2 — review goal, question battery, optional task

After Round 1, before dispatch, ask (batch into `AskUserQuestion` calls of up to four):

1. **What is this product / domain?** One-line description used to brief the sub-agents (e.g. "a kids fintech app", "a B2B HR onboarding portal", "a meditation app for adults"). Default: infer from the artifacts and read it back to the user for confirmation.
2. **What is the review goal?** Single-select. Options:
   - **Reaction** — first impressions, comprehension, trust, aesthetics, would-they-use-it. The default for Visual mode.
   - **Gap analysis** — find what's unclear, missing, age-inappropriate, or wrong for the persona. The default for Spec mode.
   - **Task walkthrough** — personas attempt a specific task on each artifact. The default for Live mode and a strong option for Visual mode.
   - **Comparative pick** — personas rank the artifacts and justify the pick. Use for shortlist decisions.
   - **Custom** — user types their own focus statement; the orchestrator builds a battery from it.
3. **Emphasis (optional, multi-select; default: none).** Which dimensions should the personas weight? Accessibility / cognitive load, Onboarding comprehension, Trust & safety, Pricing / value, Longitudinal retention, Competitive vs a named rival, Localisation / second language. Most runs leave this empty; it only slants the *Generate from review goal* battery (inert for the other two sources).
4. **Question battery source.** Single-select:
   - **Generate from review goal** — orchestrator drafts a domain-appropriate battery and shows it for one-tap approval before dispatch. The default for any non-kids-banking domain.
   - **Custom file** — user provides a path to a `.md` battery; orchestrator uses it verbatim.
   - **Pre-built kids-banking battery (BankBank example)** — the SJÁ battery. Only valid when domain is kids-banking; warn otherwise.
5. **Task script** — only ask if review goal is *Task walkthrough*. Free text: the specific task to attempt (e.g. "Send 500 kr. to a friend", "Set up a recurring savings goal", "Cancel your subscription").
6. **External baseline (optional).** A competitor product or the tool the persona already uses, to compare each artifact against. Leave empty for a self-contained review.

Save the approved battery to `<output_folder>/_battery.md` for traceability.

## Workflow

### Step 1 — Discover

Read every persona file. Read any `README.md` alongside the personas as cohort context (do not treat it as a persona; the persona files are authoritative for their respective sub-agents). Personas are deliberately scenario-free — they describe the user, not the product — so a finding is always about the artifact, never about the persona.

Mode-specific pre-read:

- **Spec mode**: the orchestrator reads the spec(s) in full and extracts feature name, one-paragraph summary, target audience, primary flows, and open questions. Show this to the user and confirm before proceeding. If the spec is internally inconsistent about the audience, that itself is a finding — record it.
- **Visual mode**: the orchestrator reads each artifact for context. PDFs require `pdftoppm` (poppler) — check with `which pdftoppm`; instruct `brew install poppler` on macOS if missing. Do not silently skip PDFs.
- **Live mode**: pair with `drive-sim` to capture a task-step sequence of screenshots, label them in tap order, then continue in Visual mode against the captured set. Do not attempt to drive the simulator from inside a persona sub-agent.

If personas or artifacts are absent or empty, ask the user — do not fabricate.

### Step 2 — Counter-balance the review order

Each persona reviews all artifacts. Assign each persona a distinct review order to reduce primacy bias. See `references/review-order-counterbalance.md`. State the order inside each persona report.

For Spec mode with a single spec file, there is no order to balance — skip this step and note it.

### Step 3 — Dispatch one parallel sub-agent per persona

In a **single message**, launch one `Agent` per persona with `run_in_background: true`, `subagent_type: general-purpose`. Brief each sub-agent with:

- Path to its persona file (sub-agent reads it — never paraphrase)
- Path to the cohort README (optional, marked as context, not as the persona itself)
- Paths to every artifact
- Its assigned counter-balanced review order
- The product domain one-liner from Round 2
- The review goal
- The approved question battery (verbatim)
- The task script (only if review goal is *Task walkthrough*)
- The placeholder-handling rule (only when artifacts have placeholder user data)
- The output HTML path the sub-agent must write to
- The structured return-summary contract

The full prompt template is in `references/per-persona-prompt.md`.

Wait for every background sub-agent to return its structured summary before running synthesis (Step 4). Optionally track progress with your task tool if one is available.

Cost guardrail: if persona count × artifact count exceeds ~60, confirm before dispatching.

### Step 4 — Synthesise the combined report

After every sub-agent returns its summary and writes its HTML to disk, generate the combined report in HTML using `references/combined-report-template.md`. Section *order* is fixed; section *content* is derived from the mode, review goal, and approved question battery — not from a hardcoded schema.

- **Visual mode** → comparison + scorecard emphasis (the SJÁ pattern).
- **Spec mode** → gap register with severity (Blocker / Major / Minor / Out-of-scope), clustered across personas. See `references/severity-rubric.md`.
- **Live mode** → task-completion table per persona × per step, plus the Visual-mode comparison if multiple variants were captured.

Content is grounded in the structured returns from the sub-agents (do not re-read the per-persona HTMLs — the structured returns are the contract).

The combined report is a single self-contained HTML file, inline CSS, max-width 880px, prints cleanly on A4, no external assets. Aim for sponsor-grade: scoreable, decision-oriented, concrete.

### Step 5 — Print the in-conversation summary

After the report is written, surface in chat:

- Output folder path
- Mode-appropriate headline (winner + runner-up for Visual; blocker count for Spec; task-completion summary for Live)
- 3 cross-cutting agreements (claims 5+ of N personas converge on)
- Single most important recommendation
- 1–2 biggest unanswered questions for real-user testing

Keep this in-chat summary under ~250 words. Full reasoning lives in the HTML.

## Quality bar (enforced via sub-agent prompts)

- Persona is **adopted from the file**, not invented. Anything not in the persona file is marked `[inference]`.
- Reactions are **concrete**. Ban: "intuitive and engaging". Allow: "Rafn reads the green plus as 'money in this month' because his older brother's app shows inflows that way."
- Personas write in their own voice. A 9-year-old says "I don't get this", not "this lacks clarity in the empty-state copy". Language fidelity matters — Icelandic personas in Icelandic, Polish in Polish, etc. The orchestrator-side report normalises to English with quotes preserved in source language.
- For Spec mode: if a persona would have a question, the question is itself the finding — *do not invent an answer*. The point is to surface what the spec didn't say.
- Severity (Spec mode) is assigned by the orchestrator after clustering — never by individual personas.

## Operating constraints

- Sub-agents must **write HTML to disk** and return a structured summary — never paste full HTML back into the chat.
- All sub-agents launched in a single message (parallel) with `run_in_background: true`, `subagent_type: general-purpose`.
- Honour the BankBank worktree workflow — write all output inside the current worktree.
- One file per persona, always. Never combine.
- Produce the combined report only after every per-persona file is saved and verified on disk.

## Reference files

- `references/question-battery.md` — the generation rule (the default path), custom-file format, task-walkthrough addendum, and the pre-built kids-banking battery (BankBank example).
- `references/per-persona-prompt.md` — the full sub-agent prompt template.
- `references/combined-report-template.md` — HTML structure, CSS scaffold, section order for the sponsor report (with mode-specific variations).
- `references/review-order-counterbalance.md` — how to assign distinct review orders across personas.
- `references/persona-discovery.md` — how to scan the personas folder, accept ad-hoc paths, and apply cohort-axis subset selection.
- `references/severity-rubric.md` — severity definitions and clustering rule for Spec-mode gap registers.

## Reference output (quality bar)

A known-good Visual-mode output (decision-oriented, scoreable, concrete) to reproduce is the SJÁ hópur set below — one worked example of a kids-banking run, not the only valid shape. Reproduce its *structure*, not its domain vocabulary.

- `specs/personas/sja-hopur/review/combined-report.html`
- `specs/personas/sja-hopur/review/persona-{rafn,roisin,arthur,anna,baldur,brak}-review.html`

## Caveats

This is a model-driven simulation. It is most useful for catching obvious failures before booking real participants, comparing variants where the difference is visible to any reasonable user, surfacing audience-mismatch gaps in specs, and generating questions for the next real-user round. It is not a substitute for in-person observation, motor-skill testing, accessibility audit tooling, or engineering critique.
