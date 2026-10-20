# English Expression Controls (80% ASD-STE100 + Google Tech Writing)

Apply these sentence and vocabulary controls after the [writing guide](writing-guide.md) establishes document structure and paragraph order.

## Define the 80% STE-100 boundary

Full ASD-STE100 targets aerospace maintenance manuals and bans everyday software verbs (such as `configure` or `validate`). This Skill enforces an **80% STE-100 software adaptation** that captures maximum clarity without crippling software terminology:

- **Enforce 100% of STE-100 structural and syntactic rules (the 80% clarity gain):** Apply strict sentence length limits, paragraph limits, maximum 3-word noun clusters, condition-first ordering, one instruction per sentence, active voice, present tense, and one meaning per word.
- **Exempt standard software primitives (the 20% domain adaptation):**
  1. Preserve exact code identifiers, CLI commands, file paths, API fields, UI labels, and direct quotations. Wrap code tokens in backticks (`` `...` ``).
  2. Allow standard software verbs with a single technical meaning: `authenticate`, `authorize`, `build`, `compile`, `configure`, `deploy`, `encrypt`, `hash`, `index`, `initialize`, `log`, `mount`, `parse`, `publish`, `query`, `render`, `retry`, `route`, `schedule`, `serialize`, `sync`, `validate`, and `verify`.

If a user explicitly requests 100% strict aerospace STE-100 compliance, apply only the official STE dictionary and flag any unverified domain terms.

## Classify passages and enforce sentence limits

Classify each passage by its communicative role and enforce the corresponding STE-100 mood and length limits. Count a code literal, file path, or URL as 1 word.

| Passage type | Mood, voice, and tense | Hard limits (STE Rules) | Example |
| --- | --- | --- | --- |
| **Instruction to reader (Procedural)** | Imperative verb (`Run`, `Set`, `Delete`). Address the reader directly. | **≤ 20 words** per sentence (Rule 5.1).<br>**1 action** per sentence (Rule 5.2). | "If the checksum fails, delete the local archive." |
| **System behavior (Descriptive)** | Active voice, **simple present tense** (`reads`, `rejects`, `sends`). Avoid `will` for deterministic behavior. | **≤ 25 words** per sentence (Rule 6.3).<br>**≤ 6 sentences** per paragraph (Rule 6.6). | "The worker deletes expired session tokens every 15 minutes." |
| **Requirement (Obligation)** | Explicit actor + controlled modal (`must`, `must not`, `may`) + active verb. | **≤ 25 words** per sentence. Preserve exact modal force. | "The API gateway must reject payloads larger than 5 MB." |
| **Proposal or open question** | Explicit status prefix (`Proposal:`, `Open question:`, `Not verified:`). | Do not state unapproved proposals as established system behavior. | "Proposal: retain failed jobs in the dead-letter queue for 7 days." |

Follow four mandatory procedural rules (STE Section 5):

1. **One instruction per sentence (Rules 5.2–5.3):** Give only one command per sentence, unless two actions must happen simultaneously (connected by `and` or `at the same time`, such as "Press and hold the reset button").
2. **Condition first (Rule 5.4):** Start the sentence with the condition (`If...`, `When...`, `Before...`) before stating the command, so the reader sees the gate before acting.
3. **No instructions inside notes (Rule 5.5):** Never hide a required action inside a `Note:` or `Tip:` callout. Notes give information only; put actions in numbered steps.
4. **Retain a longer sentence only for safety of meaning:** If splitting a 26-word sentence would sever a restrictive condition or corrupt a threshold, keep it intact or convert its branches into a vertical list.

## Enforce explicit grammar and unpack noun clusters

### 1. Limit noun clusters to at most 3 words (STE Rules 2.1–2.2)

Never stack more than **3 consecutive nouns** (or modifiers acting as nouns) unless they form an official proper name. Unpack dense clusters with prepositions (`of`, `for`, `in`, `from`, `to`) or a relative clause.

