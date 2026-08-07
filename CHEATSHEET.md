# Metaconcert - Member / Bias Map

Read the middle column, not the left one. The mechanism is what does the work;
the member is just where it lives.

| Member | Filters | Mechanism | Cost |
|---|---|---|---|
| **mc-observer** | Confirmation bias at source; anchoring; premature closure | Strips causal claims from the report before any member sees them; quarantines rather than deletes, so human-vs-independent divergence stays measurable | Very low |
| **mc-cartographer** | Curse of knowledge; fluency illusion; unstated-assumption defects | Forces the system model into an auditable structure with per-item epistemic class; the `[assumed]` list is the externalised knowledge gap | Low |
| **mc-diagnostician** | Confirmation bias; availability; single-hypothesis fixation | Minimum three hypotheses, one located outside the symptom's component, each with a named falsifier; ranked by information-per-cost not by likelihood | Low |
| **mc-historian** | Planning fallacy; optimism bias; scope insensitivity | Reference-class forecasting from actual git history; forbidden from inside-view decomposition; reports distribution plus rework tail | Very low (Haiku) |
| **mc-oracle** | Outcome bias; tests-mirror-implementation; spec ambiguity laundering | Writes criteria blind to the diff; names the plausible wrong implementation; refuses to resolve spec ambiguity silently | Low |
| **mc-falsify** | Confirmation bias at the moment of measurement; p-hacking; outcome-driven reading | Executes one pre-registered test blind to which outcome anyone wants; reports raw observation before interpretation; never says "confirmed", only which branch matched | Low |
| **mc-builder** | Sunk cost; scope creep; inherited rationale | Receives the decision, not the deliberation; halts on map/reality contradiction instead of repairing the map and continuing | Medium |
| **mc-adversary** | Automation bias; IKEA effect; fluency illusion at review | No rationale in context; cannot return a clean verdict without enumerating checks and evidence; verifies by execution not by reading | High (Opus, different family) |
| **Director** | Re-centralisation; consensus pressure; premature synthesis | Enforces the membrane, surfaces divergence unresolved, never forms a view | Free in dispatches, paid in main-session context (carries every artifact at least twice) |

## The four cross-cutting rules

1. **Independent, then compare. Never converge.** Agreement between members that
   shared a frame is an echo. Only agreement between members that could not see
   each other is evidence.
2. **Artifacts cross the membrane, reasoning does not.** Rationale is the vector
   by which one member's blind spot becomes everyone's.
3. **The human reconciles.** Every divergence lands on you, unsmoothed. If the
   workflow ever hands you a tidy consensus, it has failed silently.
4. **Verdicts trace to observations.** "Who was right" is decided at `falsify`
   by a pre-registered test, never at the divergence stop by judgement. Without
   a falsify observation the ledger reads `unresolved` (Modes A and B); a Mode
   C run, having nothing to compare, reads `no-comparison` whether or not
   `falsify` ran. The non-member side is adjudicable only where the compared
   claim - the instinct, or Mode B's prior analysis - coincides with a
   hypothesis the members generated independently.

## Extending

Members are discovered at run time from `.claude/agents/mc-*.md`. Drop in a new
one and it is adopted on the next run - the skill is never edited. See
MEMBER-TEMPLATE.md. Domain is a free string; the shipped members declare `code` and `any`.

## Five ceilings

Isolation gives members independent *conversational* context and nothing more.
`SKILL.md` states all five in full.

1. **Shared priors.** Shared weights; isolation decorrelates context, never
   training. Partial lever: run `mc-adversary` on a different model family.
2. **Shared ambient layer.** An identical harness layer in every member,
   ~28,500 tokens against a 257-token prompt in run 001. No lever.
3. **Harness-forwarded parent state.** In run 002 a stale repository-state
   snapshot reached members outside `receives` and outside the director's
   control. The name records its inferred origin - parent-forwarded rather
   than harness-computed is inference, not observation. No lever.
4. **Member tool grants.** Read/Grep/Glob reach quarantine-class material
   sitting anywhere in the working tree, tracked or not - one grep for an
   error string lands a member in the file the quarantine withheld. Lever only
   between runs: keep such material out of the tree.
5. **The director holds everything.** Withholding is mechanical once the
   director has decided to withhold; the deciding is discipline, not
   structure.

Run figures come from `.metaconcert/ledger.md` (runs 001 and 002) — a local
record, gitignored and absent from the repository's commit history, so not
independently checkable from the repo alone.

Member agreement is therefore weaker evidence than member divergence, and
self-reported membrane compliance is not evidence at all. No shipped member can
read its own token count (a borrowed agent's grant may differ - check), so the
only mechanical check is the size of the prompt the director constructed - a
weak proxy, not a measurement of what arrived.

## Honest limits

- The member/bias mapping is **design intent, not measurement**. Biases do not
  partition cleanly; several members touch several. Treat this table as what
  each role was built to resist, not as a proof it does.
- The whole protocol is **untested**. The `ledger` phase exists to change that.
  Until it has thirty entries you have a hypothesis, not a method.
