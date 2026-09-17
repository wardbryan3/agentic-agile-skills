---
name: agile-checkin
description: Run an explicit Agentic Agile checkin when the user asks for an Agile sprint checkin or Agile sprint status.
---

# Agile Checkin

Update the live sprint with the current facts. A checkin is not a planning ceremony.

## Preconditions

Read `.agile/config.yml` and `.agile/sprint.md`. Use the active-sprint definition from `agile-sprint`. If no sprint is active, say so and offer `agile-sprint`. Do not create or replace a sprint here.

## Check In

1. State the goal and Definition of Done in one line each.
2. Ask in one exchange:
   - What moved?
   - What broke or blocked?
   - Is the human verdict closer, or is the goal invalid?
3. Replace the `## Progress` section with a current snapshot only:

```markdown
## Progress

- Done: <current facts>
- In progress: <current facts>
- Blocked: <current facts>
```

4. Set `**Consecutive no-progress checkins:**` to zero when anything moved; otherwise increment it. After two consecutive no-progress checkins, plainly offer to close the sprint as `learned` or `abandoned`.
5. If the goal is invalid, do not rewrite it. Close the sprint with `agile-review`, log its outcome, then start a replacement sprint with `agile-sprint`.
6. When the work discovers a worthwhile outcome, either the agent or a human may propose one line with its value. In a personal workflow only the user approves it; in a shared workflow the command holder is delegated authority. Add it to the backlog only after approval, using the next unused `O-###` ID.
7. When changed work makes a supporting gate relevant, propose the gate and update the checklist only after the same approval rule.
8. When complexity changes the work shape, use the same Matt routing conditions as `agile-sprint`. In a personal workflow, do not propose a flow that writes shared domain documents or ADRs. After approval, invoke the skill immediately, add its source plus at most three decision-relevant clauses to `## Context`, and check only the supporting gates the returned evidence explicitly passes. For `/research`, record the question as pending and update it only after the background work completes.
9. If the DoD appears satisfied, offer `agile-review`. Do not close it yourself.

## Guardrails

- Keep progress factual and current. Do not append a checkin transcript.
- Preserve the one goal. New independent work belongs in the backlog.
- Do not create a design document, tracker item, or retrospective from a checkin without the explicit approved flow that owns it.
