---
name: write-skill
description: Writes a new skill from the conversation, or rewrites an existing one if given its path, so that it meets our standards.
disable-model-invocation: true
---

Your objective is to write a skill that meets our standards. Do NOT interview the user: synthesize what you already know and stop only at the checkpoints.

- With an existing skill path: you are **rewriting** that skill.
- Without an existing skill path: you are **creating** a new one from the conversation.

## Process

1. **Starting point.** When rewriting, read the whole skill, including its external files. When creating, synthesize the conversation.
2. **[Checkpoint] Trigger.** Propose user-invoked or model-invoked, reasoning about its cost, and a name. When creating, ask the user where to save it.
3. **[Checkpoint] Leading words.** Propose the leading words you will repeat in the skill and confirm them with the user.
4. **Write** the skill applying our standards.
5. **Cleanup.** Go over the skill and remove what's unnecessary according to the Cleanup section.
6. **[Checkpoint] Overwrite** (When rewriting). Show the user what you are going to remove before overwriting.

## Our standards

### Trigger

- **User-invoked** (`disable-model-invocation: true`): the description doesn't reach the agent. It costs **cognitive load**, the user has to remember it, so the name is the interface and must be short and memorable.
- **Model-invoked**: the description is a **context pointer** that always lives in the context. It costs **context load** on every request and unpredictability: the agent may not invoke it even when it fits.

### Structure

- A skill is made of **steps** (the procedure) and **references** (what the steps need). It can have only one of the two.
- The `SKILL.md` must be as small as possible.
- Identify the **branches**: the different paths the skill can take. Reference used by only one branch goes in an external file, behind a context pointer: "If you need X, read `x.md`".

### Steering

- **Leading words**: terms that condense a lot of meaning and activate what the model already knows ("vertical slice", "tracer bullet"). They replace paragraphs of explanation. Always repeat them in the same form so the agent adopts them in its reasoning.
- **Leg work**: if the agent rushes through a step because it sees the final goal, split the skill into separate skills to hide the following steps from it.

### Language

Write the skill in English, even if the conversation is in another language.

### Cleanup

- **Single source of truth**: each idea lives in only one place, also across external files.
- **Sediment**: whatever was added without structure goes to its branch; whatever is stale or irrelevant, out.
- **No-ops**: instructions that don't change the agent's behavior. Apply the **deletion test**: if the agent would behave the same without it, delete it.
