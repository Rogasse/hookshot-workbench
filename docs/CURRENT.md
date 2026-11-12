# Current state

Updated: 2026-11-12 (America/Santo_Domingo).

## Accounts and project

- Upstream: [NotRexed/Hookshot](https://github.com/NotRexed/Hookshot).
- This public context repository: [Rogasse/hookshot-workbench](https://github.com/Rogasse/hookshot-workbench), `main`.
- GitHub publication identity: `Rogasse` (verified with `gh api user --jq .login` on 2026-11-12). Recheck before every write.
- Hookshot team chat identity: `@rogasse:magicbean.dev` (verified with `python -I scripts/team_chat.py whoami`). No automatic updates enabled.
- Public performance report, posted as Rogasse: [issue #993 comment](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011). An earlier comment from the wrong account was deleted.

## Machine and installed game

- Windows 11 Home, build 26200; Intel Core i5-13420H; 32 GB RAM; NVIDIA GeForce RTX 4050 Laptop GPU, 6 GB VRAM.
- Current NVIDIA driver observed on 2026-11-12: 621.14. The existing play logs were produced with driver 616.92.
- Installed Hookshot: v2.2.0-rc.1, [release tag](https://github.com/NotRexed/Hookshot/releases/tag/v2.2.0-rc.1). The update and its pipeline/cache preparation completed on 2026-11-12. Exploratory gameplay measurements on this version are below. Earlier controlled comparisons used v2.1.0, source `633eb435`.
- C: had 19.05 GiB free after the update completed on 2026-11-12, below the roughly 60 GB that Hookshot documents for a full source build. Only the Vulkan renderer has been built in the separate v2.1.0 source checkout.

## Evidence and limits

- User reports stutters and around 20 FPS in Kokiri Forest; completed the Great Deku Tree.
- One v2.1.0 session had 122 of 729 VRAM samples above the driver's allowance; peak excess: 5,976 MB used / 4,920 MB allowed. At that sample textures were 3,115 MB / 2,249 MB budget. There were 6,841 `textures retired` log entries.
- Another gameplay log has slow samples around 16-23 FPS, with 17-26 ms/frame in renderer `memory sync` and about 36-40 ms/frame of GPU time. The log does not tie every sample to an exact Kokiri camera position.
- These observations do not establish one cause or measure a fix. Raw logs remain local.

## Work in progress

- Candidate [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585): squeeze textures again once VRAM use exceeds the driver's allowance, even if VMA has room inside existing blocks. The existing v2.1.0 source contains the same condition that the PR changes.
- A clean v2.1.0 (`source 633eb435`) renderer DLL compiled successfully from source on Windows using `RX_VK_ONLY=1`, `RX_RELEASE=1`, llvm-mingw, and the Builder's pinned headers: 208 files, 0 failures. SHA-256 `8099463214BA51A7E6DD8FAADEAEF87BC532FA066230218E6943FC6B4FBBFA42`.
- The one-line PR #2585 change was backported to the same v2.1.0 source and compiled successfully. SHA-256 `1B967975201ED4E2E69B6DCFC1F6D45A63E0C028EECC5172F32A165`. Both local renderer variants were tested in game on the same scripted Kokiri route; the installed renderer was restored after testing.
- Under the normal driver allowance, one baseline/patch pair averaged 28.58/28.79 FPS during movement. Neither arm reached the allowance, so this pair did not exercise the changed condition. With an artificially lowered 4,300 MB renderer allowance, the pair averaged 27.46/27.38 FPS during movement. The patch reduced over-allowance samples but did not demonstrate an FPS gain. The artificial limit is not the real Windows VRAM budget, and one pair per condition is insufficient for a performance claim. [Results were posted as Rogasse on PR #2585](https://github.com/NotRexed/Hookshot/pull/2585#issuecomment-6828095123).
- PR #2585 was open when checked on 2026-11-12. Comments on the PR report that the change removes a `not squeezed` log condition but does not clearly improve VRAM usage or FPS in the tested configurations. A related image-pool fix in [PR #2711](https://github.com/NotRexed/Hookshot/pull/2711) may matter more. These are other contributors' results, not tests on this machine.
- [PR #2711](https://github.com/NotRexed/Hookshot/pull/2711), [#2825](https://github.com/NotRexed/Hookshot/pull/2825), and [#2826](https://github.com/NotRexed/Hookshot/pull/2826) merged after v2.1.0 and are included in v2.2.0-rc.1. Their effect on this PC remains unmeasured. [PR #2814](https://github.com/NotRexed/Hookshot/pull/2814) targets AMD Windows pipeline behavior; it was not tested on this NVIDIA machine.

## Graphics setting checks (2026-11-12)

- The connected external display reported by Windows was a Dell P2419H at 1920x1080, 60 Hz. The Acer 120 Hz display was not detected during these tests.
- With the installed v2.1.0 build and driver 621.14, a short scripted Kokiri route at the original Handheld/50% settings averaged about 30 game FPS. Changing to DLSS Performance or Ultra Performance in that short route did not show an FPS gain. The longer route varied in position between runs, so its apparent differences between settings are not a valid same-scene comparison.
- At the original settings, frame generation Auto targeting the 60 Hz display showed 58.71 and 56.83 FPS over two 24-second movement runs in a window; fullscreen showed 56.67 FPS in one run. Their respective counts of displayed frames over 50 ms were 0, 6, and 4. Auto was more useful for displayed smoothness than fixed 2x in these runs (47.08 FPS moving); fixed 3x averaged 72.25 displayed FPS but still had long frames and a low 1% rate. Frame generation does not raise the game's own simulation rate or remove all hitches.
- One Auto/67% run collapsed to 27.58 displayed FPS moving; a repeat gave 56.92. That spread prevents a reliable claim about 67% or thermal behavior. A single active-game GPU reading was about 76 C at 2460 MHz, which does not establish sustained thermal throttling. No save-slot file changed during these tests.
- Current player setting after testing: frame generation Auto and fullscreen, retaining the game's own upscaler, Handheld profile, 50% render resolution, frame pacing, and 60 game-FPS cap. The previous options were backed up locally; no raw options or game artifacts are in this repository. This aims for smoother display on the current 60 Hz screen, not a guaranteed constant 60 FPS.
- [PR #2850](https://github.com/NotRexed/Hookshot/pull/2850) is a hardware-aware Auto preset, merged after the v2.2.0-rc.1 tag. The real RTX 4050 Laptop 6 GB on Windows matches a requested test group, but the PR lacked the required `testing wanted` label when checked. It is not in the installed RC and was not tested here.

## v2.2.0-rc.1 exploratory Market gameplay (2026-11-12)

- The player entered Hyrule Castle Town/Market and made several short recordings while changing settings and restarting. These were not the same camera route or a planned A-B-A-B comparison. The game logs and recordings stay local; none was uploaded. The display was 1920x1080 for the first runs.
- With built-in frame generation on, one video showed 62-68 displayed FPS but only 15-18 base game FPS. The corresponding gameplay log had a median 16.9 game FPS across 19 five-second windows and a reported 2044.5 ms worst frame. This does not demonstrate a smooth 60 FPS experience.
- With frame generation off, Minimum preset, 1920x1080 output and 50% render resolution, a later run had median 23.1 game FPS across 21 five-second gameplay windows, with a 338.6 ms worst reported frame. A subsequent Minimum/50% run at 1280x720 output had a 30.0 FPS median across 15 windows, 33.1 FPS median in the nine windows after its first 30 seconds, but also a 2188.4 ms worst frame on entry. These runs differed in route, cache and background state; do not attribute the difference solely to output resolution.
- Low (6 GB) preset at 1920x1080 output, 75% render resolution and frame generation off had only seven gameplay windows before another restart: median 13.7 FPS, 1288.2 ms worst reported frame; this is too short to establish steady-state performance. A following Low/75% 1280x720 run was longer: median 28.9 FPS across 30 gameplay windows, 30.1 FPS in the 24 windows after its first 30 seconds, with a 14.4 FPS dip and 953.1 ms worst reported frame. The camera route differed, so these are not controlled setting comparisons.
- The logs repeatedly showed the renderer near its driver VRAM allowance, with some samples above it. Windows reported only about 1.5-1.8 GiB physical RAM free while the game and other apps were running. This is evidence of memory pressure, not proof of one root cause. The visible haze in the distant Market street persisted in a recording with frame generation off; low render resolution and built-in frame generation at 15-18 base FPS can add softness or motion artifacts, but not all distant haze is caused by FPS.
- Next: at 1920x1080 output, keep frame generation off for measurement, compare one fixed scene at Minimum/50% versus Low/75% or a 67% custom step, repeating each arm and preserving options/saves. Prioritize base FPS and long frames over generated FPS. No RC-versus-v2.1.0 same-scene comparison has been completed.
- [Posted a 6 GB RC Market data point on issue #2780](https://github.com/NotRexed/Hookshot/issues/2780#issuecomment-6838575114) as Rogasse. It reports the 1080p Minimum/50%, frame-generation-off run and explicitly says that no matched direct-Market-load versus Hyrule Field → Market transition was captured. It does not claim #2825/#2826 failed or that the transition regression persists. A fixed-view transition pair is the next useful follow-up for that issue.

## Upstream contribution opportunity (checked 2026-11-12)

- The installed release is now v2.2.0-rc.1. The full build requires about 60 GB free per upstream's contribution guide, while the last observed C: free space was 19.05 GiB. Exploratory RC gameplay is documented above; no individual PR or controlled RC-versus-v2.1.0 result was measured. Do not attribute the Market FPS to one PR.
- [PR #2834](https://github.com/NotRexed/Hookshot/pull/2834) is open and targets real 6 GB cards. Its 2026-11-12 head `14b92e2` raises the Auto and Low preset mirror allowance to 1536 MB on 6 GB cards, while capping presets on smaller cards. The two focused game-free tests passed locally against the same source blobs; this verifies the rule, not gameplay performance. A broad source-suite attempt had 216 passes, 129 failures, and 178 skips, primarily because this Windows environment lacks required compilers/runtime DLLs and a .NET SDK; it cannot serve as a clean source-suite result. No in-game #2834 A/B has been run on this RTX 4050. The author measured an RTX 3060 Laptop 6 GB on Windows; this machine would add a different real card after a compatible full build. [PR #2794](https://github.com/NotRexed/Hookshot/pull/2794) is open and opt-in; its 6 GB result comes from a 12 GB card with an artificial allowance.
- The prior long Kokiri walk diverged between launches. For a future A-B-A-B comparison, isolate the save, use a repeatable scene or fixed camera, consider `HOS_REALTIME_STEP=0` as in #2834's method, keep frame generation off while measuring real game FPS, and report raw per-run spread and long frames. No upstream PR test request has been claimed or posted from this PC.
