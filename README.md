# Rogasse's Hookshot workbench

Public notes and repeatable methods for testing [Hookshot](https://github.com/NotRexed/Hookshot) and its [Longshot continuation](https://git.magicbean.dev/MagicBeanDev/Longshot) from a Windows PC with an RTX 4050 Laptop GPU (6 GB). This repository records what was observed, what remains unproven, and the next useful test. It is independent of both projects.

Inspired by [mooki000/hookshot-workbench](https://github.com/mooki000/hookshot-workbench). Its Linux scripts and machine-specific paths are not copied here. The comparison and evidence principles are adapted to this PC.

## Start here

1. Read [AGENTS.md](AGENTS.md), then [docs/CURRENT.md](docs/CURRENT.md).
2. For new Longshot work, read its current [workflow](https://git.magicbean.dev/MagicBeanDev/Longshot/src/branch/main/docs/workflow.md), [AGENTS.md](https://git.magicbean.dev/MagicBeanDev/Longshot/src/branch/main/AGENTS.md), and [CONTRIBUTING.md](https://git.magicbean.dev/MagicBeanDev/Longshot/src/branch/main/CONTRIBUTING.md). For historical Hookshot work, read Hookshot's own instructions.
3. Check [docs/TASKS.md](docs/TASKS.md) and the linked issues/PRs for overlap.
4. Record completed work in [docs/WORKLOG.md](docs/WORKLOG.md), and update CURRENT and TASKS when their status changes.

On Rogasse's Windows PC, the local Codex workspace has an `AGENTS.md` pointer to this repository, and `skills/hookshot-context` is linked into the local Codex skills folder. Those local links help a new Hookshot session discover this context; the repository remains the canonical copy.

## Boundaries

This repository contains no game files, saves, keys, binaries, generated code, shader caches, logs, options file, credentials, or private local paths. Keep run artifacts on the PC. Publish only summaries and evidence allowed by the destination project's rules. Verify that `gh api user --jq .login` returns `Rogasse` before any GitHub write.

## Current focus

The v2.1.0 play logs show Kokiri Forest stutter near 20-30 real game FPS, heavy memory synchronization, and VRAM sometimes above the driver's allowance. The [report on #993](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011) is observational; it does not prove a fix. A local test of [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585) did not demonstrate an FPS gain. The installed v2.2.0-rc.1 was also observed during exploratory Market play: substantial base-FPS drops and entry hitches remain under several changed settings. A separate [PR #2557 texture-detail test](https://github.com/NotRexed/Hookshot/pull/2557#issuecomment-6844684249) showed less texture memory at Medium in a fixed view, but no established gameplay FPS gain. These routes do not establish a controlled release comparison. See [docs/CURRENT.md](docs/CURRENT.md) for numbers and limits.
