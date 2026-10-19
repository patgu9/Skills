## Design Doc : $TITLE$

- Status: DRAFT
- Version: v1
- Approval: Pending
- Mode: $Startup or Builder$
- Date: $YYYY-MM-DD$
- Stage: Think

- **Supporting Records:** $Relative links to product-design-questions.md and product-design-review.md when they exist; otherwise mark each as Not started.$

<!-- Follow the [document contract](../references/document-contract.md) for saving, structure, versions, and approval. Use [Technical Writing](../../technical-writing/SKILL.md) for wording. Replace placeholders and remove comments. Omit only optional fields. -->

### Glossary

<!-- Step 1: Define unfamiliar domain terms and abbreviations. Keep one term per concept. -->

| Term | Definition |
|-----|-----|
| $Domain term or unfamiliar abbreviation$ | $Meaning and boundaries in this design$ |

### Background

#### Problem Statement

$State the actor, target segment, situation, and selected unmet need or aspiration. Explain the desired outcome and any relevant workflow, workaround, and consequences. Include the context readers need to assess this choice.$

- **Evidence:** $Describe reported experience, observations, or data. Link sources. Distinguish stated intent and agent inference. Mark hypothetical cases and missing evidence.$
- **Constraints (optional):** $State time, resource, platform, or business limits that affect the decision.$

#### What Makes This Cool

$Describe the value compared with actual alternatives, including the current approach. For Startup: concrete benefits and relevant differentiation. For Builder: an experience worth trying. Mark untested claims.$

### Solution Design

#### Approaches Considered

<!-- Step 2: Compare at least two meaningful ways to achieve the same goal. Follow [approach comparison](../references/discovery-methods.md#compare-approaches). -->

| Approach | Core Idea and Benefits | Main Costs and Risks |
|-----|-----|-----|
| A: $Way to achieve the user goal$ | $Describe the user journey, trigger, behavior change, value, and reuse$ | $Effort: S/M/L/XL. Risk: Low/Medium/High. Drawbacks. If not selected: reason$ |
| B: $Different way to achieve the same goal$ | $Describe the different user journey, trigger, behavior change, value, and reuse$ | $Effort: S/M/L/XL. Risk: Low/Medium/High. Drawbacks. If not selected: reason$ |

#### Recommended Approach

**Recommendation:** $Name the chosen approach. Explain why it serves the goal, the relevant strategic tradeoff, and retained complexity. If the decision is unresolved, mark it as pending.$

**How It Works:** $Number the end-to-end workflow steps. For each step, name the actor, action, and observable result. Include the trigger, handoffs between actors, how the product reaches users, and shared dependencies where relevant. Link SC and Feature IDs.$

**Scope:** $State the initial audience and smallest useful outcome. List included Feature IDs. State exclusions or deferrals and their reasons. Include the costs of future changes where relevant.$

**Assumptions and Limits:**

$State only current premises, material assumptions, and limits needed to understand this design. State unresolved product effects and approval blockers briefly, with links to Q or R records. Use None if there are no material assumptions or limits.$

**Next Action:** $Give one concrete action and its observable result in one short sentence. For Startup: validate demand or a critical assumption. For Builder: try a usable outcome. Recommend the action without implementing it.$

#### Success Criteria

<!-- Step 3: Follow [define Success Criteria](../references/discovery-methods.md#define-success-criteria). Builder may use an observable task or demonstration instead of numerical targets. -->

| ID | Desired Outcome and Pass Condition | Measurement Context and Method |
|-----|-----|-----|
| SC1 | $State the outcome and pass condition. For quantitative goals: metric definition, baseline, target, and units. Link TBDs to open questions$ | $State the observed population, time window, and verification method. Explain how to obtain missing baselines$ |

### Requirements

<!-- Step 3: Repeat Features with stable IDs. Follow [Feature rules](../references/document-contract.md#feature-rules) for User Story order, rule coverage, boundaries, exceptions, and examples. -->

#### Feature 1 — $Capability Name$

##### User Story

> In order to $achieve a specific value or behavioral outcome$,
> as a $specific role$,
> I want to $perform a specific capability$.

- **Related Success Criteria:** $Defined SC IDs.$
- **Boundaries and Dependencies (optional):** $Limits or prerequisites for this Feature.$

##### Rules

- **F1-AC1:** $State the condition, actor, and required behavior. State exceptions separately. Give units where relevant. State whether boundaries are inclusive or exclusive where relevant.$

##### Key Examples

| Example | Related Rule | Given: Context / Input | When: Action / Event | Then: Expected Outcome |
|-----|-----|-----|-----|-----|
| F1-E1: $Scenario name$ | F1-AC1 | $Concrete data and state$ | $Business action$ | $Observable outcome$ |
| F1-E2: $Boundary or exception$ | F1-AC1 | $Facts that establish the boundary$ | $Business action$ | $Observable outcome and what stays unchanged where relevant$ |
