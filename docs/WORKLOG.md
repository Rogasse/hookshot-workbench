# Worklog

Append a dated entry after a meaningful result. Keep each entry factual and link the public record. Do not paste private local paths or raw game data.

## 2026-11-12 — Setup and 6 GB baseline

- Created the public [Rogasse/hookshot-workbench](https://github.com/Rogasse/hookshot-workbench) repository for durable Windows-specific Hookshot context. Its first commit contains only documentation and a `.gitignore` for game/build artifacts. A local workspace `AGENTS.md` points Hookshot sessions to this repository.
- Added `skills/hookshot-context/SKILL.md` and linked it into the local Codex skills folder so future Hookshot sessions can find the canonical context. The bundled skill validator could not start because its Python environment lacks PyYAML; the frontmatter and local link were inspected directly.
- Read upstream `AGENTS.md`, `CONTRIBUTING.md`, `docs/workflow.md`, and the ranked worklist. Read mooki000's public workbench README and measurement/evidence guides for method, adapting for Windows.
- Verified the intended GitHub account `Rogasse`; deleted the accidentally posted `MecaprojectRD` issue comment and [reposted the baseline as Rogasse](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011).
- Signed into the Hookshot team chat through Discord; `whoami` returned `@rogasse:magicbean.dev`. No team message or automatic update was sent.
- Existing v2.1.0 log review: 122/729 VRAM samples above the driver allowance, peak 5,976/4,920 MB; a separate slow gameplay interval had 17-26 ms/frame memory sync. The latest driver is 621.14, while those logs were from 616.92.
- Read [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585): it changes the exact `room_in_blocks` condition present in v2.1.0. A clean v2.1.0 renderer-only build (`RX_VK_ONLY=1`, `RX_RELEASE=1`) completed: 208 compiled, 0 failed, 10 MB DLL. The DLL has not been game-tested; no speed result yet.

## 2026-11-12 — Scripted Kokiri renderer comparison

- Backported the single PR #2585 condition to v2.1.0 and built both baseline and changed Vulkan renderer DLLs. Repeated the same timed movement script from the same Kokiri save with identical game options, first under the normal allowance and then under an artificial 4,300 MB renderer allowance.
- Normal-allowance movement averaged 28.58 FPS baseline and 28.79 FPS patch; neither arm reached the VRAM allowance. Under the artificial limit, movement averaged 27.46/27.38 FPS. The patch reduced over-allowance samples in that diagnostic condition, but did not demonstrate an FPS improvement. These are one A/B pair per condition, not a full A-B-A-B study.
- [Published the measured result as Rogasse on PR #2585](https://github.com/NotRexed/Hookshot/pull/2585#issuecomment-6828095123). No game content, raw logs, binaries, or saves were uploaded. The original installed renderer was restored after each run; save slots were not changed by the scripted route.
- Recorded a local video replay of the same route for the player. Recording overhead means its visible FPS counter is illustrative only; the published measurements came from the unrecorded runs.
