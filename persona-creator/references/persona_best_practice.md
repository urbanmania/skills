# Persona best practice — reference summary

A condensed reference on what makes personas useful in software and product development. Read this before drafting personas.

## What a persona is

A persona is a fictional but evidence-grounded representation of a user group. It distils observed patterns from research into a single, named character that a product team can refer to when making decisions. The fiction is the narrative wrapper; the evidence is the spine.

A persona built without research is not a persona. It is an assumption with a name attached. The word "fictional" in the standard definition refers to the composite character, not the basis for the patterns.

## Why personas exist

- **Empathetic decision-making.** Personas humanise abstract user data. They help teams reason about real people instead of an idealised average user.
- **Alignment.** When teams have differing implicit assumptions about who the user is, decisions devolve into opinion. A shared persona replaces "I think users want…" with "Would Sigríður want this?"
- **Resistance to self-referential design.** Without a specific user representation, teams unconsciously design for themselves. A specific persona breaks this pattern.
- **Resistance to the "elastic user."** Without fixed personas, the definition of "the user" expands and contracts to fit whatever the team wants to build. Fixed personas hold the line.

## What a useful persona contains

- **Demographics and context** — age, location, life context. Specific, not "Europe", not "20s".
- **Goals and motivations** — what they are actually trying to accomplish, including emotional and social goals, not just feature requirements.
- **Pain points and frustrations** — what stops them, inside and outside the product.
- **Observed behaviours** — how they act in practice. These often diverge from what they say in interviews.
- **Quotes** — verbatim or constructed phrases that capture mindset.
- **Design implications** — actionable signals for the team.

Note: scenarios of use are deliberately excluded from this list. They are useful, but they belong in separate user journey or jobs-to-be-done documents — not embedded in the persona itself. Including scenarios inside the persona document tends to bake assumed product functionality into the user representation, which inverts the intended relationship between user understanding and product design.

## What a persona is not

- A buyer or marketing persona. Buyer personas focus on purchase journey; UX personas focus on use.
- A demographic profile. Demographics are inputs to the persona; they are not the persona.
- A user story. User stories are scoped to specific tasks; personas are broader characterisations.
- A target market summary. Markets are aggregations; personas are individuals.

## Common mistakes

- **Building on assumptions alone.** The most common failure. A guess-based persona looks convincing in a workshop and falls apart on contact with real users.
- **Too many personas.** More than five or six dilutes focus. One strong primary plus two or three secondaries is usually correct.
- **Vanity documents.** Beautiful slides with stock photos and long biographies do not improve UX. Substance over polish.
- **Filing it away.** A persona that lives in a folder and is never referenced during decisions is dead weight.
- **Treating personas as static.** Users evolve. Products evolve. Personas should be revisited.
- **The elastic user problem.** Letting personas drift toward whatever feature the team wants to build that week.
- **Demographics-heavy, behaviour-light.** Statistics about a user group are not the same as understanding how that group behaves with technology.
- **Stereotypes dressed up as personas.** A "tech-savvy millennial" or "busy mum" is not a persona. Specificity is what makes a persona useful.
- **Identical personas with different names.** If you can swap two personas' names without anything else changing, they are not differentiated.

## Evidence vs assumption vs invention

The single most important discipline in persona creation. For every claim:

- **Evidence** — supported by research; cite the source.
- **Assumption** — extrapolated from research, plausible but not directly supported; label it as such.
- **Invention** — fictional detail added to make the persona feel real; label it as such.

A persona that mixes these without distinction loses the trust of the team. Engineers and designers will start to question the well-grounded parts because they cannot tell which parts are sound. Visible labelling of assumptions actually increases trust in the rest.

## How personas are used

- **Design reviews.** "Would this work for Sigríður? What would she struggle with?"
- **Prioritisation.** Features evaluated against the primary persona's needs first; secondary personas used to stress-test.
- **User test recruitment.** Personas define recruitment criteria — not just "children", but children matching specific contextual attributes.
- **Test scenario design.** Scenarios written from the persona's perspective produce more realistic usability tasks.
- **Stakeholder alignment.** Personas keep cross-functional conversations grounded. "Marketing wants X, engineering wants Y, but Sigríður needs Z" is a more productive frame than competing internal opinions.
- **Onboarding new team members.** A new designer or PM can absorb the personas in an hour and start contributing with shared context.

## When personas fail

- When they are not used. The biggest failure mode. The fix: reference them by name in design discussions, code reviews, and roadmap meetings.
- When they are presented as artwork rather than tools. A polished PDF that nobody reads is worse than a one-page text file that everybody references.
- When they are created in isolation by the UX team and unveiled to the rest of the company. Personas need to be developed with cross-functional input or they will be ignored.
- When they overgeneralise. A single persona that tries to represent all users represents none of them.

## A note on proto-personas

A proto-persona is an assumption-driven placeholder used when user research is not yet possible. It is acceptable as a starting point — provided it is labelled honestly and replaced as soon as real user contact becomes possible. A proto-persona presented as a researched persona is dishonest and dangerous; a proto-persona presented as a proto-persona is a reasonable starting tool.

## Sources

This summary draws on Cooper (1999, *The Inmates Are Running the Asylum*); Pruitt and Adlin (2006, *The Persona Lifecycle*); Nielsen Norman Group writing on persona effectiveness and failure modes; published practitioner guides from Adam Fard, Qubstudio, Contentsquare, and Brand Vision; and academic work on personas in user-centred design (Frontend.com pilot study; Springer publications on persona creation in financial services).
