---
name: agile-review
description: Close an active Agentic Agile sprint only when the user explicitly asks to close or review that Agile sprint.
---

# Agile Review

Close one active sprint with an honest human verdict. This resets the one live sprint and appends the permitted log record; it does not generate another planning artifact.

## Preconditions

Read `.agile/config.yml`, `.agile/backlog.md`, `.agile/sprint.md`, and `.agile/log.md`. Validate the active-sprint shape from `agile-sprint`. If the sprint is inactive or malformed, stop rather than guessing.

## Verify

1. Read the goal, DoD, context record, and every supporting gate.
2. Inspect available evidence. Run unchecked relevant gates only within the configured verification window, or obtain immediate approval before a command can exceed it.
3. If code changed, an appropriate code-review gate must be checked. `/implement` normally supplies this gate through its built-in `/code-review` step.
4. A relevant failed or unchecked supporting gate prevents a `met` result. It may still close as `learned` or `abandoned` once the result is understood.
5. Ask for the named human evaluator and one direct verdict. The allowed classifications are:
   - `met`: the evaluator observed the DoD and concluded it was satisfied.
   - `learned`: the DoD was not met, but the evaluator gained a useful conclusion.
   - `abandoned`: the goal was wrong or no longer worthwhile.

## Reconcile

For every pulled outcome candidate, use the exact original Markdown line preserved under the primary or supporting heading:

- Remove it from the sprint without restoring it when it is met or no longer valuable.
- Restore its exact original line to `backlog.md` when it remains relevant.
- Ask the command holder only when the evidence does not make that choice clear.

Append exactly one line to `log.md`:

```text
YYYY-MM-DD | <goal> | <met|learned|abandoned> | <evaluator>: <human verdict>
```

Replace the whole sprint file with:

```markdown
# Current Sprint

**Status:** none

_No sprint planned. Run agile-sprint to start one._
```

## Report

Report the log line, returned-candidate count, and any unchecked or failed gate that prevented `met`.

## Guardrails

- A test passing does not satisfy the DoD; human inference does.
- Do not archive, retroactively create a design document, or create a new sprint during review.
- A scope replacement always closes and logs the prior sprint first.
