---
name: verify-test
description: Run the unit and UI test suite on a simulator and report results. Use when asked to run tests, verify tests pass, or run the test suite.
disable-model-invocation: true
argument-hint: [optional test filter, e.g. "LoginTests" to run only matching tests]
---

# Verify Tests

Run the unit and UI test suite on a simulator and report pass/fail results.

## Expected simulator behavior

When running tests you will see multiple app launches — this is normal and expected:

- **UI tests always launch the app as a separate process** from the test runner, so you'll see both start up.
- **`runsForEachTargetApplicationUIConfiguration: true`** (set in the Xcode template's `TestSwiftUIAppUITestsLaunchTests`) causes `testLaunch()` to run once per UI configuration (e.g. light mode and dark mode), which launches the app multiple times.

## Determine what to test

Before running anything, establish the test scope in priority order:

1. **If `$ARGUMENTS` was provided**, use that as a test filter (passed via `extraArgs` as `-only-testing` to `test_sim`).
2. **Otherwise, check for newly added tests** — run `git diff HEAD -- '**/*Tests*.swift'` and scan added lines (`+`) for new test function signatures matching `@Test func \w+` or `func test\w+`. If new test functions are found:
   - Identify each function's enclosing class or struct name from the diff context.
   - Infer the target name from the file path (e.g. a file under `FooTests/` belongs to target `FooTests`).
   - Build `-only-testing` entries in the format `TargetName/ClassName/methodName` and pass them as `extraArgs` to `test_sim`. Example: `["-only-testing", "TestSwiftUIAppTests/TestSwiftUIAppTests/amPmColor_returnsBlueInMorning"]`.
3. **If no new tests are found in the diff**, run the full test suite with no filter.

## Steps

All tools below are using the `XcodeBuildMCP` tool.

1. **First run in session only** — skip if you have already run `verify-test` or `verify-ui` earlier in this conversation:
   - Call `list_sims` and confirm at least one iOS 18+ simulator exists. If none, stop and tell the user to install one in Xcode.
   - From the iOS 18+ results, find any with state **Booted**. If exactly one is booted, call `session_set_defaults` to use it. If multiple are booted, show the list and ask the user to pick one, then call `session_set_defaults`. If none are booted, continue — `test_sim` will boot one.
   - Call `session_show_defaults`. If `projectPath` or `workspacePath` is missing, call `discover_projs` using the workspace root. If exactly one project or workspace is found, call `session_set_defaults` to set it. If multiple are found, show the list and ask the user to pick one. If none are found, stop and tell the user no Xcode project was found.
   - If `scheme` is still missing after setting the project, call `list_schemes` and set the first result via `session_set_defaults`. If multiple schemes exist, show the list and ask the user to pick one.

2. Call `session_show_defaults` to confirm project, scheme, and simulator are all set. If any are still missing, stop and ask the user to configure them.

3. Call `test_sim` to build and run the tests, using any filter determined above.

4. Report the result:
   - **Pass**: All tests passed — report the total number of tests run, note if a filter was applied, and confirm everything passed.
   - **Fail (build)**: Build failed before tests ran — show the error output and stop.
   - **Fail (test failures)**: One or more tests failed — list each failing test by name with its failure message, and report the overall count (e.g. "3 of 47 tests failed").
