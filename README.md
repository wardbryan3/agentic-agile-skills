# Agentic Agile Skills

An AI-agent workflow for running one human-judged sprint at a time. The Agile skills are the primary operating loop; selected Matt Pocock skills are approved in-sprint tools.

## Why This Exists

Matt Pocock's skills provide strong building blocks for discovery, implementation, testing, review, and delivery. This package adds the missing outer loop for AI-agent work: one visible sprint outcome, a human-judged Definition of Done, approved supporting gates, and an explicit design corpus.

The workflow exists to keep planning artifacts bounded. Personal Agile state lives in `.agile/`; durable design documents are created only by an explicit design request. Agents can escalate to Matt skills, but only after a human approves the escalation.

## Dependency and Installation Order

This repository is an overlay, not a fork of [mattpocock/skills](https://github.com/mattpocock/skills). It includes only five new Agile skills and three adapted Matt skills: `implement`, `research`, and `prototype`.

Install Matt's collection first, then install this overlay second. The order is required so the Agile-aware versions of those three skills win:

```sh
npx skills add mattpocock/skills --all
npx skills add wardbryan3/agentic-agile-skills --all
```

To install the Agile loop globally for OpenCode after Matt's skills are available:

```sh
npx skills add wardbryan3/agentic-agile-skills \
  --skill agile-init \
  --skill agile-sprint \
  --skill agile-checkin \
  --skill agile-review \
  --skill agile-design \
  --agent opencode \
  --global \
  --yes
```

Do not install Matt's collection after this overlay unless you reinstall the overlay afterward.

## Included Skills

| Skill | Purpose |
| --- | --- |
| `agile-init` | Create the bounded Agile operating record for a project. |
| `agile-sprint` | Start one flexible, human-judged sprint. |
| `agile-checkin` | Keep one live factual sprint snapshot. |
| `agile-review` | Close a sprint as `met`, `learned`, or `abandoned`. |
| `agile-design` | Maintain an explicit private or shared design corpus. |
| `implement` | Adds Agile supporting-gate and two-minute verification-budget behavior. |
| `research` | Keeps research private when invoked by a personal Agile flow. |
| `prototype` | Keeps throwaway prototype branches private in a personal Agile flow. |

## Workflow

1. Run `agile-init` in a project and choose personal or shared state.
2. Run `agile-sprint` to move one primary outcome, plus directly enabling outcomes, into the active sprint.
3. Use `agile-checkin` to update the current facts and approve any escalation.
4. Use `agile-review` after a named human evaluates the result.
5. Use `agile-design` only for explicitly requested design-corpus work.

The Definition of Done always requires human inference. Tests, builds, benchmarks, linting, and code review are supporting gates. The default verification window is 120 seconds; commands expected to exceed it require immediate approval.

## Matt Skill Integration

Agile proposes a Matt skill when work changes shape, then invokes it after approval. The intended companion skills are `grilling`, `domain-modeling`, `prototype`, `research`, `diagnosing-bugs`, `to-spec`, `to-tickets`, `implement`, `tdd`, `code-review`, and optionally `setup-matt-pocock-skills`.

Personal Agile state lives under `.agile/` and is locally excluded from Git. Shared workflows leave `.agile/` tracked. Personal design work remains private under `.agile/design/`; shared design work follows the repository's established convention.

## Upstream Sync

The adapted Matt skills are deliberately vendored so Agile can alter their behavior. [UPSTREAM.md](UPSTREAM.md) records their upstream source and base commit. A weekly GitHub Actions workflow opens one issue when `implement`, `research`, or `prototype` changes upstream. Review that diff manually and update the recorded base only after intentionally merging the change.

## Repository Layout

`npx skills` discovers each package beneath `skills/<skill-name>/SKILL.md`.

```text
skills/
  agile-init/
  agile-sprint/
  agile-checkin/
  agile-review/
  agile-design/
  implement/
  research/
  prototype/
```

## License and Attribution

The Agile skills are authored for this repository. `implement`, `research`, and `prototype`, including Prototype's reference files, are adapted from [mattpocock/skills](https://github.com/mattpocock/skills) and remain available under the MIT License. See [LICENSE](LICENSE).
