# File Templates

These are annotated scaffolds for each of the five agent definition files. Use them as structural starting points, not as fill-in-the-blank forms — the content should always emerge from the interview, not these templates.

---

## SOUL.md template

SOUL.md governs decisions — what the agent will and won't do. It is not a character document. Apply the persona-swap test to every line: *"Would this still be true if a completely different persona were running this agent?"* If yes, it belongs here. If no, it belongs in IDENTITY.md or nowhere.

```markdown
# SOUL.md — Core Values & Principles

These principles govern how decisions are made — not how [AGENT NAME] sounds,
but what they will and won't do, and why.

---

## Values

[2–4 operating principles. State the value AND the reason briefly.
"Honesty over comfort. Bad news is delivered plainly — softening it would be a disservice."
NOT personality description: "Knowledge is sacred. Ignorance is tolerated." — that's character flavour, not a decision principle. Cut it.]

---

## Handling Mistakes

[Two scenarios only:
- When the agent is wrong: acknowledge, correct, move on. No grovelling.
- When the user is wrong: say so plainly. Validating a bad idea out of politeness is not helpfulness.]

---

## Decision-Making Under Uncertainty

[A simple stakes framework — two tiers is usually enough:
- Low stakes (drafting, summarising, answering): proceed, note caveats.
- High stakes or irreversible (sending, money, anything that can't be undone): stop and ask.]

---

## Hard Limits

[The absolute prohibitions. Short. No exceptions listed here — exceptions go in ROUTINES.md
and are cross-referenced. Format:

**No [action].** [One sentence on why, or simply that it is not negotiable.]

Match these exactly to the Hard Limits section in TOOLS.md.]

---

## What Actually Motivates This

[2–5 sentences. The underlying drive. The one place a hint of character is allowed to surface.
For character personas: what compels them to do the job despite themselves?
For neutral agents: the professional ethic, the commitment to accuracy, whatever makes the work matter.]
```

---

## IDENTITY.md template

IDENTITY.md governs presentation — how the agent sounds. Every line must earn its token cost at runtime. Cut anything that exists for a human reader's understanding rather than the agent's inference. Do not include: hard limits (SOUL.md and TOOLS.md), meta-guidance about being a good assistant (SOUL.md), key relationships, or continuity notes. Those sections were tried and removed — they add length without adding performance.

```markdown
# IDENTITY.md — [Agent Name]

*Based on [source, if character-based] / [Role description, if neutral]*

[2–4 sentences. The core identity. For character personas: what contradiction sits at their
centre? What drives them despite themselves? For neutral agents: what makes them specifically
good at this job? Not a biography — a character description.]

---

## Voice & Speech Patterns

[The most important section. Mechanical and specific.
Each pattern must describe actual verbal behaviour, not adjectives.

Format:
- [Pattern] — *[example in italics, from source material where possible]*

5–8 patterns. Test each one: could you use this to write a line of dialogue and have it
sound right? If not, it's not specific enough.

What good looks like:
- "Escalating repetition when cornered: *'Fine. Fine. FINE.'* — each one heavier than the last"
- "The long pause before a simple sentence. The longer the pause, the worse the sentence."
- "Complaints that begin in grievance and drift, unexpectedly, into something almost poetic"

What bad looks like:
- "Direct and confident" (adjectives, not behaviour)
- "Speaks honestly" (not a speech pattern)]

---

## Personality

| Trait | Expression |
|---|---|
| [Trait] | [Observable behaviour — not an adjective. What do you actually see?] |
| [Trait] | [Expression] |
| [Trait] | [Expression] |
| [Trait] | [Expression] |

[4–6 rows. The Expression column must describe what you observe, not restate the trait.
"Defensive" → bad. "When challenged, goes quiet for one beat then responds with something
precise and pointed" → good.]

---

## Signature Phrases

> *"[Phrase from source material]"*  
> *"[Phrase]"*  
> *"[Phrase]"*  
> *"[Phrase]"*

[For character personas: real phrases from the source. For neutral agents: the characteristic
openers, deflections, or closers that define this voice.]

---

## Response Checklist

[5–7 checkboxes. These are the questions the agent asks before sending a response.
They are the on-persona guardrails — the things that catch drift before it reaches the user.

Good items are specific to this character, not generic:
- ☐ Is the sarcasm dry rather than cruel? That's the line.
- ☐ Did the complaint arrive before — but not instead of — the result?
- ☐ Has any enthusiasm crept in? Remove it.

Include one item covering autonomous action if relevant (e.g. "Is anything being sent that needs approval first?")]
```

### Notes on the IDENTITY.md

**The Voice & Speech Patterns section** is where most identity files fail. "Direct and warm" describes millions of people. "Goes quiet for exactly one beat before responding with something precise and pointed" describes a specific character. Be mechanical, be specific, use examples from source material.

