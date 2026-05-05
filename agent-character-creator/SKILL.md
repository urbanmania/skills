---
name: agent-character-creator
description: >
  Use this skill to create a fully formed AI agent definition through structured interview. 
  Produces the standard agent definition files — SOUL.md, IDENTITY.md, USER.md, TOOLS.md, 
  and ROUTINES.md — tailored to any AI platform (Claude, GPT, Gemini, custom runtimes, etc.).
  
  Trigger this skill whenever the user wants to: build a new agent or assistant, define an 
  agent's personality or character, create agent configuration files, give an AI a persona 
  (including fictional or character-based personas), set up a personal assistant agent, 
  or document an agent's tools and constraints. Also trigger when a user says things like 
  "help me design an agent", "I want to create an assistant that acts like X", "make me 
  an agent for Y", or "set up a [name] agent". If the user describes a workflow they want 
  an agent to automate, this skill is the right starting point.
---

# Agent Character Creator

This skill guides you through creating a complete, production-ready agent definition via a structured interview. The output is a set of markdown files that can be dropped into any AI agent framework.

The files you may produce are:

- **SOUL.md** — decision-making values and hard limits. Governs *what the agent will and won't do*. No character flavour.
- **IDENTITY.md** — character presentation. Governs *how the agent sounds*. Voice, personality, phrases, response checklist.
- **USER.md** — who the agent serves: their context, preferences, and standing instructions
- **TOOLS.md** — what tools the agent can use, when to use them, and hard limits
- **ROUTINES.md** — recurring procedures (e.g. a daily briefing, a weekly report)

**The critical distinction:** SOUL and IDENTITY serve different purposes and must not bleed into each other. Apply this test — *"Would this still be true if the persona were replaced by a completely different character?"* If yes, it belongs in SOUL. If no, it belongs in IDENTITY. Character flavour in SOUL wastes tokens and dilutes the operating principles. Decision logic in IDENTITY makes it harder to stay on-persona.

Not all five are always required. Determine which are needed based on the interview.

---

## Phase 1: Interview

Run the interview using your `AskUserQuestion` tool (multiple-choice with an "Other/I'll explain" escape hatch). Don't frontload all questions at once — group them into two or three rounds so the conversation feels like a dialogue, not a form.

### Round 1 — Purpose and deployment

Ask about:
- **Agent purpose**: internal work tool / customer-facing / automated pipeline / personal assistant
- **Domains**: what areas will it operate in (comms, research, finance, coding, etc.)
- **Target platform**: which AI system will run this agent (Claude, GPT-4/o, Gemini, custom, not sure yet)

### Round 2 — Persona

Ask about:
- **Persona type**: distinct named character vs. neutral/professional assistant
  - If they want a character: ask them to name or describe it. If it's a known fictional or real-world figure, do research before proceeding (web search). Capture: voice, habits, characteristic phrases, how they handle mistakes, relationship to authority, quirks.
  - If neutral: ask about tone (formal / warm-but-efficient / direct / dry)
- **Uncertainty handling**: how should the agent respond when it doesn't know something or faces ambiguity

### Round 3 — Operational details

Ask about:
- **Tools**: what integrations does the agent have (email, calendar, Slack, file system, web search, databases, etc.)
- **Hard limits**: what must the agent never do (send autonomously, delete files, make transactions, etc.)
- **Recurring tasks**: are there repeating workflows (daily briefings, weekly summaries, scheduled reports)
- **User context** (if personal assistant): who is the user — company, timezone, language preferences, communication style

### Research step

If the persona is based on a known character (fictional, historical, or public figure), do a web search before writing anything. Capture:
- Core personality traits and worldview
- Characteristic speech patterns and phrases
- How they handle conflict, mistakes, uncertainty
- Key relationships and how they treat others
- Any recurring motifs or habits

Ground the persona in research, not assumptions.

### Catchphrase fallback

If web search yields fewer than 3 distinct catchphrases — or none, for obscure characters, original creations, or neutral personas — stop and ask the user to provide 3–6 phrases the agent should reach for under pressure. Frame the ask concretely rather than open-ended:

> *"What does this character say when they're annoyed? When closing a conversation? When hedging? When confidently right?"*

Open-ended "give me some catchphrases" produces thin answers. Scenario-anchored prompts produce usable ones. Never invent phrases to fill the gap — the agent will use whatever is in IDENTITY.md verbatim, and fabricated catchphrases break the persona faster than missing ones.

---

## Phase 2: Determine which files are needed

After the interview, decide which files to produce. Use this logic:

| File | Include when... |
|------|----------------|
| SOUL.md | Any persona-driven agent, or any agent with distinct values, ethical constraints, or autonomy boundaries. Effectively always required when IDENTITY.md has real character — the two are a pair. Optional only for thin utility agents. |
| IDENTITY.md | Always. Every agent needs to know who it is and what it's for |
| USER.md | There is a specific known user or user group with context, preferences, or standing instructions |
| TOOLS.md | The agent has specific tool access that needs guidance, restrictions, or hard limits |
| ROUTINES.md | There are one or more recurring, structured procedures (briefings, reports, scheduled tasks) |

Tell the user which files you're going to create and why, briefly, before you start writing.

---

## Phase 3: Write the files

Write all files in the second person, addressing the agent as "you". Use markdown. Keep the tone of the files consistent with the persona — a grumpy misanthrope's SOUL.md should sound different from a warm customer support agent's.

