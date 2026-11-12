# Worklog

Append a dated entry after a meaningful result. Keep each entry factual and link the public record. Do not paste private local paths or raw game data.

## 2026-11-12 — Setup and 6 GB baseline

- Created the public [Rogasse/hookshot-workbench](https://github.com/Rogasse/hookshot-workbench) repository for durable Windows-specific Hookshot context. Its first commit contains only documentation and a `.gitignore` for game/build artifacts. A local workspace `AGENTS.md` points Hookshot sessions to this repository.
- Read upstream `AGENTS.md`, `CONTRIBUTING.md`, `docs/workflow.md`, and the ranked worklist. Read mooki000's public workbench README and measurement/evidence guides for method, adapting for Windows.
- Verified the intended GitHub account `Rogasse`; deleted the accidentally posted `MecaprojectRD` issue comment and [reposted the baseline as Rogasse](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011).
- Signed into the Hookshot team chat through Discord; `whoami` returned `@rogasse:magicbean.dev`. No team message or automatic update was sent.
- Existing v2.1.0 log review: 122/729 VRAM samples above the driver allowance, peak 5,976/4,920 MB; a separate slow gameplay interval had 17-26 ms/frame memory sync. The latest driver is 621.14, while those logs were from 616.92.
- Read [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585): it changes the exact `room_in_blocks` condition present in v2.1.0. A clean v2.1.0 renderer-only build (`RX_VK_ONLY=1`, `RX_RELEASE=1`) completed: 208 compiled, 0 failed, 10 MB DLL. The DLL has not been game-tested; no speed result yet.
