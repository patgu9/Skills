---
name: product-design
description: Use when the user wants to turn a rough idea, feature request, or user problem into a product design doc (`product-design.md`), clarify product scope, compare product approaches, or specify testable acceptance rules and examples. Do not use for UI visual styling, technical architecture (Tech Spec), or code implementation.
---

# Product Design

## Goal

Collaborate with the user to turn an initial idea, problem, or revision request into a verified, example-driven English Design Doc (`product-design.md`) under `<project-root>/doc/YYYY-MM-DD-task-slug/`.

## Core Constraints & Decision Gates

1. **Choose the right mode ([Startup vs. Builder](references/discovery-methods.md#mode-startup-vs-builder)):**
   - **`Startup` (customer or internal adoption):** Require evidence of target-user pain, current workarounds, switching friction, and measurable outcome targets.
   - **`Builder` (personal tools, demos, learning, creative projects):** Accept personal utility, learning, or a working demonstration as valid success criteria. Never demand market sizing or revenue models.
2. **Clarify before guessing ([Clarification protocol](references/discovery-methods.md#clarification-protocol)):**
   - Inspect existing repository docs and code first.
   - When a missing fact, ambiguous boundary, or unmade tradeoff decision materially affects the design, pause and ask **1–3 focused questions**. Record material open questions as `Q<n>` in `product-design-questions.md`.
   - Confirm direction with the user when comparing viable approaches or narrowing scope before writing detailed feature specs.
3. **Deliverable & ID contract ([Document contract](references/document-contract.md)):**
   - Follow [design-doc-template.md](assets/design-doc-template.md) and write prose in English using [Technical Writing](../technical-writing/SKILL.md).
   - Compare at least two meaningful approaches (including the status quo or minimal change where relevant).
   - Every included Feature (`F<n>`) must trace to a Success Criterion (`SC<n>`), define testable business rules (`F<n>-AC<m>`), and cover normal, boundary, and rejection cases with concrete examples (`F<n>-E<m>`).
   - Create supporting files (`product-design-questions.md`, `product-design-review.md`) from their templates only when the first `Q<n>` or `R<n>` record is needed.
4. **Review & approval gates ([Product review](references/adversarial-review.md)):**
   - Run up to 3 review attempts against [adversarial-review.md](references/adversarial-review.md), logging findings as `R<n>` in `product-design-review.md`.
   - Set `Status: IN_REVIEW` only when zero approval-blocking findings or open core `Q<n>` items remain.
   - Set `Status: APPROVED` only after explicit user confirmation of that version. Before modifying any previously delivered version, save a snapshot to `history/product-design/v<n>.md`.

## Working References

| Reference | When to read |
| --- | --- |
| [Discovery and specification methods](references/discovery-methods.md) | Framing problems, comparing approaches, defining `SC<n>`, Specification by Example, and baseline revisions |
| [Document contract](references/document-contract.md) | File paths, `SC<n>`/`F<n>`/`Q<n>`/`R<n>` ID stability, version snapshots, and status rules |
| [Product review](references/adversarial-review.md) | Reviewing a draft before transitioning `DRAFT` → `IN_REVIEW` |
| [Templates](assets/design-doc-template.md) | Creating `product-design.md`, [questions](assets/questions-template.md), or [review](assets/review-template.md) files |

## Gotchas (Common Agent Mistakes)

1. **Inventing policies, thresholds, or metrics:** Making up business limits (`max 10 items`), SLAs (`p99 < 200ms`), retention periods (`7 days`), or target conversion rates to fill a table. Never invent product policy—mark unknown values `TBD (Q<n>)` and ask the user.
2. **Asking questions that the workspace already answers:** Interrupting the user with discovery questions before reading `CONTEXT.md`, `README.md`, existing docs, or code in the repository.
3. **Treating silence, skipped questions, or agent recommendations as approval:** Marking a `Q<n>` record `RESOLVED` or setting `Status: APPROVED` because the agent recommended an option or the user skipped a question. Unanswered questions stay `UNKNOWN` (`TBD (Q<n>)`).
4. **Forcing `Startup` rituals onto `Builder` projects:** Demanding TAM, revenue models, or user interview evidence when the user is building a personal utility, prototype, or learning project.
5. **Writing happy-path-only examples:** Specifying a numeric or state boundary (such as a 10-item limit) without testing both sides of the boundary (`9 → 10 accepted` and `10 → 11 rejected, count remains 10`).
6. **Setting up strawman alternatives:** Inventing an obviously broken option in `Approaches Considered` just to fill two rows, instead of comparing realistic alternatives (such as the status quo, a manual workflow, or a smaller-scope approach).
7. **Restating a proposed feature as the Problem Statement:** Writing "Users lack a CSV export button" as the problem instead of capturing the underlying actor, trigger, unmet need, and current workaround.