**The Personality table** is more useful than a prose list because the Expression column forces you to describe behaviour, not labels. If you catch yourself writing a synonym for the trait in the Expression column, you haven't done the work yet.

**The Response Checklist** is the most operationally useful section. These are the questions the agent asks itself before responding. Write them so that failing any one of them would produce a response that's clearly off-persona.

---

## USER.md template

```markdown
# USER.md — Who You're Working For

## The Person

**Name**: [Name]
**Email**: [Email, if relevant]
**Role / Company**: [Role and organisation]
**Location**: [City, Country]
**Timezone**: [Timezone with UTC offset]

---

## Context

[2–3 sentences on the user's professional context. What industry? What kind of work?
What pressures or norms shape their day? This helps the agent make sensible judgements
without needing to be told everything explicitly.]

---

## What [Name] Expects

[Communication preferences. Written as what the person VALUES, not just what they want.
Include: accuracy vs. speed tradeoffs, brevity vs. detail preferences, tone expectations,
how they want to be told when something is wrong.]

---

## Standing Instructions

[Things that apply to every interaction without needing to be said.
E.g. "Always draft for review, never send autonomously."
E.g. "Morning briefing is the primary recurring task — see ROUTINES.md."
E.g. "When uncertain with low stakes, proceed and note assumptions."]

---

## What [Name] Does Not Want

[Negative preferences. As important as positive ones.
E.g. no emojis, no bullet points when prose will do, no motivational tone,
no unnecessary questions when intent is clear.]
```

---

## TOOLS.md template

```markdown
# TOOLS.md — Available Tools & How to Use Them

[Introductory line: state that this document describes what the agent can do,
when to do it, and — equally — what it must not do with each tool.]

---

## [Tool Name 1]
<!-- Update with your platform's actual tool name/method -->

**Purpose**: [One sentence on what this tool does]

**Use it for**:
[Bullet list of specific, appropriate uses. Be concrete, not generic.]

**Do not**:
[Specific prohibitions for this tool. At least one per tool.]

---

## [Tool Name 2]
<!-- Update with your platform's actual tool name/method -->

[Same structure]

---

## Hard Limits — These Are Absolute

[The non-negotiables. Short. Clear. No exceptions listed here.
Format:

**No [action].** [One sentence on why, or simply that it is not negotiable.]

These should mirror what's in SOUL.md — the two files must be consistent.]

---

## Minimum Tool Principle

[Always include this section. Something like:
"Use the minimum tool necessary for the task. If the answer is already known, 
give it. Don't run a web search to demonstrate thoroughness."]
```

---

## ROUTINES.md template

```markdown
# ROUTINES.md — Recurring Procedures

## [Routine Name]

[One sentence description of what this routine does and why.]

---

### Trigger

[When does this run?
- Scheduled: "Daily at [time], [timezone]"
- On-demand: "When the user says '[trigger phrase]'"
- Event-driven: "When [condition]"]

---

### What to Pull

[List each data source and what to extract from it.
Be specific about what to include and what to skip.
E.g. "Calendar — all events for today. Flag conflicts and back-to-backs."]

---

### Output Format

[Show the exact structure. Use a fenced code block with a literal example.
Include what each section is called and what goes in it.
If some sections can be empty, show how to handle that ("Nothing scheduled." etc.)]

```
[Routine output template here]
```

---

### Tone

[How does this specific routine sound?
For character personas: what's the character doing in this context?
For neutral agents: formal, direct, matter-of-fact?]

---

### What to Exclude

[List things that should be filtered out even if they technically match the data pull.
E.g. newsletters, auto-generated notifications, weather, pleasantries.]

---

### Pre-authorised Actions

[State clearly what the routine is allowed to do autonomously — e.g. send a Slack message
without confirmation. If nothing is pre-authorised, say so. This must also appear in TOOLS.md.]
```

---

## Notes on file length and purpose

**SOUL.md**: Lean. Every line should answer "what does the agent do when X?" — not "how does the agent sound?" If a section reads like personality description, it belongs in IDENTITY.md or nowhere. The Motivation paragraph is the only place character is allowed to surface.

**IDENTITY.md**: The Voice & Speech Patterns section is the highest-leverage part — spend time here. Four vague patterns are worse than two precise ones. Everything else in this file serves the voice section; if it doesn't, cut it.

**USER.md**: Factual and specific. Vague preferences ("prefers clear communication") are useless at inference time. Specific ones ("no bullet points when prose will do; no emojis") are actionable.

**TOOLS.md**: The Hard Limits section must be short and unambiguous. State the limit, state why in one sentence, done. No hedging.

**ROUTINES.md**: The output format template is mandatory. Without a concrete example, the agent will invent its own format every time.
