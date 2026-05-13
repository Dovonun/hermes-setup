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

Use Hermes' built-in `MEMORY.md` and `USER.md` as the hot, always-in-context layer, then start with the Holographic provider as the single external provider.

Keep Obsidian as the source-of-truth knowledge garden, but expose only an agent-safe subset to Hermes. Do not give the default agent direct access to private journaling. If the Holographic layer feels too opaque after a few weeks, test ByteRover next because it is more inspectable and markdown-like.

