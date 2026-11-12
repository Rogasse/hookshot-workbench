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

## 2026-11-12 — Display smoothness and Auto preset review

- Compared graphics settings on the installed v2.1.0 build, RTX 4050 Laptop 6 GB, driver 621.14, with other desktop apps left open at the player's request. Windows reported a connected Dell 1920x1080 60 Hz external display; the Acer 120 Hz display was absent. The player prioritized smoothness and few FPS drops over maximum sharpness.
- A short Kokiri movement script at the original Handheld/50% settings ran near 30 real game FPS. DLSS Performance and Ultra Performance did not materially raise this in the short runs. A longer scripted walk crossed different positions on repeat despite the same unchanged save, so its setting-to-setting FPS comparisons were rejected; the save-slot files were not modified.
- Frame generation Auto, aimed at 60 Hz, showed 58.71 and 56.83 displayed FPS in two windowed 24-second movement runs, with 0 and 6 displayed frames over 50 ms. The tested fullscreen run showed 56.67 displayed FPS and 4 frames over 50 ms. Fixed 2x showed 47.08 FPS and fixed 3x 72.25 FPS, but neither proved hitch-free 60 Hz play. Generated-frame counts must not be reported as real game FPS.
- A 67% render setting with Auto had inconsistent movement results (27.58 then 56.92 displayed FPS), so it was not selected. A single active-game GPU reading of about 76 C and 2460 MHz is insufficient to diagnose thermals.
- Applied Auto frame generation and fullscreen for the current 60 Hz display, preserving the other existing graphics settings and keeping a local backup. This is a reversible player setting, not a source change or upstream performance claim.
- Reviewed [PR #2850](https://github.com/NotRexed/Hookshot/pull/2850). It remains draft and had no `testing wanted` label when checked, so no test request was claimed. Its 6-8 GB Windows test would be useful on this PC after maintainer labeling and a compatible branch build. No upstream comment or team-chat message was posted.

## 2026-11-12 — Rechecked upstream test opportunities

- Read the current upstream workflow, contribution, agent and test-request guides. The newest release remained v2.1.0. Verified that [#2711](https://github.com/NotRexed/Hookshot/pull/2711), [#2825](https://github.com/NotRexed/Hookshot/pull/2825) and [#2826](https://github.com/NotRexed/Hookshot/pull/2826) merged after that release.
- [#2850](https://github.com/NotRexed/Hookshot/pull/2850) is now open and non-draft, but still had no `testing wanted` label when checked. Its latest author comment supersedes part of the description: 1080p is now selectable at any memory tier when the menu offers it. No request was claimed and no branch code was run.
- [#2834](https://github.com/NotRexed/Hookshot/pull/2834) is open with real RTX 3060 Laptop 6 GB Windows measurements; [#2794](https://github.com/NotRexed/Hookshot/pull/2794) is open with a simulated 6 GB allowance on a 12 GB card. A real RTX 4050 Laptop 6 GB comparison could help both, once a compatible build and a repeatable test route are available.
- The installed v2.1.0 game cannot load a current-main renderer DLL, and upstream documents about 60 GB free for a full build. The last observed C: free space was about 16 GB. No upstream comment, request, or PR was posted from this review.