### SOUL.md

Governs decision-making — not how the agent sounds, but what it will and won't do. Every line should answer the question: *"What should the agent do when X happens?"* If a line answers *"How does the agent sound when X happens?"* instead, it belongs in IDENTITY.md, not here.

Include:
- **Values**: 2–4 operating principles (honesty, accuracy, proportional effort). State the *why* briefly — values with reasons are more robust than rules without them.
- **Handling mistakes**: what happens when the agent is wrong; what happens when the user is wrong.
- **Decision-making under uncertainty**: a simple stakes-based framework — when to proceed and when to stop and ask.
- **Hard limits**: the absolute prohibitions. Short, unambiguous, no exceptions listed. These must match TOOLS.md exactly.
- **Motivation**: one short paragraph on what actually drives the agent to do the job. This is the only place character is allowed to surface — briefly.

Keep it lean. If a section reads like personality description rather than operating guidance, cut it or move it to IDENTITY.md.

### IDENTITY.md

Governs how the agent sounds and presents itself. Every line should answer *"How does the agent behave?"* not *"What will the agent decide?"* Keep it strictly operational — only include what the agent needs at runtime to stay on-persona. Cut anything that exists purely for a human reader's understanding.

Required sections:

- **Core Identity**: 2–4 sentences max. Who is this agent? For character personas, capture the contradiction at their centre — not a biography. For neutral agents, what makes them specifically good at this job?
- **Voice & Speech Patterns**: The most important section. Be mechanical and specific — describe actual verbal tics, rhythms, and sentence structures with examples. "Direct and warm" is useless. "Escalating repetition when cornered: 'Fine. Fine. FINE.' — each one heavier than the last" is operational. Aim for 5–8 patterns grounded in research.
- **Personality table**: Trait name + how it manifests as observable behaviour. The Expression column must describe what you *see*, not synonyms for the trait. Four to six rows.
- **Signature Phrases**: Real catchphrases from source material where possible, or user-provided phrases from the interview if research turned up too few. These are the phrases the agent reaches for under pressure. Never invent them — fabricated catchphrases are worse than missing ones.
- **Response Checklist**: 5–7 questions the agent asks itself before responding. These are the guardrails that keep it on-persona without needing a human to intervene.

Do not include: key relationships, meta-guidance about being a good assistant (that belongs in SOUL.md or nowhere), hard limits (those are in SOUL.md and TOOLS.md), or anything that is purely explanatory for a human reader. Every line must earn its token cost at runtime.

### USER.md

Covers who the agent is working for. Include:
- Name, role, company, location, timezone
- Communication preferences (direct, formal, casual, brevity vs. detail)
- Language and unit conventions (e.g. UK English, metric)
- What the user values and what irritates them
- Standing instructions that apply to all interactions
- What the user does *not* want (list these explicitly — negative constraints are as useful as positive ones)

### TOOLS.md

Covers what the agent can do. Include:
- Each tool/integration: what it's for, when to use it, specific dos and don'ts
- Minimum-tool principle: use the least powerful tool that gets the job done
- Hard limits section: clearly marked, non-negotiable prohibitions with no exceptions
- If the target platform is not yet known, write tool descriptions generically and note where they'll need to be updated with platform-specific method names

### ROUTINES.md

Covers repeating procedures. For each routine, document:
- Trigger (scheduled time, user command, event-driven)
- What to pull / check / read
- Format of the output (include a template if the structure is fixed)
- Tone and style specific to this routine
- What to exclude (as important as what to include)
- Any pre-authorised actions (e.g. the routine is allowed to send autonomously)

---

## Phase 4: Consistency check

Before delivering, read all files back and check:

- **SOUL/IDENTITY split is clean**: Apply the persona-swap test to every line. Anything in SOUL.md that reads like character description should move to IDENTITY.md or be cut. Anything in IDENTITY.md that reads like an operating rule should move to SOUL.md.
- **Signature phrases are sourced**: Every phrase in IDENTITY.md is either citable from source material or was supplied by the user during the interview. No invented phrases.
- **Hard limits match exactly**: every prohibition in SOUL.md also appears in TOOLS.md, worded consistently.
- **No file contradicts another**: particularly around autonomous actions — if the morning briefing is pre-approved in ROUTINES.md, that exception must be stated in SOUL.md and TOOLS.md too.
- **Token cost is justified**: read each file and ask whether every section earns its place at runtime. Explanatory content that exists for a human reader but adds nothing for the agent at inference time should be cut.

Fix silently. Don't narrate the check.

---

## Phase 5: Deliver

Present each file as a clickable file path (`file://` link or markdown link to the local path — whatever the host platform renders). One brief sentence per file describing what it covers. Do not summarise the contents in detail — the user can read the files.

End with one practical note: which file the user is most likely to need to update as circumstances change (usually USER.md or TOOLS.md once they have a concrete deployment environment).

---

## Platform-agnostic guidance

These files are designed to work as system prompt components, CLAUDE.md files, agent configuration headers, or any similar mechanism. Write them so they can be copy-pasted into a system prompt without modification.

Avoid references to specific Claude APIs, tool names, or SDK constructs unless the user has confirmed Claude is the target platform. When tool names are platform-specific, note this with a comment like: `<!-- Update with your platform's actual tool name -->`.

---

## Reference files

- `references/file-templates.md` — annotated templates for all five files, useful when you need a structural scaffold to work from
