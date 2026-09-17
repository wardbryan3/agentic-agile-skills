---
name: agile-design
description: Create, revise, or promote a design-corpus document only when the user explicitly asks for that design-document work.
---

# Agile Design

Maintain the project's explicit design corpus. This skill is not a generic plan writer and never creates a design document from an implicit need during a sprint.

## Preconditions

Read `.agile/config.yml`. If Agile is not initialized, direct the user to `agile-init`.

Read relevant agent instructions, existing design documents, domain documents, ADRs, and code before deciding where the requested change belongs.

## Locate the Corpus

For `sharing: personal`, the corpus root is `.agile/design/`. Create it only for the explicit requested document. On the first request, ask whether the project needs a canonical overview document and which concise status language it uses, then record that convention in `config.yml` under `design`. You may read shared project documents for context but do not modify them from a personal workflow.

For `sharing: shared`:

1. Use the documented project convention when it exists.
2. Otherwise inspect for an established design corpus such as `docs/design/`.
3. If none exists, ask once for the corpus root, whether the project needs a canonical overview document, and concise status language. Record the agreed convention in `config.yml` under `design`. Do not create an index or session map unless the user explicitly requests one and it is useful.

Example optional configuration after that decision:

```yaml
design:
  root: docs/design
  canonical: PROJECT.md
  status_language: "draft, proposal, locked"
```

## Decide and Write

1. Find the single canonical place for the requested decision. Update an existing focused document when it owns the subject; otherwise create one focused document in the established corpus.
2. Keep design documents about intent, contracts, boundaries, alternatives, dependencies, open questions, and decision-relevant evidence. Link to code, schemas, research, benchmarks, prototypes, or tracker work only when they substantiate a decision. Do not write a file-by-file implementation plan.
3. After an explicit request, write the focused change directly once the meaning is clear. Stop for ambiguity, missing decisions, or a conflict with locked material.
4. When a request conflicts with locked material, quote the conflict and require an explicit human decision to revise it before editing. Only explicit human authority may mark material locked or otherwise settled.
5. Use the project's configured status language. Existing terminology always wins.
6. Do not archive superseded text. Preserve history in Git.
7. Keep one canonical decision record. Create or update an ADR only when it owns a distinct hard-to-reverse architectural trade-off; cross-link instead of repeating the decision.

## Resolve Unknowns

When the requested design change cannot be settled from available evidence, propose one exact Matt tool and why. After approval, invoke it immediately:

- `/grilling` for unresolved choices.
- `/prototype` for a question that must be run or seen.
- `/research` for external facts.
- `/domain-modeling` only in shared work when terminology or a distinct ADR-worthy trade-off changes.

In a personal workflow, keep this entire design flow private. Do not invoke a flow that writes shared domain documents or ADRs. When `/research` is approved for private Agile work, it returns cited findings without creating a standalone artifact.

`/research` is asynchronous. After launching it, record the research question as pending in the active sprint context when one exists, do not settle or write the requested decision from incomplete evidence, and report that the design request is pending. Resume `agile-design` after the findings return; then write or revise the canonical document and replace the pending context entry with its bounded result.

## Promote

On an explicit request to promote private design work, inspect the shared corpus, propose the target document or merge, and wait for approval before moving or rewriting material. Update references after promotion. Do not leave a duplicate canonical decision.

## Report

Report the canonical document changed, its status, any evidence links added, and any unresolved decision that still needs human authority. If an active sprint directly depends on this work, add the document source plus its bounded decision, result, and DoD impact to that sprint's `## Context`.
