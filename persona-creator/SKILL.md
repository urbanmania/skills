---
name: persona-creator
description: Generate research-grounded user personas for any product domain (fintech, healthcare, B2B, consumer) — for design, prioritisation, user testing, or stakeholder alignment. Use when the user wants to create new personas: requests like "create personas", "build personas for my app", "draft personas for user testing", or asking for archetypes, user profiles, or representative users even without the word "persona". The personas this skill writes are commonly consumed downstream by the persona-design-review skill. Do NOT use when the user already has finished personas they just want to apply, edit, or critique — only when new personas need to be created.
---

# Persona Creator

Produce research-grounded user personas through a fixed workflow — clarify, research, synthesise, guide — so product teams can use them for design, prioritisation, testing, and stakeholder alignment. Do not invent personas before the assignment and demographic are clear; that is the failure mode this workflow exists to prevent.

These personas are often consumed by the `persona-design-review` skill, which loads a set once and reviews many artifacts (specs, mockups, live apps) against it. Emit the on-disk shape that skill expects — see *Output contract* under Stage 3.

## Core principles

- **A persona is fictional but evidence-grounded.** The narrative is invented; the patterns underneath it must come from research. A persona written without research is not a persona — it is an assumption.
- **Distinguish what you know, what you assume, and what you invented.** This separation is the single most important thing this skill does. It is what makes the output trustworthy enough to drive real decisions.
- **Avoid generic archetypes and shallow demographic sketches.** A "busy mum aged 35" or "tech-savvy teen" is not a persona. Specificity, grounded in local and contextual reality, is what makes a persona useful.
- **One strong persona is more useful than four weak ones.** Recommend a primary persona; treat secondary personas as stress-tests of the primary, not as exhaustive coverage.
- **Personas exist to be used.** Every persona must include design implications and representative quotes, or the team will not reach for it during real decisions.

## Workflow overview

The skill enforces four stages, in order:

1. **Clarify** — gather product and demographic context before doing anything else
2. **Research** — investigate persona best practice, the product domain, and the target demographic
3. **Synthesise** — produce personas with explicit separation of evidence, assumption, and invention
4. **Guide** — provide cross-persona analysis and next-step recommendations

Do not skip stages. Do not collapse them. Each stage protects the next from a common failure mode.

---

## Stage 1: Clarify the assignment

Before researching anything, the product context and demographic must be clear enough that research has a target. If the user opens with "make me a persona for my app", the skill cannot proceed — there is nothing to research yet.

Use the `AskUserQuestion` tool to present clarifying questions as tappable options; fall back to concise, batched chat questions only if it is unavailable. Do not interrogate one question at a time.

Ask only enough to remove major ambiguity. If the user has already supplied some of this in their initial message, do not re-ask it — extract what is there and only ask what is genuinely missing.

### What to clarify

| Topic | Why it matters |
|---|---|
| **Product / feature / service** | The persona must be grounded in something specific. "An app" is not enough; "a banking app for pre-teens" is. |
| **Languages the product will be available in** | Always ask this. Language availability fundamentally changes the persona framing — a product available only in Icelandic implies a different user than one available in Icelandic and English, or in Icelandic, Polish, and English. It affects who the persona can realistically be, what their trust signals are, and which demographic gaps exist. Ask this even if it seems obvious; assumptions here are often wrong. |
| **Intended use of the personas** | Design review, spec review, feature planning, user testing, accessibility review, onboarding, stakeholder alignment — each implies a different emphasis. |
| **Number of personas** | One primary is the default. Three to five is a typical set. More than six dilutes focus. |
| **Primary demographic** | Age range, location, cultural context, household or life context, income or access constraints. |
| **Secondary demographics** | Groups who matter but are not the primary target. |
| **Output format and location** | One Markdown file per persona (the default — see *Output contract* under Stage 3), or a presentation/artifact if the user asks. Default location `specs/personas/`, or `specs/personas/<cohort-slug>/` for a distinct cohort. A single combined document is **not** a good default — the downstream review skill discovers one file per persona. |

### Language framing — why this matters

Once language availability is known, it shapes the persona set in concrete ways:

