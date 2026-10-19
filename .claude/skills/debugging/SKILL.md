---
name: debugging
description: Finds and fixes the root cause of bugs, failing tests, build failures, crashes, regressions, and flaky or unexpected behavior. Use when diagnosing an error message or stack trace, or when code doesn't do what it should.
---

# Debugging

Find the cause before changing code, fix one problem at a time, and prove the fix with a check that failed before and passes after.

Match the effort to the bug. When the error points straight at the cause, reproduce it, fix it, and verify. Work through the investigation section when the cause isn't obvious, when a first fix didn't work, or when the bug is intermittent.

You can run tests, builds, and the app without asking.

## Reproduce

- Find the fastest command that shows the failure and run it. Keep the exact error and stack trace.
- If the project has tests, capture the bug as a failing test. It is your definition of done, and it stays in as a regression test.
- If you can't reproduce it, look for what differs between where it fails and where it doesn't: environment, data, timing, test order, versions. Try to make it fail more often (run it in a loop, shuffle the order, add load) before trying a fix. If it still won't reproduce, any fix is unverified, so say that plainly when you report.

## Investigate

- Read the evidence before guessing: the stack trace, the code it points to, the logs, the failing assertion.
- Check what changed recently in the affected code (`git log -p`, `git diff`). If there's a version where it worked, compare against it or use `git bisect`.
- If the project documents its architecture, schemas, or API contracts, read the parts that cover this code.
- When the evidence you have doesn't explain the failure, add instrumentation where expected and actual behavior first diverge: targeted logging, or a debugger if one is available. Mark temporary debug code so it's easy to find and remove.
- For a hard bug, keep a short list of hypotheses with the evidence for and against each. Test the one that's cheapest to confirm or rule out first, and change one thing at a time.
- If you spot other bugs along the way, note them and keep going on this one.

## Fix

- Fix the cause, not the symptom, with the smallest change that does it. Check whether existing code already handles this case before adding new code.
- Make the check pass honestly. Don't weaken, skip, or delete tests; don't suppress errors, type checks, or lint rules; don't add a broad catch; don't special-case the test input. If a test itself is wrong, say so and explain why.
- Ask before a fix that is destructive or hard to undo (data migrations, deleting data, schema or public API changes), or one much larger than the bug warrants. Otherwise go ahead.

## Verify

- Run the reproduction again; it should now pass. Then run the tests around the code you changed, and the build. Run the full suite if it's reasonably fast; if not, say which tests you ran.
- If the fix doesn't work, undo it before trying something else rather than stacking patches. After two failed attempts, stop and re-examine your assumptions against the evidence, or report what you've ruled out and ask.
- If the fix changes something a user sees, look at it running, not just at the test output.
- Remove temporary debug code.

## Report

- Lead with the cause and the fix, in a sentence or two.
- Show the evidence: the reproduction command or test, and its result before and after.
- Mention what else the change could affect, anything you couldn't verify, other places that may have the same bug, and docs that are now out of date.
