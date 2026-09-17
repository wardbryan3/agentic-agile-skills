---
name: agile-init
description: Initialize Agentic Agile only when the user explicitly asks to set up Agile for the current project.
---

# Agile Init

Create the bounded operating record for one project. This is a one-time setup.

## Preconditions

1. Find the project root. Use the Git root when present; otherwise use the current working directory.
2. If `.agile/` already exists, stop. Report its location and do not overwrite it.
3. Collect, in as few exchanges as possible:
   - One paragraph describing the project, who it is for, and what working means.
   - Three to seven outcome candidates, each with a description and value if done.
   - Whether this workflow is `personal` or `shared`. Recommend `personal`.

## Create

Create `.agile/` with these files and no other files:

```text
.agile/
  config.yml
  vision.md
  backlog.md
  sprint.md
  log.md
```

Write `config.yml`:

```yaml
version: 2
project: "<repo-name>"
sharing: <personal|shared>
verification_window_seconds: 120
```

Write `vision.md`:

```markdown
# Vision

<user paragraph verbatim>

Last revised: <YYYY-MM-DD>
```

Write `backlog.md`. Assign stable IDs in order. Keep the user's wording concise and do not invent priority, estimates, acceptance criteria, or grouping.

```markdown
# Backlog

<!-- Personal outcome candidates. Pulling moves a line into the current sprint. -->

- [ ] O-001: <outcome> | Value: <value if done>
```

Write `sprint.md`:

```markdown
# Current Sprint

**Status:** none

_No sprint planned. Run agile-sprint to start one._
```

Write `log.md`:

```markdown
# Sprint Log

<!-- YYYY-MM-DD | <goal> | <met|learned|abandoned> | <evaluator>: <human verdict> -->
```

## Sharing

For a personal workflow in a Git repository, add `.agile/` to `.git/info/exclude` if it is not already present. Preserve the file and do not add a duplicate. This is a local exclusion, not a repository change.

For a shared workflow, leave `.agile/` available to version control. The person issuing an Agile command is the delegated human authority for that command.

Do not create `.agile/design/` yet. It is created only by an explicit `agile-design` request.

## Matt Integration

Detect whether `docs/agents/issue-tracker.md` and `docs/agents/domain.md` exist. Agile works without them. Mention `/setup-matt-pocock-skills` only when later work needs a tracker or shared domain-document flow.

## Report

Report the workflow location, sharing choice, two-minute verification window, and that the next action is `agile-sprint`.
