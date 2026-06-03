# Question battery

The question battery is decided at Round 2 of intake. Three sources, in default-preference order:

1. **Generate from review goal** — orchestrator drafts a battery from the user's review goal, product domain, and any selected emphasis, shows it to the user for one-tap approval, then dispatches. The default for any domain. See *Generation rule*.
2. **Custom file** — user-supplied `.md`; the orchestrator uses it verbatim.
3. **Pre-built kids-banking battery (BankBank example)** — the SJÁ battery (banking, savings, customisation, asking parents for money). Use only when the domain is kids-banking. See the bottom of this file.

Whichever source is used, save the final battery as `<output_folder>/_battery.md` for traceability. The combined sponsor report cites it.

## Battery structure (all sources must follow this)

Every battery is structured as three blocks. The orchestrator pastes all three into each sub-agent prompt verbatim.

- **Block 1 — general expectations** (asked once, in character). 2–4 questions. Calibrates the persona's prior expectations before they look at the artifacts. Skip-able if the artifact is so foreign that prior expectations are meaningless (rare).
- **Block 2 — per-artifact questions** (asked for each artifact in the assigned order). 6–14 questions. The bulk of the review. Must include at least one question per dimension the combined report's comprehension table will use.
- **Block 3 — post-review reflection** (asked once at the end). 3–6 questions. Cross-artifact judgements: prettiest, most trusted, would-not-use, hybrid pick.

## Generation rule

When the user picks *Generate from review goal*, draft a battery using this template, then show it for approval. Use the product domain and review goal to make every question concrete — name the artifact type, name the user role, name the primary outcome.

### Block 1 — generic shape (adapt 2–4 of these)

- Have you used a *<product type>* before?
- What would you expect to be able to do in a *<product type>* like this?
- What makes a *<product type>* feel trustworthy / fun / easy to you?
- What's the first thing you'd look for?

### Block 2 — generic shape (pick 6–14 across these dimensions)

Always include the Comprehension group. Add others as the product warrants — domain-specific dimensions (safety, cold-start onboarding, competitor comparison, etc.) belong here too. The gated groups below switch on when the matching Round-2 emphasis is selected (or when the gate condition otherwise holds).

Comprehension:
- What do you think this *<artifact>* is for?
- What can you do here? What's the first thing you'd tap?
- Where would you check *<primary state question for the product>*?
- Where would you go to *<primary action question for the product>*?

Trust / aesthetics (when relevant):
- What do you think of the look and feel?
- Does this feel like something a real *<organisation type>* would make?
- Is anything making you feel less sure about trusting it?

Task-walkthrough (only if review goal is *Task walkthrough*):
- The task is: *<task script>*. Walk me through what you'd tap first, what you'd expect, then next, then next.
- At any step, if you expected something different from what's shown, tell me what you expected and why.
- Where would you give up?

Tone / register (when audience age or register matters):
- Does anything here sound too young / too formal / patronising?
- Is there a word or label you don't understand?

Personalisation / continuity (when relevant):
- Would you want to change how this looks? Where?
- Would you want this to remember you between sessions?

Accessibility & cognitive load (when ND / low-vision / second-language personas are in the set, or the Accessibility emphasis is selected):
- Is anything too small, too fast, or too busy to follow? Where does your attention go first, and does it stay there?
- If you read more slowly or in your second language, which words or steps lose you? Could you do this without sound / without colour?

Error recovery (when the product has destructive or irreversible actions):
- If you tapped the wrong thing, how would you get back? Is it clear what's reversible?

Value / pricing (for paid products, or when the Pricing emphasis is selected):
- Does the price feel fair for what you get? What would make it worth paying for?

Competitive comparison (when an external baseline is named, or the Competitive emphasis is selected):
- Compared with *<baseline / the tool you already use>*, what's better here, what's worse, and what would make you switch or stay?

> The **Personalisation/continuity** and **Tone-for-age** groups are visual-consumer-UI specific — drop them for non-visual or non-consumer domains.

### Block 3 — generic shape (3–6)

- Which *<artifact>* did you like most? Why?
- Did any feel *<too young / too corporate / not for me / untrustworthy>*?
- Which would you trust most with *<the primary thing the product asks of the user>*?
- If you could pick the best bits from each and combine them, what would you take and from which?
- Is there anything you'd want this to do that none of them did?

