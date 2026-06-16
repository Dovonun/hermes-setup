# Memory Setup

## Recommendation

Use a small, layered memory system:

1. Hermes built-in memory: `USER.md` and a very small `MEMORY.md`.
2. Holographic as the first external recall provider.
3. Obsidian as the human-readable, shared knowledge garden.

This keeps the setup local-first, inspectable where it matters, and simple enough to maintain.

Hermes built-in memory remains active even when an external provider is enabled, and only one external provider can be active at a time. Treat the provider as deeper recall, not as the whole memory system.

Sources:

- Hermes memory provider docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/memory-providers.md
- Hermes persistent memory docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/memory.md
- Hermes profiles docs: https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/profiles.md
- Holographic overview: https://hindsight.vectorize.io/guides/2026/04/21/guide-hermes-agent-holographic-memory-technical-deep-dive
- Mem0 OSS docs: https://docs.mem0.ai/open-source/overview
- OpenViking docs: https://docs.openviking.ai/
- ByteRover Hermes docs: https://docs.byterover.dev/autonomous-agents/hermes
- Ziwen Xu Obsidian/Codex vault post: https://x.com/ziwenxu_/status/2053241837453029439

## Memory Layers

### USER.md

Use `USER.md` for stable facts about you:

- communication preferences
- technical comfort level
- long-lived privacy preferences
- how much pushback you want
- durable preferences around planning, coding, learning, and reflection

### MEMORY.md

Use `MEMORY.md` only for tiny, always-relevant operational context.

Good examples:

- a primary host or repo that affects most sessions
- a broad pointer to where approved knowledge lives
- a rule that prevents repeated mistakes across many tasks

Avoid narrow implementation details, old task outcomes, PR numbers, ports, temporary decisions, and facts that are only useful for one project.

These files are injected into the prompt, so they should stay small, deliberate, and high-trust.

### Holographic

Use Holographic first.

Why:

- local SQLite
- no required external service
- FTS5 search, trust scoring, and compositional recall
- auto-extraction can stay off at the beginning

Suggested posture:

- keep `auto_extract` off at first
- ask the agent to store facts explicitly
- use feedback when recall is helpful or wrong
- review/delete facts periodically

The main weakness is inspectability. Holographic is not a clean human-edited Markdown tree. If you often want to browse or hand-edit memories, test ByteRover next.

### Obsidian

Use Obsidian as the durable shared knowledge base: Markdown notes that both you and Hermes can read and edit.

It is for:

- world facts and reference notes
- project context and decisions
- operating manuals
- values/rationale that should remain human-editable
- longer-form knowledge that should not live in always-on memory

Do not expose the entire vault by default. Keep an agent-safe boundary.

Allowed examples:

- selected tech/math/workflow areas
- selected project notes
- explicit agent context notes
- reference material you are comfortable sharing

Excluded by default:

- journaling graph
- private life logs
- raw emotional processing
- sensitive personal records

Your vault already roughly follows PARA. Keep that structure. Do not migrate the whole vault into a machine-first layout just because an agent will read it.

A simple shape is enough:

```text
AGENTS.md          # short map for Hermes
Inbox/             # raw captures and things to process later
Projects/          # active project notes and working context
Areas/             # ongoing responsibilities and systems
Resources/         # reference notes and world facts
Archive/           # inactive material
```

The folder names can match the vault's existing conventions. The important part is the role of each area, not exact capitalization.

Add a small vault-root `AGENTS.md` that explains:

- what the vault is for
- which folders Hermes may read/write by default
- where shared facts about the world belong
- how to update notes safely
- when Hermes should ask instead of guessing

Keep `AGENTS.md` as a map, not a second vault.

## World Facts

For shared facts about the world, prefer normal Markdown notes in `Resources/` or the relevant project/area folder.

A good fact note has:

- a clear title
- the fact or claim in plain language
- source links when available
- date/context if freshness matters
- links to related notes

Avoid over-structuring. If a fact needs querying, scoring, or deduplication, it may belong in Holographic or another app-specific store instead of hand-maintained Markdown.

## Syncthing

Syncthing is a good fit because Obsidian is just files, but conflicts are possible.

Conflicts can happen when:

- the same note is edited on two devices before either syncs
- Hermes rewrites a note while you are editing it elsewhere
- Obsidian plugins update JSON/workspace files on multiple devices
- mobile edits happen offline, then sync later

Keep conflict risk low:

- prefer small append-style or targeted edits over whole-file rewrites
- have Hermes read the latest file immediately before patching
- avoid agent-led bulk reorganizations without a plan
- sync notes and important config, but be cautious with plugin state
- consider excluding generated/ephemeral files such as `.obsidian/workspace*.json`
- let Syncthing create conflict copies rather than trying to auto-merge them blindly

Simple agent rule:

> Hermes may edit one note at a time after reading the latest version. For large reorganizations, draft a plan first.

## Provider Comparison

| Provider | Best Fit | Pros | Cons | My Take |
| --- | --- | --- | --- | --- |
| Holographic | Local private recall | SQLite, no service, fast, trust scoring, low setup | Less transparent than Markdown; newer/unusual model | Best first choice |
| ByteRover | Inspectable developer memory | Local-first, hierarchical tree, CLI, optional sync, more human-curatable | Extra CLI; still another system beside Obsidian | Best second experiment |
| Hindsight | Strong structured recall | Knowledge graph, entity resolution, local or cloud, strong benchmark story | Embedded Postgres and LLM dependency; more moving parts | Good later if recall quality matters more than simplicity |
| OpenViking | Structured context database | Filesystem-like hierarchy, tiered L0/L1/L2 loading, self-hosted | Requires running service; AGPL; likely operational overhead | Interesting but not day one |
| Mem0 | Production memory layer | Mature ecosystem, OSS option, semantic search/dedup | Hermes docs emphasize API key/cloud path; self-hosting is heavier | Good for app dev, less ideal for personal default |
| Honcho | User modeling | Dialectic user model, profile/user peer design | Cloud or self-host service; stores behavioral model | Powerful but privacy-sensitive |
| RetainDB | Cloud team memory | Hybrid search, typed memories, API | External API and paid service | Not aligned with privacy-first default |
| Supermemory | Cloud semantic recall | Profile recall, graph ingest, container tags | Cloud API | Useful, but not the privacy-first baseline |

## Privacy Primitives

Use these as design rules:

- explicit scope: the agent only reads approved folders unless asked otherwise
- memory classes: `public`, `private-but-usable`, `sensitive`, `never-store`
- source labels: durable memory should say where it came from when possible
- expiry: temporary facts should expire, especially preferences, emotional states, and project constraints
- review cadence: weekly for active projects, monthly for user profile and values
- no raw journaling ingestion: the agent may help reflect if text is pasted, but should not retain the raw text unless explicitly asked

## Decision

Default agent:

- Built-in `USER.md`/`MEMORY.md`: enabled.
- External provider: Holographic.
- Obsidian: read/write only within approved scope by default.
- Profiles: stay with one default profile until a separate coding or automation agent has a clear reason to exist.

Exit criteria for switching away from Holographic:

- recall feels opaque and hard to correct
- it stores too much low-value context
- memories need frequent manual browsing/editing
- project memory wants a visible hierarchy

If that happens, test ByteRover next.