| Avoid (> 3 words in cluster) | Preferred (≤ 3 words per cluster) |
| --- | --- |
| `default user session timeout configuration value` (6 words) | `default timeout value for user sessions` |
| `failed background import job retry limit` (6 words) | `retry limit for failed background imports` |
| `client certificate revocation list verification error` (6 words) | `verification error for the client certificate revocation list` |

### 2. Use active voice and explicit actors (STE Rules 3.6, 6.2)

Write at least **90% of sentences in active voice**. When you encounter a passive verb (`is validated`, `was rejected`, `are retried`), identify who performs the action and make that actor the grammatical subject. Use passive voice only when the actor is genuinely unknown or irrelevant, and flag ambiguity if the source text omits a required actor.

### 3. Eliminate zombie nouns (nominalizations) and ambiguous `-ing` forms (STE Rules 3.4–3.5)

Replace weak verbs (`perform`, `make`, `conduct`, `take`, `be`, `occur`) paired with abstract nouns by using a strong finite verb. Avoid dangling `-ing` participle clauses that obscure the subject or timing.

| Unclear, passive, or nominalized | Clear, active, and explicit |
| --- | --- |
| After saving the file, it is checked. | After the editor saves the file, the validator verifies the file. |
| Processing large files can cause a delay in shutdown. | The service can delay shutdown while it processes large files. |
| The module performs a validation of the token. | The module validates the token. |
| Allocation of memory takes place during startup. | The runtime allocates memory during startup. |
| In the event that retrieval fails, send an alert to the owner. | If retrieval fails, notify the owner. |

### 4. Anchor pronouns and distinguish `that` vs. `which`

- **No naked demonstrative pronouns:** Do not start a sentence with a standalone `This`, `It`, `That`, or `These` when the referent could be a whole clause or multiple nouns. Attach the noun explicitly: write `This timeout prevents deadlocks` instead of `This prevents deadlocks`.
- **Restrictive `that` vs. non-restrictive `, which`:** Use `that` (without commas) for essential restrictions that narrow the set (`Jobs that fail three times move to the dead-letter queue`). Use `, which` (with commas) only for non-essential side information, or split the side information into a second sentence.

## Replace unapproved words with controlled vocabulary

Enforce **one word, one meaning, and one part of speech** (STE Section 1). Replace verbose, literary, or multi-meaning words on the left with the controlled STE-adapted equivalents on the right:

### 1. Verbs and action phrases

| Avoid (Unapproved or verbose) | Use instead (Controlled) | Rule and part-of-speech note |
| --- | --- | --- |
| `utilize`, `employ`, `leverage`, `make use of` | **`use`** (v.) | Never use `utilize` or `leverage`. |
| `perform`, `execute`, `carry out`, `conduct` + *noun* | **Direct verb** or **`run` / `do`** | `perform a backup` → `back up`; `execute the command` → `run the command`. |
| `ensure`, `assure`, `make certain` | **`make sure`** (or **`verify`** for tests) | Use `make sure` in general prose and instructions. |
| `check` (as a verb: *check the logs*) | **`examine`**, **`read`**, **`verify`**, or **`make sure`** | In STE, **`check` is a noun only** (`run a health check`), never a verb. |
| `initiate`, `commence`, `begin`, `launch` | **`start`** (v.) | Pair consistently with `stop`. |
| `terminate`, `cease`, `abort`, `halt`, `end` | **`stop`** (v.) | Preserve exact OS signal names like `SIGTERM` or `abort()`. |
| `modify`, `alter`, `adjust`, `amend` | **`change`** (v.) | Keep `change` as the single general verb for modifications. |
| `attempt`, `endeavor`, `strive` | **`try`** (v.) | Write `try to reconnect`, not `attempt a reconnection`. |
| `assist`, `aid`, `facilitate`, `enable` (vague) | **`help`** (v.) or state exact action | Replace vague `facilitates` with what the system actually does. |
| `indicate`, `denote`, `demonstrate`, `illustrate`, `evince` | **`show`** (v.) | Example: `The status code shows why the request failed.` |
| `obtain`, `acquire`, `procure`, `fetch` (non-API) | **`get`** (v.) | Retain `retrieve` or `fetch` only when matching an exact API name. |
| `provide`, `supply`, `furnish`, `afford` | **`give`**, **`send`**, **`return`**, or **`include`** | Choose the concrete action instead of generic `provide`. |
| `eliminate`, `discard`, `expunge`, `purge` (general) | **`remove`** or **`delete`** | Distinguish `remove` (detach from list/config) from `delete` (erase data). |
| `encounter`, `experience` (errors) | **`have`** or **`get`** (or rewrite actively) | `If you encounter an error` → `If an error occurs` or `If you get an error`. |

