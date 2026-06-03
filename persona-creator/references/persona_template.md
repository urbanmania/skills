# Persona template

A structural template for individual personas. Use this when drafting each persona. Sections are required unless marked optional. Adjust ordering if the audience needs it (for example, leading with quotes for a stakeholder presentation), but do not omit sections.

The prompts after each heading are not for the final document — they are guidance to make sure the section is doing real work, not filler.

---

## 1. Name

A culturally appropriate first and last name for the demographic. Check naming conventions: patronymics in Iceland, family-first names in Hungarian or Japanese contexts, naming traditions in Spanish-speaking countries, and so on. A wrong-feeling name signals a generic persona before the reader gets to the substance.

For sensitive groups (children, healthcare patients), consider whether a real-sounding name is appropriate, or whether a more abstract identifier helps maintain the proto-persona honesty.

**File contract:** when the persona is one file in a set, the file is named `NN-slug.md` (e.g. `01-sigridur-anna.md`), the persona's full display name is the H1 (`# Sigríður Anna Magnúsdóttir`), and the slug is the filename with the leading `NN-` removed. The H1 and the slug are not the same string.

## 2. Age and location

Specific. "Aged 11" is better than "pre-teen". "Breiðholt, Reykjavík" is better than "Iceland".

If the persona represents a range, pick one specific point within it as the focal age and note the range it represents.

## 3. Tagline / archetype (optional but useful)

A short phrase capturing the essence. "The careful saver who wants to feel grown-up about money." This is what the team will reach for in conversation when they say "the Sigríður type."

## 4. Short profile summary

Three to five sentences. Who is this person? What is their relationship to the product area? What makes them specific rather than generic?

Do not pad with biographical detail that does not affect product decisions.

## 5. Background and daily life

What does their day actually look like? Routine, time pressures, key activities. This grounds the persona in lived experience and helps the team imagine when and how the product fits into their life.

For children: school day, after-school routine, weekend pattern.
For workers: commute, working hours, time-of-day pressures.
For patients: condition management routines, appointments, daily symptoms.

## 6. Household, school, work, or social context

Who they live with, who they answer to, who they collaborate with. Relationships shape decisions far more than demographics do.

For minors: guardian structure, sibling dynamics, custody arrangements where relevant.
For older adults: living arrangements, family proximity, support network.
For workers: team structure, reporting line, collaboration patterns.

## 7. Digital habits and device access

What devices do they have? Personal or shared? What apps do they use most? What is their comfort level with new digital tools?

This is where many personas drift into stereotype ("tech-savvy", "not tech-savvy"). Push for specifics: which apps, what context, what frustrations.

## 8. Relationship to the product area

What is their existing knowledge, behaviour, and comfort level with the domain the product addresses? This is the bridge between who the persona is and how they will use the product.

For a banking app: how do they currently handle money? What financial vocabulary do they have?
For a health app: what is their relationship to their condition, to clinicians, to self-tracking?
For a productivity tool: what is their current workflow? What tools do they already use?

## 9. Goals and motivations

What is the persona trying to accomplish? Distinguish:

- **Functional goals** — concrete tasks they want done
- **Emotional goals** — how they want to feel (in control, respected, safe, competent)
- **Social goals** — how they want to be seen by others
- **Identity goals** — what kind of person they want to be

Personas often fail by listing only functional goals. Emotional and identity goals are where products win or lose loyalty.

## 10. Needs from the product

What concrete needs translate to product features? Frame as needs, not features — "needs to know her balance is real" not "needs a balance display." The team will derive features from needs; if you give them features, you are doing their thinking for them and limiting the design space.

## 11. Frustrations, risks, and barriers

What stops them? What goes wrong? What has put them off similar products in the past?

Be honest. A persona without barriers is a marketing fantasy. Include both barriers in the product domain (e.g., banking jargon is alienating) and barriers in their context (e.g., shared device, limited privacy at home).

## 12. Trust, safety, privacy, or accessibility considerations

Always include this section. For most personas it is a paragraph; for sensitive groups it must be substantial.

For children: consent, guardian involvement, comprehension, safety, privacy from peers and family.
For healthcare patients: data sensitivity, clinician trust, family involvement, comprehension under stress.
For users with accessibility needs: specific accommodations, assistive technology, energy and cognitive load considerations.
For older adults: digital literacy without condescension, scam protection without infantilisation.
For workers in regulated industries: compliance, audit trail, employer visibility.

A persona without this section assumes everyone is a confident, healthy, English-speaking adult with full capacity. That assumption is wrong for most products.

## 13. Representative quotes

Four to six invented but plausible quotes that capture the persona's mindset, in language they would actually use. Avoid quotes that sound like marketing copy. Aim for the texture of how the person would talk about their problem, their goals, their frustrations.

Always label these as constructed unless they come from real research transcripts.

## 14. Design implications for the product team

The most important section, and often the weakest. Generic implications ("easy to use", "intuitive") are worthless. Specific implications drive decisions:

- "Lead with a goal, not a balance — the home screen should foreground a named saving goal and its progress."
- "Use plain Icelandic at 5th-grade reading level throughout."
- "Authenticate via PIN or biometric, not Auðkenni — under-16s cannot hold Auðkenni independently."

Each implication should be specific enough that a designer or developer could act on it the next morning. If an implication is vague, push it further.

---

## On scenarios — and why they are not here

No example scenarios in the persona: a scenario invents specific product functionality, which then gets treated as a requirement and starts driving the roadmap rather than informing it. Full rationale in `references/persona_best_practice.md`. If a team wants scenarios, produce them as a separate user-journey or jobs-to-be-done artefact, not embedded in the persona.

---

## Document-level conventions

- Label assumptions and inventions inline. Do not bury them in a footnote.
- Cite sources for evidence-based claims, even briefly. A note like "(Eurydice / Iceland)" is enough.
- Keep prose lean. Personas are reference documents; they get scanned, not read straight through.
- Include a closing paragraph stating the document's research basis and what should be validated with real users.
