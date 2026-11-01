---
name: babysteps
description: Replan an implementation plan into truly atomic baby steps instead of big vertical slices. Use when the user wants to break a plan into steps, pushes back that a step is too big, or uses phrases like "baby steps" or "step by step".
---

Tear this plan apart and rebuild it as truly atomic baby steps.

Kill every "vertical slice" that bundles several pieces together just because they touch one user flow. Server + auth + realtime + UI in one step is not small, it's several steps wearing a trenchcoat.

Each step must leave something working and finished for the little it does, never a broken fragment. "Doesn't do much yet" is fine. "Half-wired and would break if used" is not.

Each step ends at a natural commit boundary, verifiable on its own, "it runs, it renders, it responds", without the next step needed to prove it did anything.

To replan an existing plan, lay out the whole resulting staircase at once. To build from scratch with no existing plan, propose only the next step, the right one after that only becomes obvious once this one is done and committed.