### 2. Connectors, prepositions, and modifiers

| Avoid (Ambiguous or wordy) | Use instead (Controlled) | Rule and semantic lock |
| --- | --- | --- |
| `since` or `as` (meaning *because*) | **`because`** | **Strict lock:** Use `since` ONLY for time ("since 2024"). Use `because` for cause. |
| `while` or `whilst` (meaning *although* / *whereas*) | **`although`** (or split into 2 sentences) | **Strict lock:** Use `while` ONLY for simultaneous time ("while the job runs"). |
| `due to the fact that`, `owing to`, `on account of` | **`because`** | Replace multi-word causal prepositions with a `because` clause. |
| `in order to`, `so as to`, `with the aim of` | **`to`** | Write `to reduce latency`, not `in order to reduce latency`. |
| `in the event that`, `in case of`, `should` (conditional) | **`if`** | Write `If the node crashes`, not `Should the node crash`. |
| `prior to`, `in advance of`, `ahead of` | **`before`** | Use `before` for all prior-time and sequence relations. |
| `subsequent to`, `following` (meaning *after*) | **`after`** | Never use `following` as a time preposition (`after the reboot`, not `following the reboot`). |
| `via`, `by means of`, `through the use of` | **`by`**, **`through`**, or **`with`** | Use `by` (method), `through` (channel/tunnel), or `with` (tool/flag). |
| `additional`, `further`, `supplementary` | **`more`** or **`other`** | Write `more nodes`, not `additional nodes`. |
| `sufficient`, `adequate` | **`enough`** | Write `enough disk space`, not `sufficient disk space`. |
| `approximately`, `roughly`, `around` | **`about`** | Write `about 30 seconds`. |
| `numerous`, `a large number of`, `multiple` | **`many`** or **`several`** (or exact count) | Prefer exact counts (`3 retries`); otherwise use `many` or `several`. |
| `at this point in time`, `currently`, `presently` | **`now`** | Or omit entirely when simple present tense already shows current behavior. |

## Preserve logical force and modal precision

Treat modal verbs, quantifiers, and logical connectors as semantic contracts, never as stylistic variations:

- **`must` / `must not`:** Mandatory obligation or prohibition. Never substitute `shall`, `have to`, `need to`, or `is required to` when stating a formal requirement.
- **`should` / `should not`:** Strong recommendation with valid exceptions. In strict specifications, clarify whether the rule is actually `must` or `may`.
- **`may`:** Permission (`is allowed to`). Never use `may` to mean "might possibly happen" in a requirement; use `can` or `might` for possibility.
- **`can`:** Capability or objective possibility (`is able to`).
- **`only if` vs. `if`:** `only if` states a necessary condition; replacing it with `if` reverses or weakens the rule.
- **Exact timing (`before`, `after`, `until`, `while`):** Preserve exact temporal boundaries across sentence splits.
- **Exact numeric bounds:** Prefer explicit comparison phrases (`larger than 10 MB` / `> 10 MB`, `at least 10 MB` / `≥ 10 MB`, `10 MB or smaller` / `≤ 10 MB`) over ambiguous words like `exceeds`, `up to`, or `over`.
