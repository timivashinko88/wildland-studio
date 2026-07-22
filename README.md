# Wildland — Studio & Workflow

**A solo-directed, AI-orchestrated AAA open-world game.**

![Engine](https://img.shields.io/badge/Unreal%20Engine-5.8-0E1128?logo=unrealengine&logoColor=white)
![Language](https://img.shields.io/badge/Core-C%2B%2B-00599C?logo=cplusplus&logoColor=white)
![Gameplay](https://img.shields.io/badge/Gameplay-Blueprints-2A2A72)
![VCS](https://img.shields.io/badge/Assets-Perforce-404040)
![Platform](https://img.shields.io/badge/Platform-PC%20(controller--friendly)-1f6feb)
![Target](https://img.shields.io/badge/Perf-144fps%20%40%201440p-3fb950)
![Status](https://img.shields.io/badge/Status-In%20Production-blue)

Wildland is a story-driven, third-person open-world action game — built and directed by **one
person** commanding a studio of specialized AI agents, with **every architectural, technical, and
creative decision made and owned by the director**.

This repository isn't the game. It's the **workflow** — how a single director builds an open-world
title at a AAA quality bar by combining hands-on engine work with a disciplined, gated, multi-agent
production pipeline. The game's design, assets, and source live in a private depot; what's public
here is the *method*.

> **The models are not the bottleneck. The process is.** A frontier model with no grader produces
> mediocrity confidently; a mid-tier model behind a savage review gate produces good work. Excellence
> is a property of the process that refuses to accept less.

---

## What I actually do here

I'm the director, architect, and sole authority on this project. Concretely, hands-on, every day:

- **Architect the systems** — I decide *where* every system lives before *how* it works: the C++
  character core, the athletic locomotion layer, the transformation state machine, world streaming,
  the camera, the frame budget. Architecture before implementation, always.
- **Drive the engine directly** — I operate Unreal Engine 5.8 day to day: the C++/Blueprint split,
  Nanite and foliage pipelines, material graphs, lighting and atmosphere, Movie Render Graph capture,
  and Perforce for all binary assets.
- **Build and wire the pipeline** — the multi-agent studio, the build/verify gates, the measurement
  tooling, the model-routing policy, and the automation that lets production run unattended are things
  I designed and maintain.
- **Own every visual and technical call** — nothing ships on look, feel, or performance without my
  explicit sign-off. Agents propose; I decide. Silence is never approval.
- **Integrate the tools** — engine plugins, MetaHuman, the 3D/asset toolchain, capture and QA
  scripts. The AAA look comes from *art direction → lighting → integration*, and I own that seam.

The AI studio is a force multiplier, not a replacement for judgment. It handles the volume; I hold
the bar.

---

## The core idea: a one-person studio that behaves like a real one

A real studio has specialists, a review pipeline, and gates that stop bad work from shipping. I
rebuilt that as a set of wired agents, each with a narrow job and a hard rule it can't cross:

| Role | Job | Gate it enforces |
|------|-----|------------------|
| **Feasibility Scout** | Research-first — find the wall in 30 minutes, not after 4 hours | Nothing hard starts unproven |
| **Build/Verify Runner** | The objective referee — compiles, runs tests, measures perf | "It should work" is never accepted; only real tool output |
| **Art Adversary** | Red-teams every visual against the AAA reference bar | No render reaches me ungated |
| **Taste Curator** | Keeps the work on *the game I actually want*, not just "good" | Quality ≠ correct direction |
| **Pipeline Medic** | Owns every tool/import/version error, ledger-first | Errors never derail the main session |

Each is adversarial *by design*. The point isn't to get an agreeable answer fast — it's to make bad
work fail loudly before it costs anything.

---

## The workflow

**Plan → Build → Verify → Review → Commit.** Never skip a stage.

```
        ┌─────────┐     ┌────────┐     ┌──────────┐     ┌─────────┐     ┌─────────┐
        │  PLAN   │ ──▶ │ BUILD  │ ──▶ │  VERIFY  │ ──▶ │ REVIEW  │ ──▶ │ COMMIT  │
        │ architect     │ small  │     │ compile/ │     │ adversar-     │ atomic, │
        │ first   │     │ diffs  │     │ measure  │     │ ial pass │     │ with why│
        └─────────┘     └────────┘     └────┬─────┘     └────┬────┘     └─────────┘
                                            │                │
                                     fails? └──── fix the ───┘
                                            foundation, don't stack on it
```

Two principles do the heavy lifting:

- **The oracle principle.** AI builds the game with minimal human clicking *to exactly the extent
  that I can build graders.* Every hour spent building an oracle buys back ten hours of unattended
  agent work. Gated work (compiles? tests pass? within budget?) runs free; load-bearing systems
  propose *through* the gate, never as a one-shot.
- **Measure, don't look.** Geometry questions get **numbers**, never pixels. *Is it floating,
  clipping, seated, the right scale?* is a measurement, answered with mesh tooling before any
  screenshot is taken. Taste questions — *does it look right?* — are the only ones that reach a
  human eye, because that's the only place human judgment is irreducible.

Full detail: **[docs/workflow.md](docs/workflow.md)** · **[docs/principles.md](docs/principles.md)**

---

## Engineering standards (non-negotiable)

- **Build it once, build it right.** Speed comes from not redoing work, never from cutting corners.
- **Foundation-first.** Lowest layers first, hardened under stress before anything stacks on them.
  A stage is done when it's smooth and glitch-free *under load*, not when it "works once."
- **Data-driven.** Tunable values live in config, never hardcoded in logic.
- **Separation of concerns; single source of truth for state; composition over inheritance.**
- **No magic numbers, no god classes, no copy-paste, no dead code.**
- **Fail loud in dev, safe in ship.** Never silently swallow an error.
- **`main` always builds.** Broken code never lands.
- **Readable over clever.** Comment the *why*, not the *what*.

---

## Tech stack

- **Engine:** Unreal Engine 5.8
- **Code:** hybrid — C++ for the core and anything performance-sensitive; Blueprints for gameplay,
  UI, and fast iteration
- **Characters:** MetaHuman base with a fully custom outfit/gear pass
- **World:** Nanite geometry, scanned foliage and material libraries, custom terrain, dynamic
  lighting and atmosphere
- **Capture/QA:** Movie Render Graph with an automated render-validity gate
- **Version control:** Git for the design/workflow layer, Perforce for all binary game assets
- **Automation:** a multi-agent production pipeline with build-gated verification and adversarial
  visual review

---

## Quality doctrine

The reference bar is fixed: **RDR2, GTA V, and Horizon Forbidden West.** Every asset is judged
*side-by-side with a real reference screenshot from those games* — never in isolation, because the
eye is great at comparison and terrible at recall. That single habit is what kills quality drift:
you never compare today's work to yesterday's, only to the bar.

RDR2 and Horizon were made with zero AI. That's the point — the tooling changed, the standard didn't.

---

## Status

**In production.** Milestone 1, *"First Playable"* — a great-looking third-person character, beautiful
open-world roaming, and a signature traversal mechanic, smooth and glitch-free — is the current
target. Foundation systems (character core, athletic locomotion, world environment) are built and
being hardened.

---

*Directed, architected, and built by [@timivashinko88](https://github.com/timivashinko88).*
