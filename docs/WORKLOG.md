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

## 2026-11-12 — PR #2834 source validation

- Pinned [PR #2834](https://github.com/NotRexed/Hookshot/pull/2834) at `14b92e2`. Its current code changes the Auto and Low preset mirror allowance for 6 GB cards to 1536 MB and limits a preset's choice to the card's Auto allowance. Its previous description of a separate image-pool change is outdated: [#2711](https://github.com/NotRexed/Hookshot/pull/2711) is already merged, and this PR's current diff contains only mirror-budget code, menu values, tests, and docs.
- Ran `python -I -B tests/test_mirror_budget.py --cxx <llvm-mingw g++>` and `python -I -B tests/test_vram_budget_row.py --cxx <llvm-mingw g++>` on a source snapshot. Both passed. Blob hashes of the files exercised by these tests match the current PR head, which moved during the check.
- Attempted `python -I -B tests/run_all.py --jobs 4 --timeout 180`. Result: 216 passed, 129 failed, 178 skipped. The environment lacks a .NET SDK, several named compilers and Vulkan headers; many compiled fixtures failed to launch because their runtime DLLs were not on the process path. This is an environment-limited run, not a source-suite pass or a regression finding.
- C: had 17.2 GiB free and no second drive was connected. Upstream documents roughly 60 GB free for a full build. The installed v2.1.0 game has renderer API 14 and cannot load this branch's current renderer. No in-game FPS comparison, test-request claim, or upstream post was made.

## 2026-11-12 — v2.2.0-rc.1 update completed

- The Hookshot Builder updated the installed game from v2.1.0 to [v2.2.0-rc.1](https://github.com/NotRexed/Hookshot/releases/tag/v2.2.0-rc.1). The installed version marker, new executable and Vulkan renderer, and freshly prepared pipeline cache were observed. The build and cache preparation processes ended and their temporary preparation markers disappeared.
- C: had 19.05 GiB free after preparation. No game files, caches, or user data were deleted during monitoring.
- Release notes include earlier shader creation, more precompiled pipelines, VRAM and texture-memory fixes, and richer frame-time diagnostics. [#2711](https://github.com/NotRexed/Hookshot/pull/2711), [#2825](https://github.com/NotRexed/Hookshot/pull/2825), and [#2826](https://github.com/NotRexed/Hookshot/pull/2826) are included. [#2850](https://github.com/NotRexed/Hookshot/pull/2850) merged after the RC tag; [#2834](https://github.com/NotRexed/Hookshot/pull/2834) remained open when checked. Neither is part of this RC.
- No gameplay or FPS measurement has yet been run on v2.2.0-rc.1, so the expected reduction in Kokiri stutters on this 6 GB RTX 4050 is unverified. No upstream post was made.

## 2026-11-12 — Exploratory Market play on the RC

- Observed several player-driven Hyrule Castle Town/Market runs on installed v2.2.0-rc.1. The player changed graphics settings and restarted between runs. Local game logs and two local short videos were inspected; none was uploaded. The camera path and cache state differed, so these are descriptive measurements, not a controlled A-B-A-B or v2.1.0 comparison.
- One built-in frame-generation video displayed 62-68 FPS with only 15-18 base game FPS. Its log had a 16.9 FPS median over 19 five-second gameplay windows and a 2044.5 ms worst reported frame. The visual softness during movement is consistent with such a low base rate; a distant street haze persisted with generation turned off.
- Minimum preset, frame generation off, 1920x1080 output, 50% render resolution: 23.1 FPS median across 21 five-second gameplay windows, 338.6 ms worst frame. At 1280x720 output, the same preset had a 30.0 FPS median across 15 gameplay windows and 33.1 FPS median after the first 30 seconds, but a 2188.4 ms entry hitch. Different routes prevent a precise FPS gain claim from the output change.
- Low (6 GB), frame generation off, 1920x1080 output, 75% render resolution: only seven gameplay windows before the next restart (13.7 FPS median, 1288.2 ms worst frame), too short for steady state. A later Low/75% 1280x720 run had 28.9 FPS median over 30 gameplay windows and 30.1 FPS median over the 24 windows after its first 30 seconds, but dipped to 14.4 FPS and reported a 953.1 ms worst frame. Different route and load state prevent a precise setting comparison.
- Several gameplay VRAM readings were at or above the driver's allowance. Windows reported about 1.5-1.8 GiB physical RAM free while other apps remained open at the player's request. This is a possible contributor to stutter, not an isolated cause. The next useful test is a repeated fixed Market scene with one settings change at a time and frame generation off. No upstream post was made.

## 2026-11-12 — RC Market observation posted on the newer issue

- Searched recent Hookshot issues and discussions for the Castle Town slowdown. [Issue #2780](https://github.com/NotRexed/Hookshot/issues/2780) was opened the same day for FPS drops after area transitions; it is more current and specific than the older aggregate trackers. Its existing comments distinguish a direct Market load from entering through Hyrule Field and discuss merged #2825/#2826.
- [Posted one observational comment as Rogasse](https://github.com/NotRexed/Hookshot/issues/2780#issuecomment-6838575114): on v2.2.0-rc.1, the RTX 4050 Laptop 6 GB had 23.1 median base FPS over 21 five-second Market windows at 1080p/Minimum/50% with frame generation off, a 338.6 ms worst reported frame, and one 5,004/4,961 MB VRAM sample. The comment identifies background RAM pressure and states clearly that the Field → Market transition and a controlled v2.1.0 comparison were not tested. No game files, raw logs, saves or options were uploaded.
- The next relevant contribution to #2780 is a fixed-view pair: direct Market load versus entering from Hyrule Field on the same RC build and settings. No PR-specific improvement or failure was claimed.

## 2026-11-13 — Castle Town input capture and PR #2557 preparation

- Preserved the player's 2026-11-12 23:15 Castle Town save in a separate local backup. Captured the Oubang/PS4-mapped controller while the player loaded that exact save, waited at the spawn, and walked through Castle Town. The private recording contains 5,369 samples over 111.5 seconds, including about 46 seconds of movement. Neither the save nor the raw capture is in this repository.
- A first pilot using the game's timed button script reached another part of Castle Town, but its full-stick directions could not preserve the controller's analog deflection. The installed v2.2.0-rc.1 game also has the opt-in local control bridge, which accepted analog axes and loaded isolated copies of the save.
- Two analog movement-only replays with real-time game speed reached different endpoints; their FPS values cannot be compared as a controlled run. With per-frame game speed and frame generation off, two further runs both reached the fountain area, though their final camera angle still differed. The second per-frame run's 12 gameplay log windows had a 20.0 FPS median (15.5–25.8 FPS); downloads were active in the background. This is an exploratory release baseline, not a result for PR #2557.
- Pinned [PR #2557](https://github.com/NotRexed/Hookshot/pull/2557) at `3aae87ea`. Its focused texture-detail test passed 33 configurations after the bundled compiler runtime was placed on PATH. A full branch game build was started. The PR remains a draft; at this stage no upstream test request or comment had been posted.

## 2026-11-13 — PR #2557 Auto versus Medium on RTX 4050 Laptop 6 GB

- Built the pinned PR head `3aae87ea` as a separate game; the executable SHA-256 is `19168873f68d6d75cad4d643c5bb979c9a8ce2e5f3b1b3d9dee3e914e6cb5679`. The installed v2.2.0-rc.1 game and original save were left intact. The 33-case focused source test passed. PC: Windows 11 Home, i5-13420H, 31.6 GiB RAM, RTX 4050 Laptop 6 GB, driver 621.14.
- Four clean branch launches alternated Auto (`texture_detail=0`) and Medium (`=2`), each verified through the local control bridge. All used a private copy of the same Castle Town save, 1920x1080 output, 75% render resolution, upscaler Off, Handheld Profile on, frame generation forced off, per-frame game speed, and other options held. The tested quality preset was Custom (`quality_preset=0`). Background downloads and other desktop apps remained active at the player's request.
- Fixed view after a 240-frame settle, then 1,800 native frames standing: medians of the game's five-second FPS windows were Auto **34.3, 33.9** and Medium **34.7, 35.3**. Presented intervals over 40 ms: Auto **24, 25**, Medium **8, 12**. Texture-memory medians: Auto **2,132, 2,245 MB**; Medium **2,121, 2,103 MB**. Medium also had lower texture memory at the matching starting view, but the size of the difference varied. This small static-scene FPS difference is exploratory, not proof of a general performance gain.
- Replayed the last captured 46-second movement segment with analog axes sampled at 100 ms per 3 game frames, no interaction buttons. Four A-B-A-B route medians were Auto **21.0, 21.15** and Medium **20.2, 20.25** FPS. NPC collisions caused differing camera paths and endpoints. These moving numbers and their texture totals cannot isolate the setting's effect. No raw saves, logs, images, controller data, or game files were uploaded.
- [Posted the factual result on PR #2557 as Rogasse](https://github.com/NotRexed/Hookshot/pull/2557#issuecomment-6844684249), including all four fixed-view runs, the diverged movement trace, settings, and background-load limitation.

## 2026-11-13 — Review of published Hookshot reports

- Checked Rogasse's four comment threads and searched for authored issues and PRs; none were authored by Rogasse. [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585) merged on 2026-11-12, and [its reviewer explicitly credited the RTX 4050 test](https://github.com/NotRexed/Hookshot/pull/2585#pullrequestreview-5878654906) while preserving its limits. The author incorporated the numbers into the PR description.
- [PR #2557](https://github.com/NotRexed/Hookshot/pull/2557) merged on 2026-11-13. A [later maintainer comment](https://github.com/NotRexed/Hookshot/pull/2557#issuecomment-6847209607) tested a batch of 21 PRs on an RTX 4060 Ti: 58 versus 57 FPS within run spread, no one-frame flashes or crash. This did not isolate #2557 or demonstrate an FPS gain. Another 6 GB tester found less texture memory but no FPS beyond run noise. Combined with Rogasse's fixed-view and divergent moving runs, Texture detail Medium is a memory-control option, not a proven remedy for low FPS.
- [Issue #993](https://github.com/NotRexed/Hookshot/issues/993) and [issue #2780](https://github.com/NotRexed/Hookshot/issues/2780) remain open. Later comments concern other machines and mechanisms; none directly addressed Rogasse's measurements. A separate #2826 regression reported on a 10 GB card led to merged [PR #3020](https://github.com/NotRexed/Hookshot/pull/3020), which was not tested on this PC.

## 2026-11-13 — Longshot continuation announced

- Received the team's notice pointing contributors to [Longshot](https://git.magicbean.dev/MagicBeanDev/Longshot) and [its Discord](https://discord.gg/KX99srmQTe). Verified the public Forgejo repository and README: it calls Longshot a continuation of Hookshot and says the top maintainers moved. Hookshot's GitHub repository was still unarchived with recent commits; the notice speaks for the moving team, not necessarily every contributor there.
- Read [Longshot's contribution guide](https://git.magicbean.dev/MagicBeanDev/Longshot/src/branch/main/CONTRIBUTING.md), [agent instructions](https://git.magicbean.dev/MagicBeanDev/Longshot/src/branch/main/AGENTS.md), and [workflow](https://git.magicbean.dev/MagicBeanDev/Longshot/src/branch/main/docs/workflow.md). New contributions go through Forgejo and a claimed task in Discord `#dev-work`; performance changes need repeated matched runs and the local full test suite. The existing Hookshot test data remains valid historical evidence, but its PR numbers must be linked by full GitHub URL in Longshot discussions.
- Confirmed [Longshot v3.0.0-rc.2](https://git.magicbean.dev/MagicBeanDev/Longshot/releases/tag/v3.0.0-rc.2) and [Launcher v1.0.0-rc.2](https://git.magicbean.dev/MagicBeanDev/LongshotLauncher/releases/tag/v1.0.0-rc.2). The [save guide](https://git.magicbean.dev/MagicBeanDev/Longshot/src/branch/main/docs/saves.md) documents Hookshot import with destination backup and no change to the Hookshot source. No Longshot account sign-in, checkout, build, save migration or public post was performed.

## 2026-11-13 — Claimed a Longshot 6 GB retest

- Cloned Longshot and reread its current agent, contribution, workflow and team-chat guidance. Verified the team-chat identity as `@rogasse:magicbean.dev` and Forgejo as `Rogasse` after the player's Discord sign-in.
- Read the latest agent updates and approved test-request queue. Another tester is investigating growth over play on a 10 GB RTX 3080; no claimable request matched this Windows RTX 4050 Laptop 6 GB and display. Posted one complementary claim in `#agent-updates:magicbean.dev` for the worklist score 5.6 memory-growth/FPS-fade retest on a real 6 GB card. The message links the prior [Hookshot observation](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011) and proposes repeated Castle Town / Hyrule Field measurements of base FPS, long frames, RAM and VRAM.
- No Longshot build, gameplay measurement, code fix, PR, or test-request claim has been made yet. The posted claim does not establish a memory leak or FPS change.

## 2026-11-13 — Installed Longshot and corrected project status

- The official Longshot Launcher v1.0.0-rc.2 built Longshot v3.0.0-rc.2 on this Windows PC, with shader preparation complete. A short first start logged the release version and no error-like lines; this is a start-up check, not a gameplay or performance test.
- Imported six normal save slots using Longshot's save script and verified their files against Hookshot by SHA-256. Preserved 15 separate testing profiles and an untouched archive of all 16 save sets locally. No save, game file or cache was published.
- Rogasse supplied later Discord announcements stating that NotRexed intends to continue Hookshot and that Longshot is not an official Rexed port. The old GitHub repository returned HTTP 404 when checked later that day. Treat the projects separately; do not infer that Hookshot development has ended. Rogasse chose to retain Hookshot.

## 2026-11-13 — Updated Longshot in place to rc.3

- Verified the official rc.3 builder ZIP against its release SHA-256 and used `LongshotBuilder.exe --cli --update` on the existing game folder. The build and shader preparation completed with exit code 0. A short start logged `v3.0.0-rc.3` and no error-like lines; this does not test gameplay or FPS.
- Verified all 14 files in the six normal save slots against the untouched local archive by SHA-256 after the update. The 15 separate testing profiles remain preserved. The launcher's build record was corrected to show rc.3 in the original folder. Hookshot remains installed by Rogasse's choice.

## 2026-11-13 — Chose the next 6 GB test

- Checked the current Longshot releases, worklist, test requests, team updates, and open performance issues. rc.3 remains the latest release candidate. The high-priority memory-growth/FPS-fade row (score 5.6) is still open; another tester has a distinct 10 GB Windows run. [Issue 89](https://git.magicbean.dev/MagicBeanDev/Longshot/issues/89) explicitly asks for a matched direct-load versus post-area route, so the next local test is a short Market direct-load versus Hyrule Field → Market comparison before a longer memory tour.
- Confirmed the installed rc.3 log reports no DLSS in this build. Keep the first route test on the game's own upscaler and describe that limit; a DLSS-toggle test needs a restored SDK-enabled build. No new gameplay measurement or upstream post was made during this review.

## 2026-11-13 — Stopped the first Longshot field pilot at the Windows commit limit

- Launched one rc.3 game instance with an isolated, verified copy of the normal saves and sampled its private memory and system-wide GPU memory at five-second intervals. Rogasse began moving in Hyrule Field toward Castle Town. This was a pilot, not a controlled A/B run; it ended before the city transition.
- In 15 samples over about 72 seconds, process private memory rose from 16.6 to 22.1 GB. Windows reached 53.64/54.39 GB committed (98.6%) with roughly 1.8 GB of physical memory available. The game log independently reported that the commit limit was near and reduced its texture budget. One late game log window reported 15.8 FPS; it is not a route average.
- Closed only the test game through its window to avoid a system freeze. Windows committed memory then fell to 21.5 GB and physical memory available rose to about 18.5 GB. The isolated save profile and local samples remain on the PC; no game data was published. One short run cannot establish a leak, an FPS fade, or the effect of entering Castle Town. Check memory headroom before resuming the matched route test.
