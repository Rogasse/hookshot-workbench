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
- Installed Hookshot: v2.1.0, source `633eb435`, renderer API 14. The current upstream `main` was API 19 when checked; its DLL cannot simply replace this installed game's DLL.
- C: had about 20 GB free when work began, below the roughly 60 GB that Hookshot documents for a full source build. Only the Vulkan renderer is being built in the separate source checkout.

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
- Next: consider #2711 when a compatible build is available. [PR #2814](https://github.com/NotRexed/Hookshot/pull/2814) targets AMD Windows pipeline behavior; it was not tested on this NVIDIA machine.

## Graphics setting checks (2026-11-12)

- The connected external display reported by Windows was a Dell P2419H at 1920x1080, 60 Hz. The Acer 120 Hz display was not detected during these tests.
- With the installed v2.1.0 build and driver 621.14, a short scripted Kokiri route at the original Handheld/50% settings averaged about 30 game FPS. Changing to DLSS Performance or Ultra Performance in that short route did not show an FPS gain. The longer route varied in position between runs, so its apparent differences between settings are not a valid same-scene comparison.
- At the original settings, frame generation Auto targeting the 60 Hz display showed 58.71 and 56.83 FPS over two 24-second movement runs in a window; fullscreen showed 56.67 FPS in one run. Their respective counts of displayed frames over 50 ms were 0, 6, and 4. Auto was more useful for displayed smoothness than fixed 2x in these runs (47.08 FPS moving); fixed 3x averaged 72.25 displayed FPS but still had long frames and a low 1% rate. Frame generation does not raise the game's own simulation rate or remove all hitches.
- One Auto/67% run collapsed to 27.58 displayed FPS moving; a repeat gave 56.92. That spread prevents a reliable claim about 67% or thermal behavior. A single active-game GPU reading was about 76 C at 2460 MHz, which does not establish sustained thermal throttling. No save-slot file changed during these tests.
- Current player setting after testing: frame generation Auto and fullscreen, retaining the game's own upscaler, Handheld profile, 50% render resolution, frame pacing, and 60 game-FPS cap. The previous options were backed up locally; no raw options or game artifacts are in this repository. This aims for smoother display on the current 60 Hz screen, not a guaranteed constant 60 FPS.
- [PR #2850](https://github.com/NotRexed/Hookshot/pull/2850) is a draft hardware-aware Auto preset. The real RTX 4050 Laptop 6 GB on Windows matches a requested test group, but the PR lacked the required `testing wanted` label when checked. Its branch is changing during review; a later author comment says 1080p is now available at any memory tier when the menu offers it. It is not in the installed v2.1.0 build and was not tested here.