- **Single-language products** (e.g., only Icelandic) sharpen the persona to native or near-native speakers of that language. Non-speakers are excluded from the primary persona — but should be acknowledged as a known excluded group, not silently ignored.
- **Multi-language products** with a clear primary language and secondary translation imply different trust dynamics for primary vs secondary language users. The persona set should reflect both, with the secondary-language persona's experience being grounded in what translation does and does not solve.
- **Fully multilingual products** (e.g., Icelandic, English, Polish equally supported) imply a persona set spanning meaningful language communities in the target region.
- **English-only products** in non-English-speaking regions imply assumptions about user English fluency that often do not hold for the full demographic. Flag this as a constraint that narrows who the persona can be.

For products serving children, older adults, or users with lower literacy: reading level in the dominant language matters as much as language availability itself. Note this explicitly when relevant.

### When to push back

If the demographic is too broad ("women aged 18–65", "anyone who uses the internet", "consumers"), tell the user directly that this is too wide to produce useful personas. Ask them to narrow it. A persona representing "the average internet user" is the same as no persona at all.

If the product is too vague ("a productivity tool", "a social app"), ask for the specific use case the personas are meant to inform.

If the user asks for many personas (more than six), gently suggest fewer with stronger differentiation. Cite the rule of thumb: too many personas dilute focus and complicate decisions.

### When to handle with extra care

If personas are for **children, vulnerable populations, healthcare patients, people in crisis, or other sensitive groups**, build in extra dimensions:

- Consent and guardian involvement
- Privacy and data sensitivity
- Comprehension and literacy level appropriate to the group
- Safety, including digital safety
- Accessibility, including cognitive accessibility
- Trust dynamics with the institution offering the product

For children specifically: the persona is a child-led account or child-led experience, with an adult guardian as a secondary user. Do not flip this. The child is the primary user; the guardian is a stakeholder.

---

## Stage 2: Research before creating

After clarification, do real research. Three layers:

### Layer 1: Persona best practice

Quickly verify or refresh persona methodology relevant to the assignment. The summary in `references/persona_best_practice.md` covers the essentials and should be read before drafting. If the user has unusual requirements (for example, personas for accessibility audit, or for a regulated industry), supplement with web search.

### Layer 2: The product domain

Search for context relevant to the product or feature area. For a banking app, this includes how children relate to money at the target age, financial literacy stages, regulatory context. For a healthcare app, this includes patient journey research, condition-specific behaviour, clinical context. The depth here scales with the assignment — a quick prototype may need three searches; a flagship persona set may need fifteen.

### Layer 3: The target demographic and local context

This is the layer most often skipped, and the most consequential. A persona for "an Icelandic 11-year-old" must be grounded in Icelandic family structure, school system, language, money culture, device norms, and social context. A persona that is generic with the country name applied as a label is a failure mode this skill is specifically designed to prevent.

Search for:
- Family structure and household norms in the target region
- School or work context relevant to the age group
- Digital habits and device access for the demographic
- Cultural norms around the product domain (money, health, privacy, communication)
- Language and naming conventions
- Socioeconomic and geographic variation within the demographic

Prefer reputable sources: government statistics, academic research, established research organisations, national surveys, official policy documents. Be cautious of marketing content and AI-generated articles that compound stereotypes.

### Summarise the research

Before generating personas, present a concise research summary to the user — a few paragraphs covering what was found and what gaps remain. This serves two purposes: it lets the user correct course before personas are drafted, and it makes the evidence basis visible.

---

## Stage 3: Create the personas

### Separate evidence from assumption from invention

Distinguish **evidence** (research-backed, cited), **assumption** (extrapolated, labelled), and **invention** (fictional colour, labelled) for every claim — the discipline is defined in `references/persona_best_practice.md`. Label assumptions and inventions inline, never woven into prose as fact. A common pattern:

```markdown
She receives a weekly allowance of approximately 1,500 ISK.

> **Assumption:** No Icelandic national survey on children's allowances was identified.
> The figure is extrapolated from regional Nordic norms and local price context.
```

### Persona structure

Each persona follows the section structure in `references/persona_template.md` (read it before drafting the first persona). Sections are required unless marked optional; adjust ordering for the audience but do not omit sections.

### Output contract (what the review skill consumes)

When a multi-persona set will feed `persona-design-review` — the default for any set of more than one persona — emit:

