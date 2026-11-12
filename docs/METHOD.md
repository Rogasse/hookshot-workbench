# Windows performance comparison

Adapted from [mooki000's performance comparison guide](https://github.com/mooki000/hookshot-workbench/blob/main/skills/hookshot-perf-compare/SKILL.md) for Rogasse's Windows PC. The external scripts are Linux-specific. Hookshot's own current contribution instructions control upstream submissions.

1. Identify one specific question and pin the two source commits, binary SHA-256 hashes, GPU driver, OS, graphics settings, frame cap, output and render resolution, and cache state. Record whether the comparison changes code or only a setting.
2. Use the same save and exact camera/route in the same scene. Use a copied test folder and keep the user's installed game and save intact. Start one game at a time. Warm each variant once without measuring.
3. Run A-B-A-B in that order while other CPU/GPU work is quiet. Capture per-run duration, presents, average and 1% low FPS, median/p99 frame time, frames over 20/25/33 ms, peak VRAM, texture budget, texture retirements, replay `memory sync`, GPU time, and device-lost or fatal lines. Note background load and reject disturbed runs with a reason.
4. Compare the repeat range within A and within B. If the apparent gain falls inside that spread, report it as inconclusive. Do not extrapolate a real 6 GB result to other GPUs or to the current `main` build.
5. For a candidate fix, run its game-free check against both variants and the full source suite. State which platform/hardware paths were not tested. Attach only evidence permitted by upstream; keep raw game/build files local.

Use [RUN_TEMPLATE.md](RUN_TEMPLATE.md) for each run. A diagnostic environment switch on one build is evidence about that switch's behavior, not automatically a test of a different PR.
