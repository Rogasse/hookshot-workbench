# Rogasse's Hookshot workbench

Public notes and repeatable methods for testing and contributing to [Hookshot](https://github.com/NotRexed/Hookshot) from a Windows PC with an RTX 4050 Laptop GPU (6 GB). This repository records what was observed, what remains unproven, and the next useful test. It is independent of the Hookshot project.

Inspired by [mooki000/hookshot-workbench](https://github.com/mooki000/hookshot-workbench). Its Linux scripts and machine-specific paths are not copied here. The comparison and evidence principles are adapted to this PC.

## Start here

1. Read [AGENTS.md](AGENTS.md), then [docs/CURRENT.md](docs/CURRENT.md).
2. Read Hookshot's current [workflow](https://github.com/NotRexed/Hookshot/blob/main/docs/workflow.md), [AGENTS.md](https://github.com/NotRexed/Hookshot/blob/main/AGENTS.md), and [CONTRIBUTING.md](https://github.com/NotRexed/Hookshot/blob/main/CONTRIBUTING.md) before changing its source.
3. Check [docs/TASKS.md](docs/TASKS.md) and the linked issues/PRs for overlap.
4. Record completed work in [docs/WORKLOG.md](docs/WORKLOG.md), and update CURRENT and TASKS when their status changes.

On Rogasse's Windows PC, the local Codex workspace has an `AGENTS.md` pointer to this repository, and `skills/hookshot-context` is linked into the local Codex skills folder. Those local links help a new Hookshot session discover this context; the repository remains the canonical copy.

## Boundaries

This repository contains no game files, saves, keys, binaries, generated code, shader caches, logs, options file, credentials, or private local paths. Keep run artifacts on the PC. Publish only summaries and evidence allowed by Hookshot's contribution rules. Verify that `gh api user --jq .login` returns `Rogasse` before any GitHub write.

## Current focus

The v2.1.0 play logs show Kokiri Forest stutter near 20-30 real game FPS, heavy memory synchronization, and VRAM sometimes above the driver's allowance. The [report on #993](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011) is observational; it does not prove a fix. A local test of [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585) did not demonstrate an FPS gain. Auto frame generation approached 60 displayed FPS on a 60 Hz screen but did not remove every hitch. The game has now been updated to v2.2.0-rc.1; its gameplay FPS has not yet been measured. See [docs/CURRENT.md](docs/CURRENT.md) for exact status and limits.
