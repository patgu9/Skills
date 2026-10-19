# Product review

In **Step 4**, evaluate `product-design.md` and any existing supporting files (`product-design-questions.md`, `product-design-review.md`) against the checks below. If an independent reviewer is available, run an independent review before presenting the design for approval. Otherwise perform a self-review and record why independent review was not run. Review verifies quality and completeness; only the user grants approval.

## Product review boundary

Evaluate user goals, value over alternatives, workflow coherence, scope discipline, and observable acceptance criteria (including boundary and failure paths). Leave technical implementation details (schemas, storage engines, internal APIs) out of scope unless concrete evidence shows that a product promise conflicts with a stated constraint.

## Final review

Evaluate each area across the current Design Doc and supporting files:

| Workflow step | Review check |
| --- | --- |
| **Step 1: Problem & Value** | Actor, situation, unmet need, workaround, and value over alternatives (`What Makes This Cool`) are clear without the conversation. Facts, intent, and hypotheses remain distinct. |
| **Step 2: Approach & Scope** | At least two approaches serve the same goal. Included Features connect to actor behavior changes, exclusions have reasons, assumptions link to validation plans, and **Next Action** is concrete. |
| **Step 2: Workflow Journey** | **How It Works** steps, triggers, actor handoffs, terms, and shared dependencies match the Feature blocks and cover failure and recovery paths. |
| **Step 3: Success Criteria** | Each `SC<n>` defines a real outcome, pass condition, guardrails, units, population, window, and verification method (or a `Builder` trial). Unknowns link to `Q<n>`. |
| **Step 3: Rules & Examples** | Each Feature is a user capability with a `value → role → action` User Story linked to `SC<n>`. Concrete `F<n>-E<m>` examples cover every `F<n>-AC<m>` rule, including boundaries and rejections. No policies are invented. |
| **Decisions & Language** | Confirmed `Q<n>` answers are applied to `product-design.md`; unresolved items are marked `TBD (Q<n>)` with blocker status. Prose follows [Technical Writing](../../technical-writing/SKILL.md). |

## Structural validation

Verify compliance with the [document contract](document-contract.md) and templates:

- Heading order, metadata fields (`Status`, `Version`, `Approval`, `Mode`, `Date`, `Stage`, `Supporting Records`), and table columns match [design-doc-template.md](../assets/design-doc-template.md). Placeholders and HTML comments are removed.
- IDs (`SC<n>`, `F<n>`, `F<n>-AC<m>`, `F<n>-E<m>`, `Q<n>`, `R<n>`) are unique, stable, and never reused after deletion.
- Relative links between `product-design.md`, `product-design-questions.md`, and `product-design-review.md` resolve cleanly. Full question and review histories stay in the supporting files.
- `Version`, `Status`, `Approval`, and any prior snapshots in `history/product-design/v<n>.md` match [version and status rules](document-contract.md#versions-and-approval-evidence).

## Review loop — maximum three attempts

An attempt is one complete review pass. Allow at most **three** attempts.

1. **Run review pass:** Evaluate the draft against [Final review](#final-review) and [Structural validation](#structural-validation). Record any defects or gaps as stable `R<n>` findings in `product-design-review.md` using [review-template.md](../assets/review-template.md).
2. **Evaluate stop conditions:** Stop the review loop immediately if any condition below applies:
   - **Zero open findings remain:** Set `Status` to `IN_REVIEW`.
   - **Attempt 3 is complete:** Report any remaining findings to the user and keep `Status: DRAFT`.
   - **A finding requires a user decision or missing fact:** Link a `Q<n>` record in `product-design-questions.md` and pause the review loop. Ask the user via the [clarification protocol](discovery-methods.md#clarification-protocol), then resume at step 3 if attempts remain.
   - **No progress:** The same defect persists after a correction attempt.
3. **Apply remedies:** Fix wording, structure, or internal inconsistencies within the agreed product decisions. If a fix alters a previously delivered version, follow [version rules](document-contract.md#versions-and-approval-evidence).
4. **Verify fixes:** Re-evaluate modified sections and open `R<n>` findings in the next attempt. Mark an `R<n>` finding `RESOLVED` only when verification confirms the fix in `product-design.md`.

## Record and approval

Maintain `product-design-review.md` using [review-template.md](../assets/review-template.md):

- Assign each finding a stable `R<n>` ID. Record its location, problem, basis, consequence, remedy, approval impact (`Blocks approval: Yes / No`), and verification history. Never renumber or reuse `R<n>` IDs.
- Record each attempt's reviewed version, method (`Independent reviewer` or `Self-review`), coverage, and outcome.
- Apply the contract's [status and approval rules](document-contract.md#status-and-approval) after the loop concludes.
