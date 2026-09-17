# Debugging and Regression Checks

Capture the failing command, input, relevant error, and expected result. Find the smallest reliable repro; an obvious local defect needs no investigation tour. Trace to the first violated contract rather than hiding the symptom with a retry or timeout.

Check the symptom on unfixed code when feasible, without disturbing the user's work, and verify the fix with a regression check; reuse existing coverage when it catches the break. If the original trigger or environment is unavailable, state the evidence and verification gap. Proceed only when evidence supports the fix; do not guess or claim an unreproduced failure was reproduced.

Name the production break and exercise the smallest real boundary that owns it. Derive expectations independently of production helpers. Source-text and private-structure assertions are change detectors unless that representation is the contract; exact bytes or messages are valid when promised. A new or changed test must fail for the intended break, not setup.

Keep mocks at external or slow boundaries and model failures. For generated properties, include known examples or an independent oracle; matching encoder/decoder bugs survive a naive round trip. Control time, randomness, and resources; wait for an observable condition instead of sleeping a flake away.