- **One Markdown file per persona** in a single folder, named `NN-slug.md` (e.g. `01-sigridur-anna.md`). The leading `NN-` sets discovery sort order.
- The persona's **full display name as the H1** (`# Sigríður Anna Magnúsdóttir`) — distinct from the filename slug.
- **Free-prose body**, no YAML frontmatter required, as in `specs/personas/01-sigridur-anna.md`.
- A **`README.md`** in the same folder carrying the Stage 4 cross-persona synthesis — never itself a persona.

The consumer's `persona-design-review/references/persona-discovery.md` owns the discovery and slug rules; don't restate them here.

### Why no example scenarios

Do not embed example scenarios in the persona — they bake assumed product functionality into the user model, and teams then design toward the scenario rather than the underlying need (full rationale in `references/persona_best_practice.md`). Personas describe the user, not the product; scenarios belong in separate user-journey or jobs-to-be-done work. If the user asks for scenarios in the persona output, push back once, then produce them as a separate document if they insist.

### What to avoid

These are specific to the act of drafting; the broader catalogue of persona mistakes (stock-photo filler, demographics-as-personality, identical personas with different names) lives in `references/persona_best_practice.md`.

- **The elastic user.** Do not let personas drift toward whatever the team wants to build. Each persona has a fixed shape; if the product changes, update the persona deliberately.
- **Forced positivity.** Real users have real frustrations and risks. A persona without barriers is a marketing fantasy.
- **Quotes that sound like marketing copy.** Quotes should sound like something the person would actually say, including the way they would talk about their problem.

### Calibrating across a persona set

When creating multiple personas, vary deliberately along the dimensions that matter for the product. For a children's banking app, vary age within the band, household structure, language background, device access, and financial experience — not just first name and favourite colour.

A useful test: if you swapped two personas' names, would the document still make sense? If yes, they are not differentiated enough.

---

## Stage 4: Synthesise guidance

Personas alone are not the deliverable. The team needs help applying them. After the personas, include:

> **When the output is a file set,** write this synthesis to `README.md` in the persona folder alongside the persona files, opening with a one-line-per-persona index table that summarises the dimensions this set actually varies on (the axes from *Calibrating across a persona set*). Pick table columns to suit the cohort. Downstream readers — including `persona-design-review`, which loads the set and offers subset selection — use that table to see the axes at a glance. The README is cohort context, never itself a persona.

### Cross-persona themes
What is true across all personas in the set. These are the strongest signals for the product roadmap.

### Important differences between personas
Where the personas pull in different directions. These are the points where the team will have to choose, prioritise, or design carefully.

### Product opportunities
Specific opportunities visible from the persona set as a whole — patterns or unmet needs that are not obvious from any single persona.

### Risks and assumptions to validate
What in the personas is most speculative and most consequential. Be honest about this. The team will be more likely to do real user research if they know exactly which assumptions are load-bearing.

### Suggested next research or testing steps
Concrete next actions: who to interview, what to test, what data to collect. Translate the personas into a research plan, even briefly.

---

## Constraints and integrity rules

These are non-negotiable. The skill exists to enforce them.

- **Never skip the clarification stage.** If the user resists clarification ("just make me a persona"), explain that without context the output will be a generic archetype and not a persona. Offer to proceed with explicit assumptions clearly labelled, but recommend clarification first.
- **Never present invented details as facts.** Every detail is either evidence-grounded, an explicit assumption, or an explicit invention. The reader must always be able to tell which.
- **Never publish without a research summary.** Even a brief one. The personas' credibility depends on the visibility of their evidence basis.
- **Never refuse to flag assumptions.** Even if the user pushes for "a confident, polished persona", the assumptions stay visible. A persona's value is not its polish.
- **Do not invoke this skill if the user already has personas.** This skill is for creating new ones. Editing or critiquing existing personas is a different task.
- **For sensitive groups, do not soften the safety dimensions.** Children, healthcare patients, vulnerable users — the trust, consent, safety, and accessibility considerations must be explicit and prominent, not buried.

---

## Reference files

Read these as needed:

- `references/persona_best_practice.md` — what makes a good persona, common mistakes, how personas are used in practice. Read before drafting personas.
- `references/persona_template.md` — full structural template with section-by-section prompts. Read before writing the first persona.
- `references/research_checklist.md` — checklist of dimensions to investigate during stage 2 research. Use to make sure the demographic context is genuinely covered.
