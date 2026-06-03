# Persona discovery

The skill accepts personas from any folder. Default suggestion: `specs/personas/`.

## What counts as a persona file

A persona file is a `.md` whose body describes a single, named individual — age, location, household, language, behaviour, and their relationship to the product area. This is the shape `persona-creator` emits (its `references/persona_template.md` owns the section structure): a free-prose body with the persona's display name as the H1 (`# Sigríður Anna Magnúsdóttir`) and age in an `## Age and location` section. There is **no YAML frontmatter** by default — take the name from the first H1, and age/location/language from the prose and the sibling cohort README. If a file does carry frontmatter, treat it as an optional override and read `name`/`age`/cohort fields from it.

A file is **cohort context, not a persona**, when any of these hold — filter it out of the persona set automatically:

- It is named `README.md`, `INDEX.md`, or `CONTEXT.md`, or its filename begins with `_` or `.`.
- Its H1 is not a personal name, and its body is dominated by a roster table or links to other persona files rather than describing one individual.
- It is inside a subfolder the user didn't point at, unless they said "include subfolders".

If a `README.md` sits alongside the personas, treat it as **cohort context** — pass its absolute path to every sub-agent as supplementary reading, but never as the persona itself. The cohort README is also where subset axes come from (see below).

## Accepting input

The skill should accept any of the following:

1. **Folder path** — scan for `.md`, filter per the rules above, sort by filename.
2. **Explicit list** — comma- or newline-separated list of `.md` paths. Use as-is, in the order given. Do not filter.
3. **Glob** — e.g. `specs/personas/sja-hopur/*.md`. Expand, then filter.

If the discovered set is empty, ask the user before fabricating personas. Suggest the `persona-creator` skill if they want to generate some.

## Slug derivation for output filenames

Persona output paths use the form `<output_folder>/persona-<slug>-review.html`. Derive `<slug>` by:

1. Take the persona file basename without `.md`.
2. Strip any leading digit prefix and separator: `01-rafn` → `rafn`, `04-anna` → `anna`.
3. Lowercase, replace spaces with `-`, drop diacritics if the orchestrator can do so safely; otherwise keep them (`róisín` is fine if the filesystem accepts it — modern macOS/APFS does).

## Cohort-axis subset selection

After discovery, ask the user which subset of personas to use via `AskUserQuestion` (multi-select). **Derive the offered axes from the discovered set — do not present a fixed menu.** Two options are always available regardless of the data:

- **All personas** — every persona in the discovered set.
- **Custom** — list every persona with its key traits and let the user tick a subset.

Then offer **named subset axes only where their values are actually derivable from the loaded set** — i.e. present as columns in the cohort README's roster table, or in persona frontmatter if any exists. Scan the personas and README for the dimensions on which they genuinely differ — life-stage or role, language, location, household or organisational structure, accessibility or neurodivergence, experience level — and offer those. Never promise an axis the data can't support: if neurodivergence or income appears only as free prose (not a README column or a field), it is not a reliable filter — drop it or fall back to Custom.

For a **language** axis, distinguish the app-UI language the product ships in from a persona's home language where they differ — a persona whose home language is one thing but who uses the app in another reviews in the app's language. (For BankBank that is Icelandic / English / Polish; a Ukrainian-at-home persona reviews in the English fallback.) Useful for localisation stress.

Suggest a sensible default subset based on the inferred audience of the artifacts. Show the personas inline so the user sees what's loaded. If a chosen axis produces an empty set, surface that and ask them to broaden.

### Worked example — BankBank kids-banking set

For the `specs/personas/` set, the derivable axes are: life-stage (kids 9–12 / teens 13+ / parents), app language (Icelandic / English / Polish), location (capital area / non-capital), and household structure (shared custody / single parent / two-parent / blended / refugee — a column in that set's README). This is an instance of the derive-from-set method, not a standard menu — a fintech-for-adults set tagged differently would surface entirely different axes.

## Cost guardrails

- If the selected set exceeds 12 personas, confirm before dispatching — cost scales as personas × artifacts.
- If `personas × artifacts > 60`, suggest narrowing the persona set or splitting the run.

## What to surface before dispatch

After discovery, print to the conversation:

- Number of personas, with names listed
- Number of artifacts
- The counter-balanced order assignment (per the `review-order-counterbalance.md` rule)
- The output folder

Wait for confirmation if the user hasn't yet approved any of these.
