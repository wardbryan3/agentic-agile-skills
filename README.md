# Agentic Agile Skills

An AI-agent workflow for running one human-judged sprint at a time. The Agile skills are the primary operating loop; selected Matt Pocock skills are approved in-sprint tools.

## Install

Install all skills for every detected agent in the current project:

```sh
npx skills add wardbryan3/agentic-agile-skills --all
```

Install the Agile loop globally for OpenCode:

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

Install the adapted delivery helpers when needed:

```sh
npx skills add wardbryan3/agentic-agile-skills \
  --skill implement \
  --skill research \
  --skill prototype \
  --agent opencode \
  --global \
  --yes
```

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

Install the broader Matt Pocock collection separately when it is not already available:

```sh
npx skills add mattpocock/skills --all
```

Personal Agile state lives under `.agile/` and is locally excluded from Git. Shared workflows leave `.agile/` tracked. Personal design work remains private under `.agile/design/`; shared design work follows the repository's established convention.

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
