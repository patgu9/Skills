---
name: technical-writing
description: Use when the user asks to draft, rewrite, tighten, or review technical prose—such as design docs, requirements, API docs, READMEs, runbooks, or Skill instructions—or requests Google Technical Writing or ASD-STE100 style. Do not use for creative writing, marketing copy, or code-only changes.
---

# Technical Writing

## Goal

Produce clear, unambiguous, scan-friendly technical prose using **Google Technical Writing** (structure and paragraph focus) and an **80% ASD-STE100 adaptation** (controlled syntax and single-meaning vocabulary), while preserving 100% of the source's technical facts, logic, language, and required template.

## Hard Constraints

1. **Macro structure & paragraphs (Google Tech Writing):**
   - State scope, prerequisites, and **non-goals** early; define concepts before the steps that use them.
   - Start every paragraph with its **topic sentence** (state the conclusion, behavior, or rule in sentence 1).
   - Limit paragraphs to **≤ 6 sentences** in English (**≤ 4 sentences** in Chinese), covering one topic per paragraph.
   - Convert any sentence with **≥ 3 parallel items, branches, or steps** into a vertical list (introduced by a complete clause ending in `:`) or a comparison table.
   - Introduce diagrams and tables *before* showing them and state the key takeaway without narrating every arrow or cell.
   - Lock terminology: **one term per concept** (no synonym rotation). Spell out acronyms on first use, and **never introduce an acronym used fewer than 3 times**.
2. **Micro syntax & vocabulary (80% STE-100):**
   - **Instructions (Procedural):** Imperative verb, **1 action per sentence**, **condition first** (`If X, do Y`), **≤ 20 words** in English (**≤ 30 chars** in Chinese). Never put required actions inside `Note:` or `Tip:` blocks.
   - **System descriptions & requirements:** Active voice (**≥ 90%**), simple present tense, **≤ 25 words** in English (**≤ 45 chars** in Chinese). Requirements must keep explicit `Actor + must / must not / may + verb`.
   - **Noun clusters:** Max **3 consecutive nouns** in English (unpack longer clusters with `of`, `for`, `in`, `from`) or max **2 nested `的` modifiers** in Chinese.
   - **Language routing:**
     - For **English prose**, enforce the word replacements and grammar rules in [English controls](references/english-controls.md).
     - For **Chinese or other languages**, enforce the structural equivalents and dummy-verb removal in the [writing guide](references/writing-guide.md#chinese-and-cross-language-controls).

## Gotchas (Common Agent Mistakes)

1. **Corrupting logic to meet length targets:** Dropping `only` from `only if`, rewriting `> 10 MB` as ambiguous `exceeds / up to 10 MB` (or Chinese `超过 10 MB`), weakening `must` into a plain descriptive verb, or turning a `Proposal` / `Not verified` item into established fact. If a shorter rewrite alters meaning, keep the longer phrasing.
2. **Hallucinating an actor to fix passive voice:** Rewriting `The payload is validated` as `The gateway validates the payload` when the source never specified which component validates it. When the actor is unknown, retain passive voice and flag the ambiguity.
3. **Renaming code literals or UI labels:** Applying STE vocabulary replacements to code identifiers, CLI flags, config keys, file paths, or UI text (for example, changing `max_retry_attempts` to `max_retry_tries`). Keep exact identifiers untouched.
4. **Falling into STE lexical traps:**
   - Using `check` as a verb (`Check the logs` → use `Examine` or `Verify the logs`; in STE, `check` is a noun only, as in `run a health check`).
   - Using `since` or `as` to mean `because` (`since` is for time only; always use `because` for cause).
   - Using `while` to mean `although` (`while` is for simultaneous time only; use `although` or split sentences).
   - Starting a sentence with a naked pronoun (`This`, `It`, `That`) without its noun (`This prevents data loss` → `This lock prevents data loss`).
5. **Hiding required actions inside informational notes:** Putting a step the reader must execute inside a `Note:` or `Warning:` callout where skimmers miss it (violates STE Rule 5.5).
6. **Writing Chinese "officialese" (公文腔) and nested `的` chains:** Using empty dummy verbs (`对参数进行合法性校验的工作` → `校验参数合法性`), vague subjectless `被` clauses (`保存后将被重建` → `用户保存配置后，工作进程重建连接池`), or stacking 3+ `的` modifiers.
