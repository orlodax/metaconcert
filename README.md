# Metaconcert

An on-demand agent workflow for Claude Code that treats cognitive bias as an
engineering problem rather than a personality trait.

**Status: untested.** This is a design and a measurement instrument, not a
validated method. It ships with a ledger because the honest thing to do with an
untested protocol is instrument it, not advertise it. If you run it, the numbers
are the interesting part.

---

## The premise

Bias does not merely survive contact with an LLM. It amplifies.

A human colleague is a lossy, high-friction channel. Hand them a bad premise and
you get confusion, a dumb clarifying question, visible reluctance — friction that
leaks information about your error back to you. An LLM has near-zero frame
friction. It accepts the premise, elaborates it fluently, and returns something
that reads like corroboration. Prior in, better-argued prior out.

Four channels carry your bias into agentic work:

1. **Specification** — you encode the diagnosis, not the symptom. *"Fix the race
   condition in the pool"* has already committed the agent to your hypothesis.
2. **Omission** — what is obvious to you goes unsaid, and the gap is filled with
   the modal pattern from training. Fails silently: no error, just plausible
   wrongness shaped like the average of the internet.
3. **Evaluation** — you become a monitor rather than an operator, reviewing
   maximally fluent artifacts. The role humans perform worst, handed the most
   convincing possible input.
4. **Persistence** — in a human team, bad framings decay because people forget
   and re-derive. In a session, your opening frame is literally in the context,
   re-read every turn. It cannot decay.

Metaconcert restores friction by construction between members, and by
discipline at the director: once the director decides to withhold something,
the withholding is mechanical — the deciding never is, and that weaker second
guarantee is named here rather than hidden.

## The mechanism it rests on

A subagent gets a **fresh conversational context**, and what the parent puts in
the prompt string is the parent's deliberate channel into it. That makes every
handoff **a membrane whose permeability you specify** for the material the
parent composes.

It does not make the member's context empty. Alongside your prompt sits an
**ambient layer** — harness instructions, tool definitions, environment and
project files — measured at roughly 28,500 tokens against a 257-token prompt in
this project's own first run (`ledger.md`, run 001 — a local record, gitignored
and absent from the repository's own commit history, so this figure is not
independently checkable from the repo alone). That layer is not suppressible and
should not be: it is what makes a member a capable agent rather than a bare
completion.

So the guarantee is narrower than it first looks, and worth stating exactly:
**exclusion is structural for the material the director composes and chooses to
withhold; exclusion of everything else is not.** Run 002 located the edge of
that scope: a stale snapshot of repository state reached members outside the
prompt string entirely, and the director cannot suppress it (`ledger.md`, run
002 — same uncheckable-from-repo caveat as above). That it was the parent
session's state forwarded down, rather than harness-computed, is inference;
that it arrived outside the director's reach is not.

An earlier version of this README claimed the prompt string was the only
channel into a member's context. That was false, and the project's own protocol
is what caught it — see `ledger.md`, run 001 (same caveat).

## The shape

A director — a skill running in your main session — enforces a protocol and is
forbidden from forming a view. Members are subagents, each denied something
specific, each producing a fixed-format artifact.

    intake → map → hypothesise → [DIVERGENCE STOP] → falsify →
    specify → [OPEN QUESTIONS STOP] → build → attack → [RECONCILE STOP] → ledger

Three rules do the work:

1. **Independent, then compare. Never converge.** Agreement between members that
   shared a frame is an echo. Only agreement between members that could not see
   each other is evidence.
2. **Artifacts cross the membrane, reasoning does not.** Rationale is the vector
   by which one member's blind spot becomes everyone's.
3. **The human reconciles.** Divergence is surfaced unresolved. If the workflow
   ever hands you a tidy consensus, it has failed silently.

## The number

**Divergence rate**: how often an independently derived diagnosis disagreed with
the belief quarantined at intake — and how often the independent one was right.
The human's side of that second question is adjudicable only when the
quarantined instinct coincides with a hypothesis the members generated
independently; otherwise the ledger records the divergence and leaves
adjudication open.

That number is normally unobtainable. You type your instinct into the prompt and
destroy the measurement before anything can be compared against it. Metaconcert
holds the instinct back so the comparison survives.

## Install

Copy `.claude/agents/mc-*.md` and `.claude/skills/metaconcert/` into a repository
or into `~/.claude/`. Existing agents are untouched — the `mc-` prefix and the
"never select proactively" clause in every description keep these out of normal
routing, and the skill is `invocation: user`, so it runs only when called.

    /metaconcert i keep getting a 500 on retry uploads, only under load
    /metaconcert work on issues/backend-defects.md
    /metaconcert item 42 of issues/backend-defects.md

No required format. The director resolves the reference, echoes back what it
resolved to, and waits before spending anything.

## Read next

- `manual.html` — every step of a run, from the clean session to the ledger
  entry, with diagrams; open it in a browser
- `CHEATSHEET.md` — which member controls for which failure mode, and the honest
  limits of that mapping
- `INTEGRATION.md` — how to run it, when not to, and how to borrow the agents a
  repository already has
- `MEMBER-TEMPLATE.md` — adding a member or a domain without editing the skill

## When not to use it

Almost always. This costs many multiples of a normal session in tokens and in
attention. Architect/builder/tester exists to divide labour and optimises for
information flowing *freely* downward — which is correct, and which Metaconcert
deliberately breaks. It does not replace that pattern; it is `git bisect` for
reasoning. Reach for it when the cheap loop has already failed twice, or when a
silent error would be expensive.

Run it as your default and you will hate it inside a week, abandon it, and lose
the data. That is the realistic failure mode — not that it does not work.

## Honest limits

- The member/bias mapping is **design intent, not measurement**. Biases do not
  partition cleanly.
- **Five ceilings on independence, not two.** Shared priors — isolation
  decorrelates *context*, never *priors*. An identical ambient layer in every
  member. Harness-forwarded parent-session state: run 002 saw a stale
  repository-state snapshot reach members outside the director's control — the
  name records its origin as inferred, not observed
  (`ledger.md` — same uncheckable-from-repo caveat as above). Member tool
  grants, which reach quarantine-class material sitting anywhere in the working
  tree, tracked or not. A director that holds everything: withholding is
  mechanical once decided, and the deciding is discipline, not structure. Only
  the first has a lever inside a run — the `attack` phase on a
  different model family, and it is partial; the fourth has one only between
  runs, by keeping such material out of the tree. `SKILL.md` states all five in
  full.
- **Member self-report is not verification.** Convergent membrane reports from
  members sharing an ambient layer and identical reporting instructions are one
  measurement taken N times. No shipped member can read its own token count
  either (a borrowed agent's grant may differ — check), so the only mechanical
  check is the size of the prompt the director built — a weak proxy, not a
  measurement of what arrived.
- **Invocation is selected on failure.** The protocol is reached for only after
  the cheap loop has already failed — so every run is drawn from problems
  pre-selected for the human's instinct having been wrong. That inflates both
  the measured divergence rate and the member-win rate. The control arm in the
  pilot design corrects for it only partially.
- **No efficacy data exists.** The ledger is how that changes. Until it has
  thirty entries with a control arm, this is a hypothesis with good ergonomics.

## Licence

MIT. See `LICENSE`.

## Name

Julian May's metaconcert: independently operant minds fused under a director. In
those books the coordinator is the failure point — a corrupt director turns the
whole apparatus into an amplifier for one mind's intent. Hence a director here
that enforces protocol and is forbidden from having a view.
