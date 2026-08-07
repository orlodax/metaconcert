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
| **mc-builder** | Sunk cost; scope creep; inherited rationale | Receives the decision, not the deliberation; halts on map/reality contradiction instead of repairing the map and continuing | Medium |
| **mc-adversary** | Automation bias; IKEA effect; fluency illusion at review | No rationale in context; cannot return a clean verdict without enumerating checks and evidence; verifies by execution not by reading | High (Opus, different family) |
| **Director** | Re-centralisation; consensus pressure; premature synthesis | Enforces the membrane, surfaces divergence unresolved, never forms a view | Free |

## The three cross-cutting rules

1. **Independent, then compare. Never converge.** Agreement between members that
   shared a frame is an echo. Only agreement between members that could not see
   each other is evidence.
2. **Artifacts cross the membrane, reasoning does not.** Rationale is the vector
   by which one member's blind spot becomes everyone's.
3. **The human reconciles.** Every divergence lands on you, unsmoothed. If the
   workflow ever hands you a tidy consensus, it has failed silently.

## Extending

Members are discovered at run time from `.claude/agents/mc-*.md`. Drop in a new
one and it is adopted on the next run - the skill is never edited. See
MEMBER-TEMPLATE.md. Domain is a free string; the shipped members declare `code` and `any`.

## Two ceilings

Isolation gives members independent *conversational* context. It does not give
them independent *priors* (shared weights) or independent *ambient* context
(identical harness layer, ~28,500 tokens in this project's first run). Member
agreement is therefore weaker evidence than member divergence, and self-reported
membrane compliance is not evidence at all - verify by token accounting.

## Honest limits

- The member/bias mapping is **design intent, not measurement**. Biases do not
  partition cleanly; several members touch several. Treat this table as what
  each role was built to resist, not as a proof it does.
- Members share a training lineage. Isolation decorrelates their *context*, not
  their *priors*. Run mc-adversary on a different model family to buy partial
  decorrelation - partial, never full.
- The whole protocol is **untested**. The ledger in Phase 7 exists to change
  that. Until it has thirty entries you have a hypothesis, not a method.
