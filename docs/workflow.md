# The Workflow

How a single director ships an open-world game at a AAA bar without a traditional team. This is the
production process in depth — the five stages, the gates that enforce them, and the two ideas that
make unattended AI production actually work.

## The five stages — never skip one

Every non-trivial change moves through the same pipeline. Skipping a stage is how studios accumulate
the invisible debt that later ships as bugs and stutter.

### 1. Plan
Architecture before implementation. Before a line is written I settle *where* a system lives, what it
owns, how data flows through it, and how it will be tested. A plan is cheap to change; a shipped
system isn't. Load-bearing or culturally sensitive decisions are raised and settled explicitly — I
ask rather than guess.

### 2. Build
Small, focused increments. One task, small diffs, standards followed *as the work happens* rather
than bolted on after. The build runs from the foundation up — the lowest layers first, because
everything stacks on them.

### 3. Verify
Nothing is "done" because it looks done. It compiles, runs, and is exercised — under stress, not once.
Geometry is *measured*, not eyeballed. Performance is checked against the frame budget with real
numbers. The report says *how* it was verified, or it isn't a report.

### 4. Review
An adversarial pass whose job is to find the flaw, not to bless the work. Visuals are red-teamed
against the reference bar before I ever see them. Code is reviewed against the engineering standards.
The default posture is "what's wrong with this," not "this looks fine."

### 5. Commit
Atomic commits with a clear *why*. `main` is buildable at every point in history. The reasoning behind
a change is recorded, because six months later the *why* is worth more than the diff.

---

## The oracle principle

This is the single idea that makes AI production pay off.

> AI builds the game with minimal human intervention **to exactly the extent that graders exist.**

An agent with a grader is autonomous and trustworthy. An agent without one is a confident gambler.
The entire history of this project splits cleanly on that line: every *gated* task succeeded
unattended; every *ungated* one became a time sink. Not because of task difficulty — because of the
grader.

So the work is to build oracles:

- **Compiles?** The build runner is the referee.
- **Behaves correctly?** Automation tests are the referee.
- **Within budget?** The profiler is the referee.
- **Geometrically correct?** Mesh measurement is the referee.
- **Meets the visual bar?** The adversary screens it; a human makes the final call.

Every hour spent building an oracle buys back ten hours of unattended agent work. Gated work runs
free. Load-bearing systems — player control, the transformation state machine, streaming, camera —
propose *through* the gate, never as a one-shot, because those are the systems that break the game
when they break.

**Parallelism does not fix an ungated loop.** Three agents on one unmeasurable judgment produce the
same wrong answer three times faster. Independent threads parallelize; a single taste call does not.

---

## Measure, don't look

A corollary that saves enormous time.

Half of what feels like a visual question isn't one. *Is this asset floating? Clipping? Seated on the
ground? The right scale? Symmetrical?* — those are **measurements**, and a ruler answers them faster
and more reliably than an eye ever will. Answering a measurable question with a screenshot is a
process violation here.

Why it matters: a low-information render invites hallucination. An agent staring at an ambiguous image
*will* confidently narrate "it's sitting nicely now." A number won't lie, and measured work is
oracle-gated, so it runs unattended.

So every visual task splits in two:

- **Correctness / geometry** → the agent gets numbers, and runs free against them.
- **Taste** → a human gets good images, side-by-side with the reference bar.

Only the second needs human eyes — and it's the only place a human click is irreducible. Everything
else is automated.

---

## Time-boxing the un-gradeable

Some work genuinely has no automated pass/fail — it comes down to "does it look right." That work is
**time-boxed hard.** When the clock rings, the rule is to change the *approach*, not to keep nudging
the same numbers. Three rounds of "tweak a value and re-render" means the approach is already wrong.
Iterating on parameters with no grader has no natural stopping point except exhaustion — so the clock
is the stopping point.

Build-gated work is exempt: the referee *is* the grader, so it can iterate all night.

---

## The result

The division of labor is clean:

- **The pipeline** handles volume — compiling, measuring, screening, researching, the thousand
  mechanical steps.
- **I** hold the bar — architecture, direction, taste, and every call that decides whether the game
  is good.

That's what lets one person run a studio: not doing less, but building the graders that let the
machine do the parts a grader can check, and reserving human judgment for the parts it can't.
