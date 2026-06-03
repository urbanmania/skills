# Combined sponsor report — HTML template

The combined report is a single self-contained HTML file written to `<output_folder>/combined-report.html`. It is sponsor-grade: decision-oriented, scoreable, concrete. Inline CSS only, max-width 880px, no external assets, prints cleanly on A4.

## Inputs

The synthesis consumes only the **structured returns** from the persona sub-agents — not the per-persona HTMLs. The returns are guaranteed to contain: persona one-liner, top 3 findings, winning + runner-up, single most important recommendation, real-user-testing risks.

Do not re-read the per-persona HTMLs unless a return is malformed.

## Section order — fixed

The section *order* is fixed. The *content* of comprehension and comparison tables is generated from the review goal and the approved question battery — not from a hardcoded schema.

1. **Executive summary** — 3–5 paragraphs. Lead with the answer. Name the overall winner and the named transplants it needs from the others.
2. **Overall winner** — small score grid (one card per artifact) showing outright wins / runner-up votes per artifact.
3. **Least successful artifact** — name it; explain why the cohort consensus reads it as weakest.
4. **What works across the artifacts** — bulleted, specific, cite artifact letters/labels.
5. **What does not work** — bulleted, specific, cite artifact letters/labels.
6. **Trust reactions table** — one row per artifact. Columns: Artifact, Trust verdict (pill), Why.
7. **Tone / register observations** — bulleted, per-artifact observations on whether the artifact reads as the right age, formality, or seriousness for the audience.
8. **Comprehension table** — one row per dimension. Columns: Dimension, then one column per artifact, then Notes. *Rows are derived from the question battery:* each Block-2 comprehension-style question becomes a candidate row. Pick 4–8 rows that span the dimensions the user named in the review goal. Use pills: Best / OK / Ambiguous / Hidden / Fails.
9. **Artifact-by-artifact comparison** — table with rows: Strongest move, Weakest move, Best for, Worst for, Trust, *Carries to <next stage>* (where `<next stage>` is the natural next-state question for the domain — for kids-banking it was "Carries to 13+"; for B2B it might be "Scales to enterprise users"; for an onboarding flow it might be "Works without prior context").
10. **Persona-by-persona highlights** — one row per persona. Columns: Persona (+ profile shorthand), Winner, Runner-up, "The one thing".
11. **Where personas agree** + **Where personas disagree** — two short bulleted lists. The agree list is the safest evidence to act on now.
12. **Recommended direction** — ordered list. Concrete and hybrid-aware. Each item names which artifact contributes the pattern.
13. **Specific changes before next round** — three buckets: Must-fix, Should-fix, Nice-to-have.
14. **Risks and open questions to validate with real users** — numbered list. Each item is a question for the next real-user round, not a decision.
15. **Confidence note** — distinguish strong simulated findings (5–6 persona agreement) vs persona-specific reactions vs inferences.

### Conditional sections

- **Task-completion table** — insert between sections 5 and 6 if the review goal was *Task walkthrough*. One row per persona, one column per artifact, cells = Completed / Partial / Blocked, with a Notes column for the step where the persona broke down.
- **Recommendation strength** — if the cohort is small (≤ 4 personas) or split widely on the winner, replace section 2's score grid with a "no clear winner" call-out and lead the recommendation section with the open question rather than a pick.

## Mode variations

### Spec mode

Replace sections 2–9 of the Visual-mode structure with a **gap register**, formatted as a single table per severity bucket. Section order for Spec mode:

1. Executive summary (1–3 paragraphs; what's the spec, who's it for, how it lands).
2. **Blockers** — table of all Blocker-severity findings. Columns: ID, Title, Raised by, What the spec didn't say, Suggested change.
3. **Majors** — same table shape.
4. **Minors** — same table shape, collapsed by default if more than 10 rows.
5. **Out-of-scope** — list, one line each, with a note that these are real product questions to triage separately.
6. **What this spec gets right** — bulleted, specific. Surface the wins; the gap register alone is depressing.
7. **Persona-by-persona highlights** — one row per persona. Columns: Persona, Verdict (would-this-work-for-me), The one change they want.
8. **Recommended changes before the next spec iteration** — three buckets: Must-fix, Should-fix, Nice-to-have. Mostly Blockers/Majors map to Must-fix.
9. **Risks and open questions to validate with real users**.
10. **Confidence note**.

Severity definitions and clustering rule are in `severity-rubric.md`.

### Live mode

Live mode runs Visual mode against a `drive-sim`-captured screenshot sequence. The combined report uses the Visual structure with one addition:

