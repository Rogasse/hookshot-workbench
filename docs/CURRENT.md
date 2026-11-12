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
- A clean v2.1.0 (`source 633eb435`) renderer DLL compiled successfully from source on Windows using `RX_VK_ONLY=1`, `RX_RELEASE=1`, llvm-mingw, and the Builder's pinned headers: 208 files, 0 failures. It has not been installed or run in the game. Its build output stays local outside this repository.
- Next: inspect the whole #2585 discussion and check for a paused test or overlapping fix; create a patched DLL from the same source; design repeated, same-scene A-B-A-B runs with original DLL backup and identical settings. No FPS claim or PR review until that evidence exists.
