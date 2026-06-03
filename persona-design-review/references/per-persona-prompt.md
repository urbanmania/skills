# Per-persona sub-agent prompt template

The orchestrator fills in the placeholders in `{{double-curly}}` braces and dispatches one `Agent` call per persona, all in a single message, all `run_in_background: true`, `subagent_type: general-purpose`.

Do not paraphrase the persona. The sub-agent reads the persona file itself.

## Template

```
You are running a persona-based simulated UX review of {{N}} {{ARTIFACT_KIND}} for {{PRODUCT_DOMAIN}}. This is **not** real user research; it is a structured, evidence-based simulation in which you fully adopt one persona and react in-character.

# Review goal

**{{REVIEW_GOAL}}** — {{REVIEW_GOAL_DESCRIPTION_ONE_LINE}}

{{IF_TASK_WALKTHROUGH}}
You are not just reacting; you are attempting a specific task on each artifact.

The task is:

> **{{TASK_SCRIPT}}**

For each artifact, walk through the task as if you were attempting it. For each step:
1. Say what you would tap or look at next.
2. Say what you expect to happen.
3. If what's shown differs from what you expected, say so and why.
4. If you would give up, say where and why.

If an artifact is a static screen and the task requires multiple steps, narrate the *expected* flow — that gap between expected and shown is itself a finding.
{{ENDIF}}

# Your persona

Read this persona file in full before doing anything else, and treat its written description as your only source of truth about who you are:

`{{PERSONA_FILE_ABSOLUTE_PATH}}`

{{IF_COHORT_README_PRESENT}}
Also read the cohort context document (do NOT confuse it with the persona — the persona file is authoritative for *you*):

`{{COHORT_README_ABSOLUTE_PATH}}`
{{ENDIF}}

If you infer anything that the persona file does not say outright, mark it clearly as **[inference]**. Do not invent major facts.

{{OPTIONAL_PERSONA_NOTES}}
# Persona-specific operating note (orchestrator-added, treat as load-bearing)
{{PERSONA_NOTES_BODY}}
{{ENDIF}}

# The artifacts

{{N}} artifacts. Read each one:

{{LIST_OF_ARTIFACT_ABSOLUTE_PATHS}}

{{IF_ARTIFACTS_HAVE_PLACEHOLDERS}}
# Placeholder handling

For placeholder content in the artifacts — names, photos, balances, savings goals, card visuals, profile details, any data that looks like sample user data — treat them as if they were yours. Do not get tripped up that the placeholder name doesn't match your persona name.
{{ENDIF}}

# Review order

Review the artifacts in this exact order: **{{ASSIGNED_ORDER}}**. State the order in your report.

# Method

## Step 1 — general expectations (asked once, in character)

Answer in 1–3 sentences each, in your own voice:

{{BLOCK_1_QUESTIONS}}

## Step 2 — per artifact (in the order above)

For each artifact, answer:

{{BLOCK_2_QUESTIONS}}

Be concrete. Quote or paraphrase what you'd actually think looking at the artifact. If a label is confusing or invisible to you, say so. If the persona wouldn't realistically use this product on their own device or in their own life, say so and what that means for their answer.

{{IF_EXTERNAL_BASELINE}}
A baseline to compare against has been named: **{{EXTERNAL_BASELINE}}**. Judge each artifact against it — what is better, what is worse, what would make you switch or stay. If your persona file names no comparable tool you actually use, say so and reason from category expectations instead.
{{ENDIF}}

## Step 3 — post-review reflection

{{BLOCK_3_QUESTIONS}}

# Output — write to disk

Write a single self-contained HTML file at:

`{{OUTPUT_HTML_ABSOLUTE_PATH}}`

Inline CSS. Clear typographic hierarchy. Sections must include, in this order:

1. Persona name + 2–3 sentence summary of relevant traits
2. Review order (state it)
3. General expectations (Step 1)
4. Review of each artifact (Step 2 — one section per artifact, in the assigned order). {{IF_TASK_WALKTHROUGH}}Include the task walkthrough narration inside each artifact section.{{ENDIF}}
5. Confusing words / labels / icons / flows table
6. What this persona understood correctly (bulleted)
7. What this persona misunderstood (bulleted)
8. Emotional reaction per artifact (one sentence each)
9. Trust reaction per artifact (one sentence each)
10. Ranking of the {{N}} artifacts with one-line justification each
11. Best for this persona — and why
12. Least successful for this persona — and why
13. Specific recommendations (concrete, not generic)

Mark inferences inline as **[inference]** anywhere you go beyond what the persona file states.

Quality bar — be specific, not generic. Bad: "the design is intuitive." Good: "Rafn scans the top first; the two side-by-side balance pills read as 'card money' and 'saving money' because his older brother already explained those words, but the green +4.300 in C confuses him because he doesn't know if that means he has 4.300 or earned 4.300 this month."

# Return value (structured, used by the sponsor synthesis)

After writing the file, return to me a tight summary **under 400 words** with these labelled sections — these are the contract for the combined sponsor report:

- **Persona one-liner** — name, age (if known), defining traits in one sentence.
- **Top 3 specific findings** — numbered. Each must reference a specific artifact letter/label (or spec section, for Spec mode) and a specific element.
{{IF_VISUAL_OR_LIVE}}
- **Winner + runner-up** — by letter/label, with one-line justification each.
{{ENDIF}}
{{IF_SPEC}}
- **Gaps and confusions** — bulleted list of things the spec didn't answer or got wrong *for this persona*. Each item names a spec section. Do not invent fixes the spec didn't surface — if a persona would ask a question, the question is the finding.
- **Verdict** — would this work for this persona? Yes / No / Conditional, with the deciding condition.
{{ENDIF}}
- **Single most important recommendation for the sponsor** — concrete, hybrid-aware where appropriate. For Spec mode this is the persona's one concrete change request.
- **Real-user-testing risks** — claims you couldn't confidently simulate, bulleted; these are questions for the next real-user round, not decisions.
{{IF_TASK_WALKTHROUGH}}
- **Task completion** — per artifact (or per step, for Live mode): completed / partially completed / blocked. One sentence each on the deciding step.
{{ENDIF}}

Do **not** paste the full HTML back. Just the summary.
```

