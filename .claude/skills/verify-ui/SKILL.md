---
name: verify-ui
description: Build and run the app on a simulator, take a screenshot, and verify UI changes look correct. Use when asked to verify the UI, check the app looks right, check if the app launches, or take a screenshot of the running app.
disable-model-invocation: true
argument-hint: [what to verify, e.g. "login button color changed to red"]
---

# Verify UI

Build and run the app on a simulator, take a screenshot, and verify the UI looks correct for the current work.

## Determine what to verify

Before running anything, establish what UI changes should be validated, in priority order:

1. **If `$ARGUMENTS` was provided**, use that as the description of what to verify.
2. **Otherwise, scan for recent UI changes**:
   - Run `git diff HEAD -- '**/*.swift'` and scan changed lines for modifications to View or layout code (SwiftUI views, modifiers, colors, text, navigation, etc.).
   - Run `git status --short` and check for any untracked `.swift` files that may not yet appear in the diff.
   - Look back at the current conversation for any UI changes that were just made.
3. **If no changes are found**, just verify the app launches and renders without errors.

## Steps

All tools below are using the `XcodeBuildMCP` tool.

1. Follow [.claude/skills/shared/xcodebuildmcp-session-setup.md](.claude/skills/shared/xcodebuildmcp-session-setup.md) to ensure session defaults are configured.

2. Call `session_show_defaults` to confirm project, scheme, and simulator are all set. If any are still missing, stop and ask the user to configure them.

3. Call `build_run_sim` to build and launch the app on the simulator.

4. Call `screenshot` to capture the current simulator screen.

5. Evaluate the screenshot against the UI changes identified above. Use [docs/UI_CONVENTIONS.md](docs/UI_CONVENTIONS.md) as a reference for what correct UI looks like (layout, accessibility, visual distinction). Report the result:
   - **Pass**: The changes look correct — display the screenshot and briefly describe what was verified.
   - **Fail (build/launch)**: Build or launch failed — show the error output and stop.
   - **Fail (visual or conventions)**: The app launched but the expected changes are not visible, look wrong, or violate UI conventions (e.g. unsafe layout, missing accessibility identifiers, insufficient contrast) — display the screenshot and describe specifically what is incorrect or non-compliant.
