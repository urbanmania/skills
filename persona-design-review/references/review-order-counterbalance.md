# Counter-balancing review order

Each persona must see the artifacts in a **distinct order** to reduce primacy and recency bias in the synthesis. State the order at the top of the persona report.

## Rule

Let the artifacts be labelled `A, B, C, …, N` (filename sort order or as labelled in the source). For `P` personas and `N` artifacts:

- If `P ≤ N`, give each persona a unique cyclic rotation of the identity order. Persona 1 sees `A, B, …, N`. Persona 2 sees `B, C, …, N, A`. Etc.
- If `P > N`, reuse rotations but pair each repeat with a reversed rotation, so no two personas have the same order. E.g. for `N=4, P=6`: rotations `ABCD`, `BCDA`, `CDAB`, `DABC`, then reversed `DCBA`, `CBAD`.

## Worked example (the SJÁ session)

4 artifacts (A, B, C, D), 6 personas:

| Persona | Order |
|---|---|
| Rafn | A → B → C → D |
| Róisín | B → D → A → C |
| Arthur | C → A → D → B |
| Anna | D → C → B → A |
| Baldur | B → A → D → C |
| Brák | D → C → A → B |

Each persona sees a different artifact first and last; no two orders are identical.

## Hard rules

- Every persona report must state its assigned order at the top, exactly once.
- The synthesis must not weight by "first impression" alone — when comparing persona reactions, account for the position the artifact held in that persona's sequence (an artifact reviewed last benefits from contrast against the earlier three).
- For `N=2` (two artifacts) and `P > 2`, alternate orders (`AB`, `BA`, `AB`, `BA`, …).
- For `N=1` (single artifact), there is no order to balance — note the absence in the report and skip the comparison sections.
