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

1. **First run in session only** — skip this step if you have already run `verify-ui` earlier in this conversation:
   - Call the XcodeBuildMCP `list_sims` tool and confirm at least one iOS 18+ simulator is available. If none are found, stop and tell the user to install an iOS 18+ simulator in Xcode before continuing.

2. Call the XcodeBuildMCP `session_show_defaults` tool to confirm project, scheme, and simulator are set. If any are missing, stop and ask the user to configure them.

3. Call the XcodeBuildMCP `build_run_sim` tool to build and launch the app on the simulator.

4. Call the XcodeBuildMCP `screenshot` tool to capture the current simulator screen.

5. Evaluate the screenshot against the UI changes identified above. Report the result:
   - **Pass**: The changes look correct — display the screenshot and briefly describe what was verified.
   - **Fail (build/launch)**: Build or launch failed — show the error output and stop.
   - **Fail (visual)**: The app launched but the expected changes are not visible or look wrong — display the screenshot and describe specifically what appears incorrect.
