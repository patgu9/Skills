# Design Doc contract

This contract owns file placement, IDs, supporting files, versions, and approval states. The [template](../assets/design-doc-template.md) owns document layout; [discovery and specification workflow](discovery-methods.md) owns product decisions; [product review](adversarial-review.md) owns validation.

## Inputs

Accept a goal, available context and constraints, user answers, and any feedback on an existing product baseline. Discovery can start from an incomplete goal. Investigate available facts first and record unresolved questions through the [clarification protocol](discovery-methods.md#clarification-protocol).

For a continuation or revision request, read the existing artifacts and verify their versions and approval evidence. Missing, conflicting, or stale required inputs block dependent edits. Report what is missing and which sections are affected. Never reconstruct an approved baseline from memory.

## Saving

Save the Design Doc at `<project-root>/doc/YYYY-MM-DD-task-slug/product-design.md`. One product change uses one stable task directory across revisions.

Before saving:

1. Resolve `<project-root>` from project instructions and workspace context.
2. Reuse the existing task directory when continuing or revising the same product change. If continuation vs. a new change remains unclear after inspecting `doc/`, ask the user.
3. For a new change, name the task directory `YYYY-MM-DD-task-slug` using the start date and a short lowercase hyphenated English capability name. If another change already uses that directory name, append `-02`, `-03`, or the next unused suffix. Never overwrite unrelated files.

Keep all artifacts for the change in the same task directory:

| File | Purpose | Template |
| --- | --- | --- |
| `product-design.md` | Authoritative product intent, approach, scope, rules, and acceptance examples | [Design Doc](../assets/design-doc-template.md) |
| `product-design-questions.md` | Open and resolved `Q<n>` records, assumption validation plans, and baseline history | [Questions and decisions](../assets/questions-template.md) |
| `product-design-review.md` | Review attempts (`Attempt <n>`), findings (`R<n>`), remedies, and verification evidence | [Review record](../assets/review-template.md) |

When the first question or review record is needed, create `product-design-questions.md` or `product-design-review.md`. Do not create empty supporting files. In the Design Doc's **Supporting Records** line, link existing supporting files with relative paths and mark uncreated files `Not started`. Supporting files must link back to `[Product Design](product-design.md)`.

## Structure and content placement

Unless the user supplies a replacement template, follow the exact heading order, metadata fields, and table columns in [design-doc-template.md](../assets/design-doc-template.md). Repeat only Feature blocks (`#### Feature <n> — $Capability Name$`). Only **Constraints** and **Boundaries and Dependencies** are optional. When saving, replace placeholders and remove instructional HTML comments.

Write the Design Doc and supporting files in English using [Technical Writing](../../technical-writing/SKILL.md). Keep conversation progress updates outside the saved files.

| Section or file | Required content |
| --- | --- |
| **Glossary** | Domain terms and abbreviations, with one definition and boundary per concept |
| **Problem Statement** | Actor, segment, situation, unmet need, workaround, consequences, evidence, and optional constraints |
| **What Makes This Cool** | Concrete value over actual alternatives (including the status quo), with untested claims marked |
| **Approaches Considered** | Comparison of at least two approaches by journey, value, effort (`S/M/L/XL`), risk (`Low/Medium/High`), and rejection reason |
| **Recommended Approach** | **Recommendation**, **How It Works**, **Scope**, **Assumptions and Limits**, and **Next Action** |
| **Success Criteria** | `SC<n>` table with desired outcome, pass condition, guardrails, and measurement context ([details](discovery-methods.md#define-success-criteria)) |
| **Requirements (Feature blocks)** | User-valued capabilities containing **User Story**, **Rules** (`F<n>-AC<m>`), and **Key Examples** (`F<n>-E<m>`) |
| `product-design-questions.md` | Full `Q<n>` records, assumption validation follow-up, and `Baseline and Feedback History` |
| `product-design-review.md` | Review state, attempt logs, and `R<n>` findings with verification history |

`product-design.md` must explain the current design without requiring readers to reconstruct discovery logs. Apply confirmed answers directly to `product-design.md`, and keep full question and review histories in the supporting files. Mark unresolved behavior or metrics in `product-design.md` as `TBD (Q<n>)` beside the affected item.

## Feature rules

1. **User Story:** Use `value → role → action` order and link defined `SC<n>` IDs.
2. **Stable IDs:** Number rules `F<n>-AC<m>` and examples `F<n>-E<m>`. Preserve existing IDs across revisions; never reuse deleted IDs.
3. **Rule coverage:** Cover every `F<n>-AC<m>` rule with at least one `F<n>-E<m>` example. Each example must state concrete given facts, a when action or event, and an observable then outcome across normal, boundary, and exception cases.
4. **Format:** Use the template's **Key Examples** table by default. If narrative examples are clearer for complex state, use the format below instead (do not duplicate both):

```markdown
**F1-E1: Scenario name**
- **Related Rule:** F1-AC1
- **Given:** Concrete context and input.
- **When:** Business action or event.
- **Then:** Observable result.
```

## Supporting record rules

### Question records

Use [questions-template.md](../assets/questions-template.md) for `product-design-questions.md` and give each question a stable `### Q<n>` heading:

- Record the answer or finding before its basis and source (user turn, file path, or tool output).
- Distinguish reported experience, direct observation, stated intent, agent inference, and hypothetical cases.
- For `User decision` records, retain the options, tradeoffs, recommendation, and reason.
- When a review finding (`R<n>`) requires user clarification, link `Q<n>` and `R<n>` in both files. Answering `Q<n>` does not close `R<n>` until verification confirms the resulting edit under [review rules](adversarial-review.md#record-and-approval).

### Assumption validation

Keep each material assumption and its product impact concise in **Assumptions and Limits** inside `product-design.md`. Track unverified material assumptions as `Fact to investigate` `Q<n>` records in `product-design-questions.md`:

1. **Evidence / Validation Status:** State what to observe, how to observe it, the disconfirming result or threshold (never invented), and linked `SC<n>` IDs.
2. **Follow-up:** Name the decisions and `SC<n>` or `F<n>` IDs to reopen if the assumption fails, plus the next validation action.

## Versions and approval evidence

- Start at `Version: v1`. Increment `v<n>` (`v2`, `v3`, ...) only when substantive changes alter a version already delivered for review or approval. Work in progress keeps its current version number; typographic edits alone do not increment the version.
- Before modifying a delivered version, save its snapshot at `history/product-design/v<n>.md` in the task directory (unless already saved in an accessible git commit). Log the revision reason under `Baseline and Feedback History` in `product-design-questions.md`.
- Keep `Approval: Pending` while `Status` is `DRAFT` or `IN_REVIEW`.
- Set `Approval: <version> | <YYYY-MM-DD> | <human approver> | <evidence reference>` only after the user explicitly approves that exact version.

## Status and approval

- **`DRAFT`:** Discovery is incomplete, open questions block core behavior, or review findings remain unresolved.
- **`IN_REVIEW`:** All required sections are complete, review passed with no approval blockers, and the document is ready for user confirmation.
- **`APPROVED`:** The user explicitly approved the current `Version`.

Open issues about core users, scope, or required behavior block `IN_REVIEW` and `APPROVED` unless the user excludes that scope (`EXCLUDED`). If material changes occur after approval, save the prior baseline snapshot and increment `Version`. Then reset `Status: DRAFT` and `Approval: Pending`, and re-run review before requesting approval.