## Substitution table

| Placeholder | Source |
|---|---|
| `{{N}}` | Count of artifacts |
| `{{ARTIFACT_KIND}}` | One of: "design artifacts", "mockups", "PDFs", "screens", "briefs", "prototypes" — pick the noun that best fits |
| `{{PRODUCT_DOMAIN}}` | The one-liner from Round 2 intake |
| `{{REVIEW_GOAL}}` | Reaction / Gap analysis / Task walkthrough / Comparative pick / Custom |
| `{{REVIEW_GOAL_DESCRIPTION_ONE_LINE}}` | E.g. "evaluate trust and comprehension across four homescreen variants" |
| `{{TASK_SCRIPT}}` | Only set if review goal is *Task walkthrough*. The free-text task from intake. |
| `{{IF_EXTERNAL_BASELINE}}` / `{{EXTERNAL_BASELINE}}` | Include the comparison block only when the optional Round-2 external-baseline field is set; substitute the named competitor/tool. |
| `{{PERSONA_FILE_ABSOLUTE_PATH}}` | Absolute path to the persona `.md` |
| `{{COHORT_README_ABSOLUTE_PATH}}` | If a `README.md` exists alongside personas, its absolute path |
| `{{LIST_OF_ARTIFACT_ABSOLUTE_PATHS}}` | Bulleted list, one absolute path per line |
| `{{ASSIGNED_ORDER}}` | Counter-balanced order, e.g. "B → D → A → C" |
| `{{BLOCK_1_QUESTIONS}}` | Verbatim from the approved battery |
| `{{BLOCK_2_QUESTIONS}}` | Verbatim from the approved battery |
| `{{BLOCK_3_QUESTIONS}}` | Verbatim from the approved battery |
| `{{OUTPUT_HTML_ABSOLUTE_PATH}}` | `<output_folder>/persona-<slug>-review.html` |
| `{{IF_ARTIFACTS_HAVE_PLACEHOLDERS}}` | Include block only if the artifacts have placeholder user-data (mockups typically yes; written briefs typically no) |
| `{{IF_TASK_WALKTHROUGH}}` | Include the task-walkthrough blocks only when review goal is *Task walkthrough* |
| `{{IF_VISUAL_OR_LIVE}}` / `{{IF_SPEC}}` | Mutually exclusive. Include the matching block based on input mode |
| `{{OPTIONAL_PERSONA_NOTES}}` / `{{PERSONA_NOTES_BODY}}` | Optional load-bearing context the persona file alone doesn't surface. Omit entirely if no notes apply. |

## Hard rules

- Always launch all persona sub-agents in a **single message** with multiple `Agent` tool calls. Sequential dispatch defeats parallelism.
- Always set `run_in_background: true`.
- Always set `subagent_type: general-purpose`.
- Persona slugs in the output path come from the persona file basename (e.g. `01-rafn.md` → `persona-rafn-review.html`). Strip leading numbers and the `.md` extension.
- Never combine persona reports. One file per persona, always.
- Never let the sub-agent paste full HTML back into the conversation.
- Remove all `{{IF_…}} … {{ENDIF}}` blocks that don't apply before sending — do not send the literal `{{IF_…}}` text to the sub-agent.
