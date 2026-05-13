# Workflows

## Goal

The agent should make you more capable, not more dependent.

The useful version of Hermes is not a machine that tells you what to do. It is a thinking partner that helps you slow down, reframe, choose the next action, and keep long-term values visible when the local situation feels noisy.

## Default Operating Loop

Use one default profile at first.

Daily loop:

1. Review active projects and commitments.
2. Pick one main path for the day.
3. Identify the smallest meaningful next action.
4. Check whether the plan respects energy, health, relationships, and long-term goals.
5. End with a short memory review: what should be retained, updated, or forgotten?

Project loop:

1. Define the outcome.
2. List current constraints.
3. Identify unknowns.
4. Create a first implementation plan.
5. Execute in small steps.
6. Record decisions and lessons in the project note.

Reflection loop:

1. Describe the situation plainly.
2. Separate facts, interpretations, feelings, and obligations.
3. Ask what matters long term.
4. Pick the next action that keeps the path intact.
5. Store only the distilled lesson, not the whole emotional transcript.

## Values-Oriented Reframing

Short quotes can help, but they are too small when you are deep in a difficult project or mentally overloaded. The agent should translate values into practical questions.

Example: "Focus on the path, not the trees."

The agent should ask:

- What is the actual path here?
- Which detail is consuming attention without changing the outcome?
- What would future-you be glad you protected today?
- What is the next honest step, even if it is small?

The point is not motivational language. The point is regaining altitude.

## Kanban

Use Kanban for project execution, not identity or values.

Suggested columns:

- Backlog
- Clarify
- Ready
- Doing
- Waiting
- Done

Rules:

- `Doing` should usually have one item.
- `Clarify` is for fuzzy tasks, not a dumping ground.
- Each card should have a concrete next action.
- Decisions belong in the project note, not only on the card.

## Profiles

Hermes profiles are isolated Hermes homes. The docs describe each profile as having its own config, API keys, memory, sessions, skills, gateway state, and `SOUL.md`.

Start with one default profile.

Create another profile only when one of these becomes true:

- The agent needs different tools or permissions.
- The memory should be intentionally separate.
- The tone/persona should be meaningfully different.
- The work has a different risk profile, such as autonomous coding or server automation.

Likely future profiles:

- `coder`: dev work, repo context, tests, agentic coding.
- `planner`: life planning, goals, weekly review.
- `archivist`: Obsidian cleanup and knowledge curation.

Do not split early just because profiles exist. Split when the memory boundary or permission boundary earns it.

## Memory Hygiene Workflow

At session end, ask:

- What did we learn that should persist?
- Is this a fact, preference, decision, pattern, or temporary state?
- Where should it live: `USER.md`, `MEMORY.md`, provider memory, project note, or nowhere?
- Is it sensitive?
- Should it expire?

Default storage rule:

- `USER.md`: stable preferences and durable personal operating style.
- `MEMORY.md`: stable environment/project facts.
- Holographic: searchable facts and patterns that may be useful later.
- Obsidian: human-readable knowledge, decisions, and project state.
- Nowhere: raw vents, temporary emotions, speculative guesses, private material.

## Questions To Answer Next

- What parts of the Obsidian vault should Hermes be allowed to read by default?
- Should Hermes be allowed to write to project notes, or only propose patches?
- Which private categories are hard `never-store`?
- How much pushback do you want when your stated plan conflicts with your values?
- Do you want a weekly review ritual with the agent?
- What are the 3-5 long-term goals Hermes should keep visible?

