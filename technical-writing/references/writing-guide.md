# Technical Writing Guide (Structure & Cross-Language Controls)

Use these structural patterns and rewrite rules alongside [English controls](english-controls.md). Preserve 100% of the source's technical meaning, conditions, thresholds, IDs, unknowns, and approval status.

## Order by reader purpose

Keep the document's required template and headings. Within each section, order content so prerequisites and definitions appear before the rules or steps that use them:

| Reader's purpose | Progression |
| --- | --- |
| **Understand behavior** | Main behavior → required concepts → concrete example → operational limits |
| **Complete a task** | Goal and prerequisites → numbered steps → expected result → recovery actions |
| **Assess a proposal** | Problem and proposal status → proposed behavior → tradeoffs and evidence → open decisions |
| **Find a reference detail** | Exact name → contract or meaning → inputs and outputs → limits and example |

For Skill instructions, keep routing, goals, hard constraints, and gotchas in `SKILL.md`; place lookup tables and detailed reference rules in `references/`. Give each rule one authoritative location.

## Compress content and choose representations

Remove duplication before editing sentences:

- **One representation per fact:** Use a **table** to compare identical attributes across cases, a **diagram** to show flows or state transitions, and **prose** to state rules, conditions, and exceptions.
- **Introduce before showing:** Precede every diagram, table, or code sample with a sentence that states its main takeaway. Do not narrate every arrow or repeat every table row in prose.
- **Keep exceptions attached:** Place every exception or boundary condition directly beside the rule it limits.

## Sentence focus and structural rewrites

Split sentences when the actor, stage, or topic changes. Keep conditions attached to the actions they govern:

| Before | After | Why it improves clarity |
| --- | --- | --- |
| When an import starts, the tool checks access, retrieves the document if access is allowed, and saves it after retrieval succeeds. | When an import starts, the tool verifies access. If access is allowed, the tool retrieves the document. After retrieval succeeds, the tool saves the document. | Separates three stages, removes `check` as a verb, and puts each gate before its action. |
| Files that exceed 10 MB are rejected by the gateway. | The gateway rejects files larger than 10 MB. | Uses active voice and states the exact boundary (`> 10 MB`, excluding 10 MB). |
| The report, which the team uses in its weekly review, summarizes failed imports. | The report summarizes failed imports. The team uses this report in its weekly review. | Splits a non-essential relative clause into a standalone sentence. |
| To deploy, build the image, push it to the registry, and updating the manifest is also required. | To deploy the service:<br>1. Build the container image.<br>2. Push the image to the registry.<br>3. Update the deployment manifest. | Converts 3+ embedded steps into a numbered list with parallel imperative verbs. |

## Chinese and cross-language controls

When writing in Chinese (中文) or another non-English language, do not apply English word counts or morphological rules. Enforce these structural equivalents instead:

| Dimension | Hard constraint (中文输出规范) | Avoid (反例) | Preferred (正例) |
| --- | --- | --- | --- |
| **Dummy verbs (消灭虚化动词)** | Delete bureaucratic dummy verbs (`进行`, `加以`, `予以`, `实现`, `完成`, `开展`, `做出`) before action nouns; use the verb directly. | 系统对请求参数**进行合法性校验**，并**完成日志的记录**。 | 系统**校验**请求参数合法性，并**记录**日志。 |
| **Explicit actor (显式主语与主动语态)** | Avoid subjectless clauses and vague `被` passives that hide which component or user acts. | 配置文件保存后，连接池**将被重建**。 | 用户保存配置文件后，工作进程**重建**连接池。 |
| **Modifier depth (拆解多层“的”字长定语)** | Limit chained `的` modifiers to **≤ 2 levels** (equivalent to STE's 3-noun cluster limit). Move qualifiers into clauses or parentheses. | 用于处理来自未认证客户端的并发重连请求的限流器默认阈值 | 限流器的默认阈值（针对未认证客户端的并发重连请求） |
| **Condition first (条件永远前置)** | Place preconditions (`如果……，`, `当……时，`, `仅当……时，`) before the command or system result. | 请清理本地缓存，如果校验和比对失败。 | **如果**校验和比对失败，**请清理**本地缓存。 |
| **Exact bounds (精确边界与逻辑词)** | Replace ambiguous bounds (`超过`, `以内`, `左右`) with explicit operators (`大于` `> 10 MB`, `不少于` `≥ 10 MB`, `约`). Lock `因为` (cause), `如果` (condition), and `仅当` (`only if`). | 文件大小**超过** 10 MB 时不予处理。 | 文件**大于 10 MB（`> 10 MB`）**时，网关拒绝该请求。 |
| **Length limits (句长与段落上限)** | Keep instructions **≤ 30 Chinese chars** (1 action/sentence), descriptions **≤ 45 chars**, and paragraphs **≤ 4 sentences** (topic sentence first). | 一句话内堆叠三四个无主语逗号分句和多重转折。 | 拆分为单句单动作短句；包含 ≥ 3 项时转为垂直列表。 |
