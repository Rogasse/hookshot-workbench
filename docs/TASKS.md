# Tasks

| Status | Task | Evidence / next action |
|---|---|
| In progress | Test the VRAM squeeze condition on the 6 GB RTX 4050 | [PR #2585](https://github.com/NotRexed/Hookshot/pull/2585). Baseline renderer DLL compiled; patched variant and same-scene game runs pending. |
| Waiting for compatible build | Test sparse VRAM mirrors on a real 6 GB card | [PR #2794](https://github.com/NotRexed/Hookshot/pull/2794). Needs a current-main game build; API 19 cannot pair with installed v2.1.0/API 14 game. |
| Track upstream | Retest memory and VRAM after the next release | [Issue #993](https://github.com/NotRexed/Hookshot/issues/993), [PR #2759](https://github.com/NotRexed/Hookshot/pull/2759), [PR #2557](https://github.com/NotRexed/Hookshot/pull/2557). Compare the same scene and settings; record driver and build. |
| Done | Publish the existing v2.1.0 baseline from the intended account | [Rogasse's report](https://github.com/NotRexed/Hookshot/issues/993#issuecomment-6826001011). |

Check every PR's latest head, description, reviews, and comments before investing in a test; maintainers may have changed the intended test or paused it.
