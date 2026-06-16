# Hermes Setup Notes

This repo is a working space for designing a personal Hermes Agent setup.

Current focus:

- A memory architecture that is useful without exposing everything.
- A default workflow that helps with project planning, day-to-day prioritization, and long-term direction.
- A draft `SOUL.md` that makes the agent calm, objective, privacy-aware, and values-oriented.

Start here:

- [docs/memory-setup.md](docs/memory-setup.md)
- [docs/workflows.md](docs/workflows.md)
- [SOUL.md](SOUL.md)

## Current Recommendation

Use a small layered setup:

- `USER.md` for stable preferences and personal operating style.
- `MEMORY.md` only for tiny always-relevant operational context.
- Holographic as the first external recall provider.
- Obsidian as the human-readable knowledge garden and shared source of truth for notes, world facts, decisions, and project context.

Expose only an agent-safe subset of Obsidian to Hermes. Do not give the default agent direct access to private journaling. If Holographic feels too opaque after a few weeks, test ByteRover next because it is more inspectable and Markdown-like.

