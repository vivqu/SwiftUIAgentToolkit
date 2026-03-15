---
name: verify-ui
description: Build and run the app on a simulator, take a screenshot, and verify UI changes look correct. Use when asked to verify the UI, check the app looks right, check if the app launches, or take a screenshot of the running app.
disable-model-invocation: true
argument-hint: [what to verify, e.g. "login button color changed to red"]
---

# Verify UI

Build and run the app on a simulator, take a screenshot, and verify the UI looks correct for the current work.

## Determine what to verify

Before running anything, establish what UI changes should be validated:

- If `$ARGUMENTS` was provided, use that as the description of what to verify.
- Otherwise, look back at the current conversation and identify any UI changes that were just made (layout, colors, text, components, navigation, etc.).
- If neither applies, just verify the app launches and renders without errors.

## Steps

All tools below are using the `XcodeBuildMCP` tool.

1. **First run in session only** — skip if you have already run `verify-ui` earlier in this conversation:
   - Call `list_sims` and confirm at least one iOS 18+ simulator exists. If none, stop and tell the user to install one in Xcode.
   - From the iOS 18+ results, find any with state **Booted**. If exactly one is booted, call `session_set_defaults` to use it. If multiple are booted, show the list and ask the user to pick one, then call `session_set_defaults`. If none are booted, continue — `build_run_sim` will boot one.

2. Call `session_show_defaults` to confirm project, scheme, and simulator are set. If any are missing, stop and ask the user to configure them.

3. Call `build_run_sim` to build and launch the app on the simulator.

4. Call `screenshot` to capture the current simulator screen.

5. Evaluate the screenshot against the UI changes identified above. Use [docs/UI_CONVENTIONS.md](docs/UI_CONVENTIONS.md) as a reference for what correct UI looks like (layout, accessibility, visual distinction). Report the result:
   - **Pass**: The changes look correct — display the screenshot and briefly describe what was verified.
   - **Fail (build/launch)**: Build or launch failed — show the error output and stop.
   - **Fail (visual or conventions)**: The app launched but the expected changes are not visible, look wrong, or violate UI conventions (e.g. unsafe layout, missing accessibility identifiers, insufficient contrast) — display the screenshot and describe specifically what is incorrect or non-compliant.
