# Discovery and Specification Methods

Use these rules alongside the [document contract](document-contract.md) when framing problems, asking questions, comparing approaches, and specifying testable behavior.

## Clarification protocol

When a missing fact, ambiguous term, or unmade decision affects the design:

1. **Investigate first:** Check repository docs, code, and prior turns before asking the user.
2. **Track material questions (`Q<n>`):** Log unresolved questions in `product-design-questions.md` with a stable `Q<n>` ID (`OPEN`, `WAITING`, `RESOLVED`, `UNKNOWN`, or `EXCLUDED`). Never renumber or reuse IDs.
3. **Ask 1–3 focused questions per turn:** Ask 1 question by default (at most 3 mutually independent questions).
   - For **decisions**, state the options, tradeoffs, and your recommendation with its reason.
   - For **ambiguous boundaries**, test with concrete counterexamples (such as `https://example.com/a` vs. `https://example.com/a/`).
4. **Apply answers strictly:**
   - **Answered:** Set `RESOLVED` and update `product-design.md`.
   - **Skipped or unknown:** Set `UNKNOWN`, mark dependent items `TBD (Q<n>)` in `product-design.md`, and propose either a validation step or a scope exclusion.
   - **Scope dropped:** Set `EXCLUDED` and remove or defer the affected Feature.
   - **Prior decision reversed:** Preserve the old decision in `History`, reopen dependent questions, and update affected sections.

## Mode: Startup vs. Builder

- **`Startup` (Customer or internal adoption):** Require target-user evidence, current workarounds, switching friction, and measurable outcomes. Separate stakeholder opinions from observed user behavior.
- **`Builder` (Personal tools, learning, demos, open-source exploration, creative work):** Completion, personal utility, and a working demonstration are valid outcomes. Identify who will try the project, what makes it useful over the closest alternative, and the smallest usable result. Do not require market sizing, revenue models, or customer interviews.

## Frame Context and Problem

1. **Anchor in a concrete event:** Identify the actor, trigger situation, goal, obstacle, current workaround, and consequence. Replace vague claims ("slow", "often") with a specific case or mark the scenario as hypothetical.
2. **Separate need from solution:** Capture the unmet need in **Problem Statement** before proposing features.
3. **Define value over the status quo (`What Makes This Cool`):** State why the change matters compared with existing alternatives, including manual workarounds or doing nothing.

## Explore Approaches and Converge Scope

1. **Compare at least two viable approaches:** In **Approaches Considered**, compare realistic options (including the status quo or a minimal workflow change) across user journey, value, effort (`S/M/L/XL`), and risk (`Low/Medium/High`).
2. **Trace every Feature to behavior change:** Each included Feature (`F<n>`) must support an agreed outcome (`SC<n>`) or constraint. Record explicit exclusions with reasons.
3. **Specify `How It Works`:** Write a numbered end-to-end flow stating the trigger, actor, action, handoffs, observable result, and linked `SC<n>` and `F<n>` IDs. Include failure and recovery paths.
4. **Surface key assumptions and `Next Action`:** Identify the value, usability, or feasibility assumption whose failure would invalidate the design. Log its validation plan in `product-design-questions.md` and define one concrete **Next Action** with an observable outcome.

## Define Success Criteria

- **Quantitative `SC<n>` (`Startup`):** Specify the metric (including rate numerator and denominator), baseline, target, units, eligible population, measurement window, and verification method. Unknown baselines or targets must be marked `TBD (Q<n>)`.
- **Guardrails:** Add a guardrail `SC<n>` row whenever optimizing the primary metric could degrade another critical outcome (such as latency or error rate).
- **`Builder` pass condition:** An observable task completion or working demonstration is sufficient.

## Specify Features by Example

For each Feature (`F<n>`) under [Feature rules](document-contract.md#feature-rules):

1. **User Story (`value → role → action`):** Write `In order to <outcome>, as a <role>, I want to <capability>` linked to `SC<n>`.
2. **Business Rules (`F<n>-AC<m>`):** State the condition, actor, required system behavior, units, and exact inclusive/exclusive boundaries. State exceptions separately.
3. **Key Examples (`F<n>-E<m>`):** Cover every `F<n>-AC<m>` rule across normal, boundary, and rejection cases. Test both sides of every limit (for example, adding at 9 succeeds → 10; adding at 10 is rejected → stays 10).
4. **AI / non-deterministic behavior (when applicable):** Specify representative inputs, unacceptable outputs, and observable fallback or user-correction paths. Never promise accuracy targets without evaluation evidence.

## Step 5: Revisit a Product Baseline

When new feedback or evidence challenges an existing Design Doc:

1. Save the prior delivered version snapshot to `history/product-design/v<n>.md` and log the revision reason in `product-design-questions.md` (`Baseline and Feedback History`).
2. Reopen only the `SC<n>`, `F<n>`, `F<n>-AC<m>`, or `F<n>-E<m>` items whose basis changed; preserve unaffected decisions.
3. Re-verify modified sections before requesting approval on the incremented version (`v<n+1>`).
