---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets. At the start, inspect Git status and preserve unrelated changes. Do not stage or commit unrelated work; if the requested work cannot be committed independently, ask the user how to proceed. When the work is in an active Agile sprint, record the current `HEAD` SHA as the review base.

Use /tdd where possible, at pre-agreed seams.

When `.agile/config.yml` exists and `.agile/sprint.md` has `**Status:** active`, read `verification_window_seconds` from the config. It defaults to 120 seconds.

In an active Agile sprint, read the approved `## Supporting Gates` from the sprint. The code-review gate is post-commit; every other approved gate is pre-commit. Run typechecking and focused test files only when they satisfy an approved gate. If TDD needs an unapproved validation command, ask the calling Agile skill to propose that gate before running it. Before starting any validation command expected to exceed the verification window, obtain immediate user approval. When duration is unknown, run it with a timeout no longer than the window and report the timeout rather than continuing. Do not run the full suite after every change. Run it at most once at the end, and only when it fits the verification window or the user explicitly approves the longer wait. Report each passed or failed pre-commit gate to the calling Agile skill so it can update its supporting-gate checklist.

Outside an active Agile sprint, run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once every approved pre-commit gate passes, commit the implementation work. The code-review gate runs after this commit: use `/code-review <review-base>` so it reviews the implementation commit rather than an empty uncommitted diff. If review findings require fixes, commit the fixes and rerun `/code-review <review-base>` before reporting completion. Report the final code-review result to the calling Agile skill so it can check that gate.
