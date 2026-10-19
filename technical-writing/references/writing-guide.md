# Technical writing guide

Decide what readers need and in what order. For English, then apply the [English controls](english-controls.md).

Write in the language requested by the user or required by the project. Preserve the task's format, domain rules, approval state, decisions, conditions, exceptions, IDs, sources, units, and uncertainty. Clarify missing meaning instead of inventing facts to make a sentence complete.

## Write for the reader

Identify the reader's goal, existing knowledge, and missing knowledge. Select content that closes the gap. Distinguish the document's readers from the product's users. Explain unfamiliar concepts; link background that readers can consult separately. Avoid internal shorthand, idioms, and cultural references.

For a substantial draft, use a brief working outline:

- Who will read this, and what do they already know?
- What must they understand, decide, or do after reading?
- Which questions must the document answer to support that outcome?
- What is outside scope but could reasonably be expected here?

Use the answers to write the document; do not add a planning questionnaire to the deliverable. For a small edit, infer these answers from the surrounding text. State the relevant scope and prerequisites in the locations assigned by the template.

## Order explanations by need

Put the main point early. Introduce a concept before relying on it, and give prerequisites before the task that needs them. Add detail where it becomes useful. Use headings that help readers find a question, concept, or task.

Choose the order from the reader's purpose. These are patterns within the required format, not replacement templates:

| Reader's purpose | Useful order |
| --- | --- |
| Understand behavior | Main behavior → necessary concepts → concrete example → relevant limits |
| Complete a task | Goal and prerequisites → steps → expected result → supported recovery actions |
| Assess a proposal | Problem and proposal status → proposed behavior → evidence and tradeoffs → unresolved decisions |
| Find a reference detail | Stable name → meaning or contract → inputs and outputs → limits and examples |

Keep required headings, fields, and their order. Improve the explanation within those boundaries. Put optional background behind a link when it interrupts the reader's task. Do not move an exception away from the rule it limits.

For Skill instructions, address the agent performing the task. Keep routing in `SKILL.md` and detailed rules in references. Give each rule one authoritative location and link to it where needed.

## Compress content before sentences

First remove duplication and place detail at the reader's required scope. Then shorten sentences. Link existing evidence, history, and supporting detail instead of creating new documents by default. Keep current conclusions in place and preserve superseded records through accessible references.

Choose one primary representation for each fact or relationship. A diagram can replace a flow description; a table can replace repeated comparisons. Retain the rationale, conditions, exceptions, and uncertainty that the representation does not convey. Do not narrate every arrow or repeat a table in prose.

Keep table cells comparable and brief. Move narrative explanations to a nearby focused paragraph or linked record. Preserve the outcome and important limits in the visible summary. Group repeated qualifications where their scope remains clear; never remove an unknown or approval condition just to meet a length target.

## Lead each paragraph with its point

Begin with the behavior, result, problem, or decision that the paragraph explains. Follow with the reason or evidence needed to assess it. Keep one topic per paragraph and connect adjacent sentences. Remove preambles, tangents, promotional claims, and repeated recaps.

Prefer an explicit actor and a specific action. Replace vague claims such as “fast” or “easy” with supported measurements or observable behavior. When evidence is missing, retain the uncertainty or open question. Never invent a target to make a claim sound precise.

## Keep terms and references clear

Use one name for each concept. Define unfamiliar terms and acronyms where readers first need them, or link to the existing definition. Avoid new acronyms for terms used only a few times. Preserve proper names, UI labels, and exact identifiers.

Replace an ambiguous pronoun with its intended actor or object. Repeat the noun when several referents are possible. Distinguish different operations: structural validation, assumption validation, and user approval do not mean the same thing. If the source does not establish the distinction, flag the ambiguity instead of choosing a meaning.

## Keep sentences focused

Use four moves to keep sentences focused:

1. Split independent ideas when the sentence changes actor, stage, or topic.
2. Expose embedded sequences or alternatives as lists when that helps the reader.
3. Remove filler and replace indirect expressions with direct verbs.
4. Move side topics into separate sentences; retain clauses that restrict the rule.

Keep a condition with its action. Preserve causes, sequence, alternatives, and simultaneous actions when splitting. Retain “only,” “unless,” “at least,” negation, permission, obligation, and verification limits. These words carry meaning.

| Before | After | Meaning to retain |
| --- | --- | --- |
| When an import starts, the tool checks access, retrieves the document if access is allowed, and saves it after retrieval succeeds. | When an import starts, the tool checks access. If access is allowed, the tool retrieves the document. After retrieval succeeds, the tool saves the document. | Both gates and the action order |
| Files that exceed 10 MB are rejected. | Files larger than 10 MB are rejected. | The threshold excludes files of exactly 10 MB |
| The report, which the team uses in its weekly review, summarizes failed imports. | The report summarizes failed imports. The team uses the report in its weekly review. | The review detail remains available |

These examples illustrate edits; they do not introduce product requirements or claim STE compliance. Reread the passage after splitting so that it remains connected prose.

## Choose lists, tables, and examples deliberately

Use numbered steps when order matters, bullets for unordered items, and tables to compare the same attributes across cases. Keep list items parallel in grammar and detail. Give lists and tables context through a heading, field label, or brief introduction.

Keep a shared condition in the introduction so it applies to every item. State whether alternatives permit one choice or several. Do not turn “A or B” into steps that require both. Group long lists by topic when helpful; preserve required headers and columns. Do not delete rules or examples merely to shorten a table.

Place an example beside the explanation it supports. Use a simple case first, then a boundary or failure case when needed. Keep example terms and values consistent with the documented behavior. Mark hypothetical examples; do not present them as observed results. For code samples, give the necessary setup, input, and expected output. Verify executable samples when permitted; report samples that were not run.

## Keep evidence and visuals useful

State each fact or rule in its assigned location, then use a cross-reference or stable ID. Put source links beside the claims they support. Use descriptive link text and include a retrieval location for opaque IDs. Keep uncertainty, verification limits, and review history in their assigned fields; repeat only when needed to prevent misunderstanding.

For a user-visible failure, explain what failed and the available recovery action. Give a cause only when supported. Never turn “not verified” into success.

Use a diagram when it clarifies a relationship or flow. Place it beside the relevant text and explain its essential meaning there. Give informative images concise alt text; use empty alt text for decorative images.

## Edit in separate passes

Review in this order:

1. **Content and order:** Can readers find the information needed for their goal? Are prerequisites and concepts introduced before use? Apply the [content compression pass](#compress-content-before-sentences); keep each rule in its assigned location.
2. **Expression:** Check sentence focus, actors, references, examples, and list and table structure. For English, apply [English controls](english-controls.md), including the distinction between instructions and descriptions.
3. **Meaning:** Compare source and revision. Verify the same actors, actions, conditions, exceptions, sequence, alternatives, negation, limits, units, IDs, evidence, uncertainty, and approval state. A wording change cannot settle an unresolved decision.
4. **Reader walkthrough:** Follow a documented task or answer the document's main question using only the text and its stated prerequisites. Identify missing steps or unexplained terms. Treat this as a text review, not evidence that the product or procedure works.
