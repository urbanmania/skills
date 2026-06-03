# Severity rubric (Spec mode)

In Spec mode the combined report is a gap register, not a comparison. Each item in the register is a thing the spec didn't say (or said wrong) for one or more personas. Severity is assigned by the orchestrator after clustering — never by individual personas.

## Definitions

- **Blocker** — multiple personas in the target audience cannot complete the flow as specified, *or* a hard exclusion (e.g. a refugee parent cannot access the feature at all because the spec assumes a specific identity flow; or a screen-reader-only persona cannot complete the flow because the spec relies on a drag interaction with no keyboard path). A Blocker means "do not ship this spec without fixing this".
- **Major** — a pattern of confusion that will cause significant drop-off; the spec is unclear or wrong on a load-bearing point. Two or more personas converge on the same misunderstanding.
- **Minor** — single-persona friction, copy nit, missing edge case affecting a small slice. Worth noting; not a release blocker.
- **Out-of-scope** — a persona-raised concern that's a real product question but outside this spec. Surface it; don't try to solve it here. (E.g. a persona asks "what happens if my parent dies?" while reviewing a savings-goal spec; or a persona reviewing a checkout spec asks about the returns policy — real concern, wrong spec.)

## Clustering rule

Before assigning severity:

1. Read every per-persona summary.
2. For each finding, check whether any other persona raised the same issue (same flow step, same copy, same missing affordance). Group identical or near-identical findings.
3. Severity is a function of *who* raised the issue, not how many.
   - 1 persona, in the target audience → Minor.
   - 2+ personas in the target audience → Major.
   - Multiple personas blocked, or a hard exclusion regardless of count → Blocker.
   - Outside the target audience or outside the spec's scope → Out-of-scope.

## Output shape

In the combined report's gap register, each row has:

- **ID** — short, e.g. `B-01` for first Blocker, `M-03` for third Major.
- **Severity** — pill.
- **Title** — one-line summary of the gap.
- **Raised by** — which personas, with profile shorthand.
- **What the spec didn't say** — concrete description, with the spec section reference.
- **Suggested change** — one-line. May be the persona's verbatim ask, may be the orchestrator's synthesis. Mark synthesis with `[synthesis]`.

## Hard rules

- A persona feeling "confused" once is Minor, not Major. Look for the cross-persona signal.
- Never invent a fix the personas didn't ask for and then dress it up as a finding. If the personas didn't surface it, it isn't a persona finding — note it separately as an orchestrator observation if it must be raised.
- "Real-user-testing risks" (claims you couldn't simulate confidently) are a separate section, not severity rows. Keep them apart from the gap register.