Retention (when the review goal includes longer-term use, or the Longitudinal emphasis is selected):
- Imagine you've used this for two weeks — are you still opening it, and why / why not? What would make you stop? What would bring you back? Is anything here boring or pointless once the novelty wears off?

**Single-artifact runs** (one PDF, one screen, one spec): drop the comparison/hybrid items ("liked most", "trust most", "best bits combined") and keep the reflection items reworded for one artifact — "would you use this and why", "what felt too young / too corporate / not for you", and the closer "Is there anything you wanted this to do that it didn't?"

## Task-walkthrough addendum

When the review goal is *Task walkthrough*, the orchestrator also injects this block at the top of the per-artifact section of each sub-agent prompt:

> The task you are about to attempt on each artifact is:
>
> **<task script>**
>
> Walk through the artifact as if you were attempting this task. For each step:
> 1. Say what you would tap or look at next.
> 2. Say what you expect to happen.
> 3. If what's shown differs from what you expected, say so and why.
> 4. If you would give up, say where and why.
>
> Then answer the Block 2 questions in context of that walkthrough.

If the artifact is a static screen (one PDF, one image) and the task requires multiple steps, the persona narrates the *expected* flow rather than the *actual* flow — that gap is itself the finding. State the limitation explicitly in the persona report.

## Custom battery file format

Accept any `.md` file with three top-level sections, each containing a bulleted list of questions:

```markdown
# Block 1 — general expectations
- …
- …

# Block 2 — per artifact
- …
- …

# Block 3 — post-review reflection
- …
- …
```

If the file doesn't match this structure, tell the user, do not silently restructure.

## Default kids-banking battery (BankBank / SJÁ)

Only use this when the product domain is kids-banking. Warn if used elsewhere.

### Block 1

- Hefur þú notað bankaapp áður?
- Hvað gerir maður í bankaappi / hvað myndir þú vilja geta gert í bankaappi?
- Hvað gerir app skemmtilegt fyrir þig?

### Block 2

- Hvað finnst þér um útlitið/hönnunina á þessu appi?
- Hvað heldur þú að hægt sé að gera í þessu appi?
- Hvar myndir þú athuga hvar þú átt mikla peninga?
- Sérðu hvað er mikið inn á kortinu þínu, ef þetta væri þitt app?
- Ert þú stundum að safna eða spara fyrir einhverju?
- Getur þú fundið sparnaðarmarkmið í þessu appi?
- Hversu mikið vantar upp á að þú náir markmiði þínu?
- Skilur þú alveg hvað appið er að segja um sparnaðarmarkmiðið þitt?
- Það er hægt að breyta útlitinu á appinu. Hvernig myndir þú gera það?
- Finnst þér skipta máli að geta breytt útlitinu eða bakgrunninum?
- Hvar myndir þú breyta um útlit á kortinu?
- Finnst þér mikilvægt að geta skipt um mynd á kortinu þínu?
- Viltu að sama mynd sé á raunverulega plastkortinu þínu sem þú ert með í vasanum?
- Hvernig myndir þú biðja mömmu/pabba um pening í appinu?
- Er eitthvað sem þér finnst skrítið eða sem þú skilur ekki?
- Myndir þú vilja nota þetta app?
- Af hverju / af hverju ekki?

### Block 3

- Hvaða app fannst þér flottast? Af hverju?
- Fannst þér eitthvað app eða hönnun of barnaleg?
- Hvaða appi myndir þú treysta best?
- Ef þú gætir valið það sem þér finnst flottast í öppum og blandað saman, hvað myndir þú velja úr hverju appi og hvers vegna?

## Hard rules

- Show the generated/loaded battery to the user **before dispatch** when the source is *Generate from review goal* or *Custom file*. One-tap approval, then dispatch.
- Save the approved battery to `<output_folder>/_battery.md`.
- Sub-agents must answer every question in the battery; "n/a — artifact doesn't show this" is an acceptable answer, silently skipping is not.
- Question language follows the persona's profile (Icelandic / English / Polish / etc.) — do not normalise to English in the sub-agent's reactions. The orchestrator-side battery can be in English; the persona answers in their native register.
