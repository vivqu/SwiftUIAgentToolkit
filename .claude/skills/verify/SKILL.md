---
name: verify
description: Full verification — runs verify-ui and verify-test in sequence and reports a combined summary. Use when asked to verify everything, do a full verification, or make sure everything works.
disable-model-invocation: true
argument-hint: [optional: what UI changes to verify, e.g. "login button color changed to red"]
---

# Verify (Full)

Run full verification by invoking both sub-skills in sequence, then report a combined summary.

## Steps

1. Invoke the `verify-ui` skill (passing `$ARGUMENTS` if provided). Note the result — do not stop if it fails, continue to step 2.

2. Invoke the `verify-test` skill. Note the result.

3. Report a combined summary:
   - Show the UI result (pass or fail with details) and the test result (pass or fail with details).
   - End with a single-line overall verdict: **All checks passed** or **Verification failed** (listing what failed).
