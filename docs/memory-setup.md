# Memory Setup

## Recommendation

Start with this three-layer setup:

1. Hermes built-in memory: `MEMORY.md` and `USER.md`.
2. One external provider: Holographic.
3. Obsidian as an explicit, curated knowledge base, not as raw unrestricted memory.

This fits the goals best because privacy, local-first operation, low setup cost, and evolvability matter more right now than benchmark chasing or cloud-scale memory.

Hermes' own docs say built-in memory remains active even when an external memory provider is enabled, and only one external provider can be active at a time. That means the provider choice should be treated as the deeper recall layer, not as the only memory system.

Sources:

- Hermes memory provider docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/memory-providers.md
- Hermes persistent memory docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/memory.md
- Hermes profiles docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/profiles.md
- Holographic overview: https://hindsight.vectorize.io/guides/2026/04/21/guide-hermes-agent-holographic-memory-technical-deep-dive
- Mem0 OSS docs: https://docs.mem0.ai/open-source/overview
- OpenViking docs: https://docs.openviking.ai/
- ByteRover Hermes docs: https://docs.byterover.dev/autonomous-agents/hermes

## Memory Layers

### Hot Memory

Use `USER.md` for stable facts about you:

- Communication preferences.
- How much pushback you want.
- Your timezone and practical defaults.
- Long-lived preferences around privacy, planning, coding, and learning.

Use `MEMORY.md` for stable operational context:

- Current important projects.
- Tools, machines, repos, and conventions.
- Repeated lessons the agent should apply.
- A short pointer to where approved Obsidian context lives.

Do not put raw journal-like material here. These files are injected into the prompt, so they should be small, deliberate, and high-trust.

### External Provider

Use Holographic first.

Why:

- It is local SQLite.
- It has no required external service.
- Hermes documents it as having FTS5 search, trust scoring, and HRR-style compositional recall.
- Auto-extraction is off by default, which is good for a privacy-conscious first setup.

Suggested posture:

- Keep `auto_extract` off at the beginning.
- Ask the agent to store facts explicitly.
- Use feedback when recall is helpful or wrong.
- Review/delete facts periodically.

The main weakness is inspectability. Holographic is not a clean human-edited markdown knowledge tree. If you want to hand-edit memory heavily, ByteRover is the better experiment.

### Obsidian

Keep Obsidian as the durable personal knowledge base. It already matches your taste: markdown, links, areas, projects, and manual editing.

Do not expose the entire vault. Keep a whitelist boundary:

- Allowed: `areas/tech`, `areas/math`, `areas/workflows`, selected `projects/*`, books/notes you are comfortable sharing.
- Excluded: journaling graph, private life logs, raw emotional processing, sensitive personal records.

Add an agent-facing folder such as:

```text
Sync/wiki/areas/ai_agent_context/
├── index.md
├── values.md
├── current-projects.md
├── privacy-boundaries.md
├── decision-log.md
└── recurring-workflows.md
```

The agent can read from this folder freely and propose edits elsewhere only when asked.

## Provider Comparison

| Provider | Best Fit | Pros | Cons | My Take |
| --- | --- | --- | --- | --- |
| Holographic | Local private recall | SQLite, no service, fast, trust scoring, low setup | Less transparent than markdown; newer/unusual model | Best first choice |
| ByteRover | Inspectable developer memory | Local-first, hierarchical tree, CLI, optional sync, more human-curatable | Extra CLI; still another system beside Obsidian | Best second experiment |
| Hindsight | Strong structured recall | Knowledge graph, entity resolution, local or cloud, strong benchmark story | Embedded Postgres and LLM dependency; more moving parts | Good later if recall quality matters more than simplicity |
| OpenViking | Structured context database | Filesystem-like hierarchy, tiered L0/L1/L2 loading, self-hosted | Requires running service; AGPL; likely operational overhead | Interesting but not day one |
| Mem0 | Production memory layer | Mature ecosystem, OSS option, semantic search/dedup | Hermes docs emphasize API key/cloud path; self-hosting is heavier | Good for app dev, less ideal for personal default |
| Honcho | User modeling | Dialectic user model, profile/user peer design | Cloud or self-host service; stores behavioral model | Powerful but privacy-sensitive |
| RetainDB | Cloud team memory | Hybrid search, typed memories, API | External API and paid service | Not aligned with privacy-first default |
| Supermemory | Cloud semantic recall | Profile recall, graph ingest, container tags | Cloud API | Useful, but not the privacy-first baseline |

## Privacy Primitives

Use these as design rules:

- Explicit scope: The agent only reads approved folders unless you ask otherwise.
- Memory classes: mark facts as `public`, `private-but-usable`, `sensitive`, or `never-store`.
- Source labels: every durable memory should say where it came from when possible.
- Expiry: some facts should expire, especially preferences, emotional states, and temporary project constraints.
- Review cadence: weekly for active projects, monthly for user profile and values.
- No raw journaling ingestion: the agent may help reflect if you paste text, but it should not retain the raw text unless explicitly asked.

## Obsidian Structure Thoughts

Your current PARA-inspired structure is good enough. I would not migrate the whole vault now.

I would make two small changes:

1. Add an agent-approved context area.
2. Add lightweight project index files.

Suggested project file:

```markdown
# Project: learning_zig

## Outcome

What success looks like.

## Current State

What is true right now.

## Next Moves

- One concrete next action.
- One follow-up.

## Decisions

- YYYY-MM-DD: Decision and reason.

## Open Questions

- Things the agent should help clarify.
```

This gives Hermes useful structure without forcing the whole vault into a rigid system.

## Decision

Default agent:

- Built-in `MEMORY.md`/`USER.md`: enabled.
- External provider: Holographic.
- Obsidian: read/write only within an approved context folder by default.
- Profiles: stay with one default profile until a separate coding or automation agent has a clear reason to exist.

Exit criteria for switching away from Holographic:

- Recall feels opaque and hard to correct.
- It stores too much low-value context.
- You often want to browse/edit memories manually.
- Project memory wants a visible hierarchy.

If that happens, test ByteRover next.

