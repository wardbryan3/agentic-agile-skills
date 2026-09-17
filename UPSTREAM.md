# Upstream Tracking

This repository is an overlay, not a fork. It tracks only the upstream skills whose behavior is adapted for Agentic Agile.

**Source:** [mattpocock/skills](https://github.com/mattpocock/skills)

**Base commit:** `959a8e9f1edc3adbe2f7e3054bb6fbefa6696260`

## Adapted Skills

| Upstream path | Overlay path | Agile adaptation |
| --- | --- | --- |
| `implement/` | `skills/implement/` | Approved supporting gates, a 120-second verification budget, and a post-commit review base. |
| `research/` | `skills/research/` | No standalone research artifact in a personal Agile flow. |
| `prototype/` | `skills/prototype/` | No push or shared issue update in a personal Agile flow. |

## Sync Policy

1. The scheduled monitor compares the recorded base against the current upstream `main` branch.
2. It opens one issue only when an adapted upstream path changed.
3. Review the upstream diff, preserve the Agile behavior, and merge only changes worth adopting.
4. Update the base commit in this file after the reviewed sync is merged.

Do not merge upstream wholesale. The rest of Matt's skills remain an external dependency installed before this overlay.
