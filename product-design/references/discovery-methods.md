# Discovery and specification workflow

Follow these methods in workflow order. The [document contract](document-contract.md) defines file paths, ID rules, and status transitions.

---

## Clarification protocol

When a missing fact, ambiguous term, or unmade decision affects the design across Steps 1–4, follow this protocol.

### Question types and states

| Question type | Purpose |
| --- | --- |
| `Exploration question` | Understand user experiences, triggers, workflows, and motives through neutral follow-up |
| `Fact to investigate` | Verify a claim from existing files or data, or track an assumption that needs validation |
| `User decision` | Obtain a choice or scope authorization after explaining options and tradeoffs |

| State | Meaning |
| --- | --- |
| `OPEN` | Identified, but not yet investigated or asked |
| `INVESTIGATING` | Gathering facts from available context |
| `WAITING` | Asked and awaiting the user's answer |
| `RESOLVED` | Answered by the user's account, verified evidence, or an explicit user decision |
| `UNKNOWN` | Evidence is unavailable, or the user answered “I don't know” or “skip” |
| `EXCLUDED` | The user agreed to remove the affected scope |

### Execution loop

1. **Investigate first:** Inspect existing domain docs (such as `CONTEXT.md`), code, and prior answers before asking the user. Never ask a question that available files already answer.
2. **Record `Q<n>`:** Assign each material unresolved question a stable `Q<n>` ID in `product-design-questions.md` under [question record rules](document-contract.md#question-records). Never renumber or reuse IDs.
3. **Select 1–3 questions per round:** Ask only questions whose prerequisites are resolved and whose state is not `WAITING`. Ask one question by default, and at most three mutually independent questions per turn. Pause dependent drafting while continuing independent work.
4. **Ask clearly:**
   - For **exploration**, ask neutral, concrete questions about real workflows or recent events.
   - For **decisions**, state the choice, product impact, options, tradeoffs, and your recommendation with its reason.
   - For **ambiguous terms**, test boundaries with concrete counterexamples (for example, `https://example.com/a` vs. `https://example.com/a/`).
   - Set asked questions to `WAITING`.
5. **Resolve and apply:** Record the answer, basis, and source. Recommendations, silence, and skipped questions are not decisions:
   - When **answered**, set the state to `RESOLVED` and update the affected sections in `product-design.md`.
   - When **skipped or unavailable**, set the state to `UNKNOWN` and mark dependent content `TBD (Q<n>)`. Propose either a validation step or a scope exclusion.
   - When the user agrees to **drop scope**, set the state to `EXCLUDED` and remove or defer the affected Feature or rule.
   - When a **prior decision changes**, preserve the earlier answer in `History`. Reopen dependent questions as `OPEN` and update affected sections.

---

## Step 1: Frame Context and Problem

### Mode: Startup vs. Builder

Select the mode that matches the user's goal:

- **`Startup` (Customer or internal adoption):** Focus on target-user evidence, current workarounds, switching friction, and measurable outcomes. Separate the idea owner's expectations from observed user behavior.
  - *No users yet:* Investigate the unmet need, current alternatives, and access to the first users.
  - *Existing users:* Investigate time-to-first-value, repeat usage, and adoption barriers.
  - *Internal or infrastructure:* Identify the workflow bottleneck and resource or adoption commitments.
- **`Builder` (Personal tools, learning, demos, open-source exploration, creative work):** Completion, personal utility, and learning are valid outcomes. Identify who will try the project, what makes it useful, the closest alternative, and the smallest usable result. Do not require market sizing, revenue models, or customer interviews.

### Uncover the real problem

When the situation, trigger, or desired outcome is unclear, anchor discovery in concrete events rather than abstract opinions:

1. **Trace a concrete case:** Ask what happened recently that triggered the idea. Identify the situation, goal, steps taken, obstacle, workaround, and consequence. Turn broad claims such as “often” or “slow” into a specific example.
2. **Distinguish need from solution:** Separate the user's problem from proposed features. For example, “I cannot tell which request is urgent” is a need; “add a dashboard” is a solution. Capture the underlying need in **Problem Statement** before comparing solutions.
3. **Separate evidence from hypotheses:** Distinguish observed behavior and past actions from stated interest, praise, or predictions. If a creative project has no past event, mark the scenario as hypothetical instead of inventing a pain point.
4. **Define value over the status quo (`What Makes This Cool`):** Explain why the direction matters compared with actual alternatives, including manual workarounds or doing nothing.

---

## Step 2: Explore Approaches and Converge Scope

### Connect goal → actor → behavior change → deliverable

Before listing Features, establish how the product creates value:

- **Goal:** Which problem or outcome (`SC<n>`) must improve?
- **Actor:** Which user or supporting role acts?
- **Behavior change or obstacle removed:** What can the actor do differently, faster, or more reliably?
- **Deliverable:** Which capability (`Feature`) enables that change?

Mark unproven causal links as hypotheses. If a proposed capability cannot explain which actor behavior it changes or which constraint it satisfies, challenge it during scope convergence.

### Compare approaches

For a new design or a material change in direction, compare at least two meaningful approaches in **Approaches Considered**:

- Start with differences in the user journey, trigger, or value delivery.
- Include the status quo or a minimal manual alternative when relevant.
- Compare technical options only when they materially affect user-visible behavior, constraints, or feasibility.
- State effort (`S/M/L/XL`), risk (`Low/Medium/High`), and estimate uncertainty. Never invent engineering precision to justify a choice.

For minor revisions within an agreed direction, reuse the existing comparison unless goals, constraints, or evidence changed.

### Converge scope with Occam's Razor

When coverage of agreed outcomes and constraints is comparable, prefer fewer assumptions, concepts, steps, exceptions, and dependencies:

1. **Justify every addition:** Each included Feature (`F<n>`) must support an agreed outcome or constraint. Propose deferring or excluding unsupported additions through the [clarification protocol](#clarification-protocol).
2. **Preserve essential paths:** Retain necessary failure handling, recovery actions, and boundary rules.
3. **Specify `How It Works`:** Write a numbered end-to-end workflow. For each step, state the trigger or actor, action, actor handoffs, observable result, and linked `SC<n>` and `F<n>` IDs.
4. **Surface assumptions and validation (`Assumptions and Limits` & `Next Action`):**
   - Identify the assumption (value, usability, or feasibility) whose failure would most change the decision.
   - Select a validation method that matches the uncertainty (such as workflow observation, prototype task, pilot trial, or controlled experiment). Record the validation plan in `product-design-questions.md` under [assumption validation rules](document-contract.md#assumption-validation).
   - Define one concrete **Next Action** with an observable result. For `Startup`, validate demand or a key assumption; for `Builder`, try a usable outcome.

---

## Step 3: Define Success and Specify Behavior

### Define Success Criteria

Select measures that represent delivered value rather than vanity activity:

- **Outcome and pass condition:** Define what success looks like in the `SC<n>` table. For quantitative goals, specify the metric (including rate numerator and denominator), baseline, target, units, eligible population, time window, and verification method.
- **Guardrails:** When optimizing the primary metric could harm another critical outcome (such as error rate or latency), add a separate guardrail `SC<n>` row.
- **Cadence and evidence:** Match the measurement window to the real task frequency. Never copy external benchmarks as targets without an explicit basis and user decision; link unknown baselines or targets to `Q<n>`.
- **Builder alternative:** For `Builder` projects, an observable task or working demonstration is a valid pass condition.

### Specify Features by Example

Translate each included Feature into testable requirements under [Feature rules](document-contract.md#feature-rules):

1. **User Story (`value → role → action`):**
   - Write `In order to <outcome/impact>, as a <role>, I want to <capability>`, and link defined `SC<n>` IDs.
2. **Business Rules (`F<n>-AC<m>`):**
   - State the condition, actor, required system behavior, units, and inclusive or exclusive boundaries. State exceptions separately.
3. **Key Examples (`F<n>-E<m>`):**
   - Use concrete cases to test and sharpen every rule.
   - *Boundary check:* For a 10-item limit, compare adding at 9 (count becomes 10) with adding at 10 (rejected, count stays 10).
   - *Normalization check:* Use concrete inputs to expose edge cases before writing general rules. Consolidate shared patterns instead of adding ad-hoc exceptions.
   - Never invent business thresholds or policies; link unresolved behaviors to `Q<n>`.
4. **AI product behavior (when applicable):**
   - When model variability affects the outcome, specify representative inputs, unacceptable outputs, and observable fallback or user-correction paths. Request evaluation evidence before promising accuracy targets; a single demo is insufficient.

---

## Step 5: Revisit a Product Baseline

When user feedback, constraints, or trial results challenge an existing Design Doc, follow these steps:

1. **Inspect inputs:** Read the current `product-design.md`, supporting files, and prior version snapshot under [version rules](document-contract.md#versions-and-approval-evidence). Identify the affected `SC<n>`, `F<n>`, `F<n>-AC<m>`, or `F<n>-E<m>` IDs.
2. **Reassess:** Compare the new evidence or constraint against the intended outcomes and guardrails. Reopen only decisions and rules whose basis changed; preserve unaffected decisions.
3. **Update and record:**
   - Before modifying a delivered version, save its snapshot and log the revision reason in `product-design-questions.md` (`Baseline and Feedback History`).
   - Run Steps 2–4 on the affected scope. If the same conflict recurs without new evidence or a viable alternative, present the options and consequences. Request an explicit user decision to revise, defer, or stop the affected scope.
