---
name: agile-sprint
description: Start an explicit Agentic Agile sprint when the user asks to begin or plan an Agile sprint for the current project.
---

# Agile Sprint

Start one goal-boxed sprint. A sprint may be a small discovery or a feature-sized delivery, but it always has one human-judged outcome.

## Preconditions

Read `.agile/config.yml`, `.agile/vision.md`, `.agile/backlog.md`, and `.agile/sprint.md`.

An active sprint contains all of these:

- `**Status:** active`
- `**Goal:**`
- `## Definition of Done`

The inactive template has `**Status:** none`. If the file is malformed, stop and ask the command holder to repair or confirm the state. If a sprint is active, do not overwrite it. Direct the user to `agile-review` first.

## Plan

1. Quote the vision in one line and read every backlog candidate.
2. Propose two to four candidate goals. Favor a single outcome that a human can judge, not an estimate, task list, or test result.
3. Recommend one goal. The command holder chooses it.
4. Select one primary outcome candidate. Supporting candidates are allowed only when they directly enable the same goal. A pure discovery sprint may have no pulled candidate.
5. Draft a Definition of Done that requires human inference. A passing test, build, benchmark, or lint command is supporting evidence only, never the DoD.
6. Inspect the project's validation commands and propose the few supporting gates relevant to this goal. The command holder approves, edits, or removes them. Code-changing work includes a narrow typecheck gate, a focused-test gate, and an appropriate code-review gate. The code-review gate is mandatory once code-changing work is approved.
7. If the work shape warrants another tool, propose one exact Matt skill and why:
   - `/grilling` for unresolved design choices.
   - `/domain-modeling` only for shared work that changes project vocabulary or creates a distinct ADR-worthy trade-off.
   - `/prototype` for a question that must be run or seen.
   - `/research` for external facts.
   - `/diagnosing-bugs` for a hard or intermittent defect.
   - `/to-spec` then `/to-tickets` for multiple independent delivery slices.
   - `/implement` for understood code work.
   Before proposing a shared flow that needs a tracker, verify Matt tracker configuration exists. If it does not, propose `/setup-matt-pocock-skills` first. Do not invent a tracker artifact.
8. Once the command holder approves the sprint contents, move each selected backlog line exactly from `backlog.md` to `sprint.md` and write the active sprint before invoking another skill. Do not copy or rewrite the selected lines.
9. After approval, invoke the chosen Matt skill immediately. A personal sprint may create shared tracker artifacts only after this explicit approval. Record the result in the bounded context record and check only the supporting gates the returned evidence explicitly passes. For `/research`, record the question as pending; replace it with the result only after the background research completes.

## Write

Write this shape to `.agile/sprint.md`:

```markdown
# Current Sprint

**Status:** active
**Goal:** <one human-judged outcome>
**Started:** <YYYY-MM-DD>

## Definition of Done

<A named human can observe the result and conclude ...>

## Supporting Gates

- [ ] <approved validation or review gate>

## Pulled Outcome Candidates

### Primary

- [ ] O-001: <outcome> | Value: <value>

### Supporting

- [ ] O-002: <outcome> | Value: <value>

## Context

- None yet

## Progress

- Done: none
- In progress: <first concrete action>
- Blocked: none

**Consecutive no-progress checkins:** 0
```

Use `None` under `### Primary` for an approved pure discovery sprint and under `### Supporting` when none are pulled. Preserve every moved backlog line byte-for-byte. Replace `- None yet` with one bullet per source, containing at most three concise clauses: decision, result, and DoD impact. Do not turn this into a copied spec or execution narrative.

## Verification Budget

The configured verification window defaults to 120 seconds. Do not start a verification command expected to exceed that window without a separate immediate approval, even when its checkbox was approved. Focused checks run during work. A full suite runs at most once at the end and only within the window or after explicit approval.

## Report

Report the goal, human DoD, approved supporting gates, any invoked Matt flow, and the first action.
