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
2. **Otherwise, check for newly added tests**:
   - Run `git diff HEAD -- '**/*Tests*.swift'` and scan added lines (`+`) for new test function signatures matching `@Test func \w+` or `func test\w+`.
   - Run `git status --short` and check for any untracked `*Tests*.swift` files not yet in the diff — read those files directly to find test function signatures.
   - Look back at the current conversation for any tests that were just written.
   - If new test functions are found from any of the above sources:
     - Identify each function's enclosing class or struct name.
     - Infer the target name from the file path (e.g. a file under `FooTests/` belongs to target `FooTests`).
     - Build `-only-testing` entries in the format `TargetName/ClassName/methodName` and pass them as `extraArgs` to `test_sim`. Example: `["-only-testing", "TestSwiftUIAppTests/TestSwiftUIAppTests/amPmColor_returnsBlueInMorning"]`.
3. **If no new tests are found**, use the `AskUserQuestion` tool to ask: "No new tests detected — run the full test suite?" and wait for confirmation before proceeding. If they decline, stop.

## Steps

All tools below are using the `XcodeBuildMCP` tool.

1. Follow [.claude/skills/shared/xcodebuildmcp-session-setup.md](.claude/skills/shared/xcodebuildmcp-session-setup.md) to ensure session defaults are configured.

2. Call `session_show_defaults` to confirm project, scheme, and simulator are all set. If any are still missing, stop and ask the user to configure them.

3. Call `test_sim` to build and run the tests, using any filter determined above.

4. Report the result:
   - **Pass**: All tests passed — report the total number of tests run, note if a filter was applied, and confirm everything passed.
   - **Fail (build)**: Build failed before tests ran — show the error output and stop.
   - **Fail (test failures)**: One or more tests failed — list each failing test by name with its failure message, and report the overall count (e.g. "3 of 47 tests failed").
