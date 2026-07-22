# Principles

The doctrine behind Wildland's production. Short, opinionated, and load-bearing — these are the rules
that decisions get checked against.

## On quality

**The models are not the bottleneck. The process is.** RDR2 and Horizon Forbidden West were made with
zero AI. A frontier model with no grader produces mediocrity confidently; a mid-tier model behind a
savage review gate produces good work. Upgrading the model raises the ceiling; only the process raises
the floor.

**Never judge an asset in isolation.** Every visual is reviewed side-by-side with a real reference
screenshot from the bar — RDR2, GTA V, Horizon Forbidden West. Quality drift never comes from
approving something obviously bad; it comes from comparing today's work to *yesterday's* instead of to
the bar. The eye is great at comparison and terrible at recall. Force the comparison and drift dies.

**The AAA look is art direction → lighting → integration, not raw asset quality.** Money and effort go
where they can't be faked; everything else is bought, scanned, or generated as a base and then
directed.

## On engineering

**Build it once, build it right.** Speed comes from not having to redo work, never from cutting
corners.

**Foundation-first. Stabilize before you stack.** The lowest layers get built and hardened first,
under stress, because everything rests on them. A stage isn't done when it works once — it's done when
it's smooth and glitch-free under load. You don't build on unstable ground.

**Harden the break-worthy things early** — movement, physics, collision, streaming, the transformation
state switch, save/load, camera, frame budget — while they're cheap to fix and nothing depends on them
yet.

**Fail loud in dev, safe in ship.** A swallowed error is a bug you'll pay for later with interest.

**Don't over-engineer.** Right means clean, correct, maintainable, and *appropriately* simple — not
maximally abstract. Prove the thing is good before polishing it.

## On autonomy

**Autonomy scales with graders, not with model count.** The project is automated to exactly the extent
that oracles exist. Build the grader and the machine runs free; skip it and you're gambling.

**Parallelize independent threads, never a single judgment.** Stacking agents on one un-gradeable call
just produces the same answer faster.

**Measure, don't look.** Geometry gets numbers; only taste gets eyes.

## On judgment

**Ask, don't guess** on anything load-bearing or sensitive. A wrong guess locked in early is expensive
to unwind.

**One authority on look and feel.** Nothing that affects how the game looks or sounds is final without
an explicit yes from the director. Consensus isn't approval; silence isn't approval. This overrides
speed, every time.

**Respect the setting.** The world is built with care and specificity, never stereotype — cultural
detail is researched and consulted, never invented and locked from assumption.

---

*The through-line: excellence isn't something a tool gives you. It's a property of a process that
refuses to accept less — and then automates everything that process can check.*