- **Step-by-step task completion table** — between sections 5 and 6. Rows: task steps in tap order. Columns: one per persona, plus a Notes column for shared friction. Cells: ✓ / ~ / ✗ with the persona's reasoning.

Include the captured screenshot filenames (in tap order) at the bottom of the report as an appendix so the reader can replay the sequence.

## Domain vocabulary

The Visual-mode template uses kids-banking vocabulary ("babyish", "too young", "pink kills trust") in places. The orchestrator must **choose the right vocabulary for the domain at intake**. For a B2B product: "amateur", "consumer-grade", "cluttered". For a meditation app: "noisy", "busy", "preachy". For a fintech with adult users: "untrustworthy", "fee-anxious", "over-promised". Generic "engaging / intuitive" language is banned. This is the canonical statement of the domain-vocabulary rule for this skill.

## CSS scaffold

Use this as a starting point. Keep colours muted; this is a sponsor document, not a marketing page.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>{{PRODUCT}} — simulated design review · Sponsor report</title>
<meta name="viewport" content="width=device-width,initial-scale=1">
<style>
  :root {
    --ink: #0f1419;
    --muted: #5b6470;
    --rule: #d7dbe0;
    --bg: #fdfcf8;
    --pill: #f1efe7;
    --good: #2f7a3a;
    --bad: #b03b2f;
    --warn: #b07a2f;
    --accent: #1d3f73;
  }
  * { box-sizing: border-box; }
  body { margin: 0; background: var(--bg); color: var(--ink);
    font: 16px/1.55 -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif; }
  main { max-width: 880px; margin: 0 auto; padding: 48px 28px 96px; }
  header.title { border-bottom: 2px solid var(--ink); padding-bottom: 18px; margin-bottom: 28px; }
  header.title .eyebrow { text-transform: uppercase; letter-spacing: 0.12em; font-size: 12px; color: var(--muted); font-weight: 600; }
  h1 { font-size: 30px; margin: 6px 0 4px; line-height: 1.15; }
  h2 { font-size: 21px; margin: 44px 0 10px; padding-bottom: 4px; border-bottom: 1px solid var(--rule); }
  h3 { font-size: 16px; margin: 22px 0 6px; }
  h4 { font-size: 14px; text-transform: uppercase; letter-spacing: 0.08em; color: var(--muted); margin: 18px 0 6px; }
  ul, ol { padding-left: 22px; }
  li { margin: 3px 0; }
  table { width: 100%; border-collapse: collapse; font-size: 14px; }
  th, td { text-align: left; padding: 8px 10px; border-bottom: 1px solid var(--rule); vertical-align: top; }
  th { background: var(--pill); font-weight: 600; }
  .callout { background: #f5f1e3; border-left: 4px solid var(--accent); padding: 12px 16px; margin: 14px 0; border-radius: 0 6px 6px 0; font-size: 15px; }
  .pill { display: inline-block; padding: 2px 8px; border-radius: 999px; background: var(--pill); font-size: 12px; font-weight: 600; }
  .pill.good { background: #d8ecd9; color: var(--good); }
  .pill.bad { background: #f4d8d4; color: var(--bad); }
  .pill.warn { background: #f4e4cc; color: var(--warn); }
  .scorecard { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin: 14px 0 6px; }
  .scorecard .card { border: 1px solid var(--rule); padding: 12px; border-radius: 8px; background: white; }
  .scorecard .score { font-size: 24px; font-weight: 700; color: var(--accent); margin: 2px 0; }
  .scorecard .small { font-size: 12px; color: var(--muted); }
  @media (max-width: 720px) { .scorecard { grid-template-columns: 1fr 1fr; } }
</style>
</head>
<body><main>
  <!-- title block, then sections 1–15 -->
</main></body>
</html>
```

If the number of artifacts is not four, rescale the score grid columns (`grid-template-columns: repeat(N, 1fr)`).

## Tone

- Lead with the answer; rationale follows.
- Cite artifact letters/labels. Never generic "the design".
- Quote a persona where it adds force; avoid more than one quote per paragraph.
- Use pills sparingly — they exist to enable a fast skim of trust, comprehension and task-completion tables only.
- Distinguish strong findings from persona-specific reactions from inferences. The confidence note in section 15 is mandatory.
- Adapt vocabulary to the product domain — see the **Domain vocabulary** section above.

## Worked example

`specs/personas/sja-hopur/review/combined-report.html` is a known-good output of this template — one kids-banking instance. Reproduce its *structure* (the scoreable sections, the comprehension and comparison tables, the confidence note), not its domain vocabulary.
