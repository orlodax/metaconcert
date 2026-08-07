# Integrating Metaconcert with existing project agents

## How to actually run it

**Metaconcert must open a clean session.** This is the part that is easy to get
wrong and fatal when you do.

If you spend a session working normally and *then* invoke the skill, the main
session context already contains your reasoning, your architect's reasoning, and
your preferred hypothesis. The director is supposed to hold no view; that session
holds several. Worse, the quarantine comes back empty - you already talked
yourself through the diagnosis, so there is nothing left to withhold and nothing
to measure divergence against.

**Correct — any of these:**

```
/clear
/metaconcert i keep getting a 500 on retry uploads but only under load,
             and only since we moved to the new pool
```
```
/metaconcert work on issues/backend-defects.md
```
```
/metaconcert item 42 of issues/backend-defects.md
```

There is no required format. The director resolves the reference the way any
session would, echoes back what it resolved to, and waits for you to confirm
before spending anything.

**Wrong:** brief your coordinator agent first, let it plan, then invoke the skill.
You have pre-committed every downstream member to a frame.

**Wrong:** ask a subagent to run Metaconcert. Triggers flow downward; a subagent
has no slash-command interface, and an architect-as-director is the failure mode
this design exists to avoid.

### On having a hunch

The director asks once whether you suspect a cause, and in the same breath for
your own estimate of what the work will cost. **"I don't know" is a complete
answer** to either and it will not ask again. The two are separate questions -
a hunch is about *why*, an estimate is about *how much* - and neither substitutes
for the other.

- **You have a hunch** → strongest run. Your belief is quarantined and compared
  against an independently derived diagnosis. That comparison is the one thing
  this workflow produces that nothing else can.
- **No hunch, but the source file already carries a diagnosis** → the comparison
  runs against that instead. Weaker: if the prior analysis came from an LLM,
  agreement is partly shared lineage rather than corroboration, and the director
  will say so.
- **Neither** → no causal divergence measurement this run, stated once and
  dropped. An estimate you did give is still compared against the forecast; that
  comparison does not depend on having a hunch. You still get the map with its
  assumptions exposed, ranked falsifiable hypotheses, blind-authored criteria,
  and adversarial review. That is most of the value.

Do not manufacture a hunch to feed the machine. A fabricated instinct produces a
fabricated divergence, and the ledger becomes worse than empty.

### What the run looks like

1. You send `/metaconcert` + brief.
2. Director discovers members, prints the plan, and waits. You confirm or adjust.
3. Phases run. The director stops at DIVERGENCE, at OPEN QUESTIONS, and at
   RECONCILE. At each stop it hands you unresolved artifacts and refuses to pick.
4. You pick. The run continues.
5. Ledger entry appended.

### When NOT to use it

Routine work. This costs many multiples of a normal session in tokens and in
your attention. It earns that on: bugs where your first two fixes failed,
irreversible or cross-repo changes, architectural decisions, and drafts that are
not working for reasons you cannot name. Everything else, use your normal agents.

## The rule that makes this cheap

A subagent's context starts fresh, and the only channel from parent to subagent
is the prompt string. Therefore **the membrane is enforced by the director's
prompt construction, not by the member's own definition.**

Consequence: existing agents can serve as Metaconcert members with ZERO
modification. You are not changing them; you are changing what reaches them.

## Direction of control

Triggers flow downward. Skills and commands are triggers; agents are workers.
A subagent has no slash-command interface, so **a coordinator agent cannot invoke
`/metaconcert`**. Do not try to build that. Even if nesting made it mechanically
possible, it is the wrong shape - see below.

## Why the architect must not run the Metaconcert

a coordinator agent holds project context and forms judgments. That is its value in
normal operation and its disqualification here. The director must have no view;
an architect-as-director puts your most context-saturated agent in the one seat
that has to be empty, and every downstream member inherits its frame.

Split the architect's two functions:

| Function | Inside Metaconcert? |
|---|---|
| Context authority - knows canon, conventions, history | Yes, as a supply-only member. Output passes through as an artifact, unsummarised. |
| Coordinator - decides, sequences, synthesises | No. Never. This is the director's structural role and the director is view-less. |

## Two modes, never mixed

**Ordinary work.** a coordinator agent coordinates its subordinates exactly as it
does today. Metaconcert is not involved. Nothing changes.

**Metaconcert run.** You invoke `/metaconcert` in the main session. The main
session is the director. It spawns `mc-*` members and, where useful, existing
project agents in constrained roles.

The two modes never nest. If a Metaconcert phase invokes an agent that spawns
its own subagents, uncontrolled context flow re-enters and the run is void.

## Using an existing agent as a member

Prefix its prompt with the constraint block:

```
Operating as a Metaconcert member for this invocation.
Use only the material below. Do not request additional context.
Do not spawn subagents. Do not coordinate other agents.
Return only the artifact requested.
---
<permitted material per the membrane table>
```

**Worker-shaped agents** (writers, implementers): safe. Call-site constraint is
sufficient. a worker agent receives intent spec + canon map, never the
deliberation.

**Coordinator-shaped agents** (architects, leads): constrained but degraded.
Call-site constraint controls the INFORMATION membrane; it does not prevent ROLE
DRIFT, because the agent's own system prompt still tells it to coordinate. Expect
it to try. If drift matters for a given role, build a thin `mc-` member instead
of constraining an existing one. This is a real limitation, not a caveat.

## Measurement

`.metaconcert/ledger.md`. The number that matters differs by track:

**Divergence rate**: how often the independently derived diagnosis disagreed with
the belief that was quarantined at intake, and how often the independent one was
right when it did.

That number is normally unobtainable, because normally you type your instinct
into the prompt and destroy the measurement before anything can be compared to
it.
