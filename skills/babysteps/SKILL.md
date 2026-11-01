---
name: babysteps
description: Break an implementation plan into small, natural commits, each one quick to review and verifiable on its own. Use when the user wants to break a plan into steps, pushes back that a step is too big, or uses phrases like "baby steps" or "step by step".
---

Take this plan and rebuild it as baby steps, one natural commit each. Lay out the whole resulting staircase at once.

Split by the seams a developer would commit at, for example:

- Data contract
- Endpoint
- Client service
- View
- Wiring them together

Remember that these are examples, not a checklist. Use the seams that fit the plan.

A step that bundles several seams is several steps wearing a trenchcoat.

Each step must leave something working and finished for the little it does, never a broken fragment. "Doesn't do much yet" is fine. "Half-wired and would break if used" is not.

Each step is small enough to review in a couple of minutes and verifiable on its own, "it runs, it renders, it responds", without the next step needed to prove it did anything.
