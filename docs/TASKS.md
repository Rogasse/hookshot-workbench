# Tasks

| Status | Task | Evidence / next action |
|---|---|
| In progress | Test the VRAM squeeze condition on the 6 GB RTX 4050 | [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585). Both v2.1.0 renderer variants compiled locally; same-scene game runs pending. Other contributors' tests have not shown a clear FPS gain, so report this machine's measurements without assuming one. |
| Waiting for compatible build | Test image-pool preallocation on the real 6 GB RTX 4050 | [PR #2711](https://github.com/NotRexed/Hookshot/pull/2711). The v2.1.0 installed source does not expose `RX_VK_IMAGE_PREALLOC`, and the current-main renderer API does not match the installed game. Mooki000 is taking over the PR's integration/testing; a real 6 GB NVIDIA Windows result would add distinct hardware evidence when a compatible game build is available. |
| Waiting for compatible build | Test sparse VRAM mirrors on a real 6 GB card | [PR #2794](https://github.com/NotRexed/Hookshot/pull/2794). Needs a current-main game build; API 19 cannot pair with installed v2.1.0/API 14 game. |
| Track upstream | Retest memory and VRAM after the next release | [Issue #993](https://github.com/NotRexed/Hookshot/issues/993), [PR #2759](https://github.com/NotRexed/Hookshot/pull/2759), [PR #2557](https://github.com/NotRexed/Hookshot/pull/2557). Compare the same scene and settings; record driver and build. |
| Done | Publish the existing v2.1.0 baseline from the intended account | [Rogasse's report](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011). |

Check every PR's latest head, description, reviews, and comments before investing in a test; maintainers may have changed the intended test or paused it.
