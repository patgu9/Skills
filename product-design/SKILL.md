---
name: product-design
description: Explore product needs, choose opportunities and scope, define success, and specify behavior with examples. Create or revise an English Design Doc in the Think stage. Use for product discovery and requirements, not visual styling or implementation planning.
---

# Product Design

Guide the user from an initial idea or problem to an example-driven English Design Doc (`product-design.md`). Run the five steps below in order. When a missing fact or decision would materially change the design, pause and ask the user.

## Working references

Read only the reference needed for the current step:

| Reference | Responsibility |
| --- | --- |
| [Discovery and specification workflow](references/discovery-methods.md) | Problem framing, clarification, approach comparison, scope convergence, and Specification by Example |
| [Document contract](references/document-contract.md) | File paths, ID rules, supporting files, versions, and status transitions |
| [Product review](references/adversarial-review.md) | Content and structural review checks, plus the 3-attempt review loop |
| [Design Doc](assets/design-doc-template.md), [Questions](assets/questions-template.md), [Review](assets/review-template.md) | Output templates; create supporting files only when the first record is needed |

---

## Workflow

### Step 1: Frame Context and Problem

1. **Inspect context:** Read project instructions, domain terms, relevant files, and any existing task directory under [saving rules](references/document-contract.md#saving). Distinguish approved baselines, drafts, and new requests. If new feedback challenges an existing baseline, follow [baseline revision](references/discovery-methods.md#step-5-revisit-a-product-baseline).
2. **Select mode:** Choose [Startup or Builder](references/discovery-methods.md#mode-startup-vs-builder). If the mode is unclear and changes the required evidence, ask the user.
3. **Frame the problem:** Identify the target actor, situation, unmet need, current workaround, and evidence using [problem framing](references/discovery-methods.md#step-1-frame-context-and-problem).
4. **Gate — Clarify before solving:** If the actor, trigger, or desired outcome is unclear, follow the [clarification protocol](references/discovery-methods.md#clarification-protocol). Investigate available facts first, then ask 1–3 focused questions. Record material open questions in `product-design-questions.md`.
5. **Draft sections:** Complete **Glossary**, **Problem Statement**, and **What Makes This Cool** in [design-doc-template.md](assets/design-doc-template.md).

### Step 2: Explore Approaches and Converge Scope

1. **Connect goal to behavior:** Identify which actor behavior must change or which obstacle must be removed ([approach exploration](references/discovery-methods.md#step-2-explore-approaches-and-converge-scope)).
2. **Compare approaches:** Define at least two meaningful ways to achieve the goal, including minimal or existing-workflow alternatives where relevant. Compare user journey, value, effort (`S/M/L/XL`), and risk (`Low/Medium/High`).
3. **Converge scope with Occam's Razor:** Retain only Features that directly support the target outcome and behavior change. Record explicit exclusions, material assumptions, and one concrete **Next Action**.
4. **Gate — Confirm direction:** If multiple approaches remain viable or scope tradeoffs require a choice, follow the [clarification protocol](references/discovery-methods.md#clarification-protocol). Present the options, tradeoffs, and recommendation, then wait for the user's decision.
5. **Draft sections:** Complete **Approaches Considered** and **Recommended Approach** (**Recommendation**, **How It Works**, **Scope**, **Assumptions and Limits**, and **Next Action**).

### Step 3: Define Success and Specify Behavior

1. **Define Success Criteria (`SC<n>`):** Specify observable outcomes, pass conditions, guardrails, and measurement context using [Success Criteria rules](references/discovery-methods.md#define-success-criteria). For `Builder` goals, you may use an observable task completion.
2. **Specify Features (`F<n>`):** Write a **User Story** (`value → role → action`) linked to `SC<n>` for each Feature. Define testable **Rules** (`F<n>-AC<m>`) and **Key Examples** (`F<n>-E<m>`) for normal, boundary, and exception cases ([Specification by Example](references/discovery-methods.md#specify-features-by-example)).
3. **Gate — No invented policies:** Never invent business limits, thresholds, or expected outcomes. Link any unresolved rule or metric (`TBD`) to an open `Q<n>` record and ask the user.
4. **Save draft:** Apply [Technical Writing](../technical-writing/SKILL.md) to refine the prose. Save `product-design.md` with `Status: DRAFT` under the [document contract](references/document-contract.md#saving).

### Step 4: Run the Adversarial Review Loop (Max 3 Attempts)

1. **Review the draft:** Evaluate `product-design.md` and existing supporting files against [Product review](references/adversarial-review.md). If an independent reviewer is available, use that reviewer; otherwise perform a self-review and record the reason.
2. **Iterate up to 3 attempts:** Record findings (`R<n>`) in `product-design-review.md`.
   - If a finding requires a user decision or missing fact, pause the review loop. Ask the user through the [clarification protocol](references/discovery-methods.md#clarification-protocol).
   - If a finding can be fixed within agreed decisions, revise the document and verify the fix (up to 3 total attempts).
3. **Gate — Review exit:** When no approval blockers remain, set `Status` to `IN_REVIEW` under [status and approval rules](references/document-contract.md#status-and-approval). If blockers remain, keep `Status: DRAFT` and report the open items to the user.

### Step 5: Obtain Approval or Revise Baseline

1. **Request approval:** Present the `IN_REVIEW` Design Doc to the user for confirmation. Set `Status: APPROVED` only after explicit user confirmation, and record the [approval evidence](references/document-contract.md#versions-and-approval-evidence).
2. **Revise on feedback:** When new feedback or evidence challenges an existing baseline, preserve the prior version snapshot first. Then follow [baseline revision](references/discovery-methods.md#step-5-revisit-a-product-baseline).
