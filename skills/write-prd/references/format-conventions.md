# Format conventions — strict spec

**Canonical example**: Confluence 4609409051 — *Sample weighing and labeling function* (Suki Yuan, 2026-04-21).
Every formatting decision in this skill defers to that PRD. When in doubt, open it and copy the shape exactly.

This file is **authoritative** for Phase 4 drafting and Phase 4.7 review. The review-expert MUST flag any deviation as a finding.

> **Length & voice override** — these conventions are about **shape** (which tables, which column names, which punctuation). For **length and tone**, `voice-and-register.md` is the binding rule:
> - PRD body ≤ 250 lines / ≤ 6 Confluence pages
> - PM voice (no repo names, no service names, no field paths, no API jargon)
> - ≤ 3 Jira ticket references in the whole document
> - Per-table row caps: §5.1 FR ≤ 12 rows; §6.4 Edge Cases ≤ 8 items; §11.1 OQ ≤ 6 rows; §9.1 Deps ≤ 8 rows; §9.2 Risks ≤ 6 rows
> If shape and length conflict, length wins — cut content, don't add tables.

---

## 1 · Section grammar

### 1.1 Heading level

| Markdown | Used for | Tag |
|---|---|---|
| `#` | Top-level sections §1–§11 + `Appendix A`, `Appendix B` | Mandatory / Optional in fullwidth parens |
| `##` | Same as `#` when the doc is published as a sub-page; choose one and stay consistent | — |
| `###` | First-level subsection (e.g. `2.1`, `5.1`, `9.2`) | no tag |
| `####` | Second-level subsection / module split (e.g. `5.1.1 Module A — 前置准备系统`) | no tag |

### 1.2 Heading text format

```
# 1. Overview（Mandatory）
## 2. Background & Objective（Mandatory）
### 2.1 Business Problem / Opportunity
#### 5.1.1 Module A — 前置准备系统
## Appendix A — HZ 现有工具已知规则速查
```

Rules:
- **Number + dot + space + English title + fullwidth `（Mandatory）`/`（Optional）`** at top level. The Mandatory/Optional tag is required exactly as in the QIMA template.
- **Subsection numbering**: `2.1`, `2.2`, `5.1.1` — never `2.1.`, never roman.
- **Module/page/page-name titles** at `####` level use **em-dash `—` with single spaces around it** to attach a Chinese descriptor to an English label.
- **Appendix** uses `Appendix A`, `Appendix B` — NEVER `Appendix 1`.
- Mixed-language titles are correct and expected. English is the structural label; Chinese (when present) is the descriptive subtitle.

### 1.3 The 11 sections + appendix — exact titles, in order

```
1. Overview（Mandatory）
2. Background & Objective（Mandatory）
   2.1 Business Problem / Opportunity
   2.2 Primary Objective
   2.3 Why Now
3. Stakeholders（Mandatory）
4. User Stories / Use Cases（Mandatory）
   4.1 Target Users & Personas
   4.2 User Stories
5. Requirements（Mandatory）
   5.1 Functional Requirements and Priority
       5.1.1 Module A — {name}
       5.1.2 Module B — {name}
       5.1.3 Cross-cutting / Platform   (only if cross-cutting FRs exist)
   5.2 Out of Scope（v1 明确不做）
6. Design
   6.1 Page 1 — {name}
   6.2 Page 2 — {name}    (one §6.x per page/screen)
   6.3 Key Interaction Specs
   6.4 Edge Cases
7. Acceptance Criteria（Optional）
8. Analytics & Tracking（Mandatory）
   8.1 Events to Track
   8.2 Success Metrics
   8.3 Measurement Method
9. Dependencies & Risks（Optional —— 本 PRD 保留因风险较多）
   9.1 Dependencies
   9.2 Risks & Mitigations
10. Rollout & Release Plan（Mandatory）
    10.1 Phasing（建议）
    10.2 Beta / Pilot Plan
    10.3 Release Gates
11. Open Questions & Next Steps（Optional）
    11.1 Open Questions
    11.2 Next Steps

Appendix A — {name}
Appendix B — {name}
```

The `（Optional —— 本 PRD 保留因 X）` form on §9 is the canonical pattern for marking an Optional section that is being kept *with reason*. Use it whenever an Optional section is non-empty.

---

## 2 · Required tables — column shapes and headers

Every table below appears in the canonical PRD. Use the **exact column headers and order** shown.

| § | Table | Columns (left → right) |
|---|---|---|
| 1 | Overview meta | `字段` · `内容` |
| 3 | Stakeholders | `角色` · `姓名` · `职责` |
| 4.1 | Personas | `Persona` · `描述` · `在流程中的动作` |
| 5.1.x | Functional Requirements | `ID` · `功能` · `优先级` · `说明 / 备注` |
| 5.2 | Out of Scope | `Item` · `理由` |
| 6.3 | Key Interaction Specs | `元素` · `交互` · `行为` |
| 8.1 | Events to Track | `事件` · `触发时机` · `关键字段` |
| 9.1 | Dependencies | `Dep` · `说明` · `Owner` |
| 9.2 | Risks & Mitigations | `风险` · `影响` · `概率` · `Mitigation` |
| 11.1 | Open Questions | `#` · `问题` · `谁答` · `阻塞 v1？` |
| 11.2 | Next Steps | `Step` · `Owner` · `When` |

Per-table rules:
- **§1 Overview meta** must include the rows: `Document Owner`, `Date`, `Version`, `Target System`, `Phase`, `相关资料`. Field names bolded (`**Document Owner**`).
- **§5.1.x FR table** — `ID` cell holds bolded `**FR-A1**` form; `优先级` cell holds plain `P0` / `P1` / `P2` (no bold, no parens).
- **§5.1 priority block** — placed *immediately above* the first FR sub-section, in this exact form:
  ```
  **优先级说明**：

  * **P0** = MVP 必做，v1 上线前提
  * **P1** = 快速跟进，可在 v1 后一个 sprint 内补
  * **P2** = 架构预留 / 未来
  ```
- **§9.2 Risks** — `概率` cell uses `高` / `中` / `低` (single hanzi). No "High/Medium/Low" English.
- **§11.1 OQ** — `阻塞 v1？` cell uses `是 —— {reason / when to resolve}` (bolded `**是**` for blockers) or `否，但影响 {what}`. Never bare yes/no.
- **All tables** use markdown pipe syntax with header separator row. NEVER use HTML tables.
- **Empty cells** use `TBD` not blank — and `TBD` is plain, not styled.

---

## 3 · Inline formatting

### 3.1 Bold lead-in label pattern (USE EVERYWHERE)

Numbered/bulleted lists where each item makes a distinct point start with a **bold 2–6 character label** followed by `：`:

```
1. **数据孤岛**：BD working sheet 要从 Submission Folder 的 NAS 路径读 Excel...
2. **扩展性差**：工具只服务 HZ，多 Lab（上海 / 东莞 / Hamburg）无法复用...
3. **下游价值未释放**：称样数据没有进入 QIMAlabs，意味着...
4. **合规 / 审计风险**：称样结果是测试链路的起点...
```

This pattern is REQUIRED for §2.1 problem list, §6.4 Edge Cases, §10.3 Release Gates. Optional but encouraged elsewhere.

### 3.2 ID conventions (bolded)

| Item | Format | Example |
|---|---|---|
| Functional requirement | `**FR-{module-letter}{n}**` | `**FR-A1**`, `**FR-B12**`, `**FR-C3**` |
| User story | `**US-{n}**` | `**US-1**` |
| Acceptance criterion | `**AC-{n}（FR-X：{feature label}）**` | `**AC-1（FR-A5：包含关系合并）**` |
| Open question | `Q{n}` (plain, in `#` column of OQ table) | `Q1`, `Q2` |

IDs are bolded **only at definition site**. References in prose are plain text (`见 FR-A5`, `如 §5.2 所述`).

### 3.3 Code-style identifiers (backticks)

Wrap in backticks anything a developer would copy verbatim:
- DB columns / config-table fields: `parent_shortname`, `lab_scope`, `replicate_count`
- Analytics event names: `weigh.weight_captured`, `prep.export_version`
- Example values that are exact strings: `T-26031452-10-R`, `FRCHCC-PBT-CHCC_T25000001-100+200+300_ZP`

DO NOT backtick: PRD-internal terms (ShortName, Breakdown), system names (QIMAlabs, AIMS), generic English words.

### 3.4 User story syntax (REQUIRED)

```
**US-N**：As a **{role}**, I want to {action / capability}, so that {value}.
```

- Role bolded.
- Sentence form, single line, no nesting.
- Keep `As a ... I want to ... so that ...` template even when the prose body is Chinese — the *connective tissue* stays English template, the action and value can be Chinese.

### 3.5 Acceptance criterion syntax (REQUIRED)

```
**AC-N（FR-X：{feature label}）**

* Given {precondition}
* When {action}
* Then {observable result, with named field/threshold}
```

`Given / When / Then` are English keywords; the body can be Chinese. Each AC must reference a named FR ID in its header.

### 3.6 Metrics split (REQUIRED in §8.2)

```
**Leading（v1 上线后 30 天内）**：

* **{metric name}**：{target with operator and number, e.g. ≥ 95%}
* ...

**Lagging（上线后 3 个月）**：

* **{metric name}**：{target}
```

Bold metric names. Leading targets must include a number; Lagging may be a defined-but-unmetered behavior change (with the operator anyway, e.g. "下降 ≥ 30%").

### 3.7 Phasing (REQUIRED in §10.1)

Each phase is a `**Phase {Letter} — {name}**` paragraph followed by sub-bullets in this exact order:

```
**Phase A — Preparation 模块（Module A）**

* Target：{whom}
* Scope：{FR list}
* （optional）依赖：{prereqs}
* 估时：{honest estimate or "待 dev 评估"}
```

### 3.8 Release Gates (REQUIRED in §10.3)

Numbered list, ≥ 3 gates with distinct signers in fullwidth parens:

```
1. **Tech Gate**（Dev + QA）：{specific exit criteria, with a quantitative threshold}
2. **Business Gate**（{named SME / lab manager}）：{exit criteria}
3. **Data Gate**（Suki + Simple）：{exit criteria}
```

Each gate must name signers — `TBD` allowed if explicit.

---

## 4 · Bilingual policy

The canonical PRD mixes Chinese and English in a deliberate, repeatable way:

| Layer | Language | Rationale |
|---|---|---|
| Top-level section titles (§1–§11) | English | QIMA template / cross-team |
| `Mandatory` / `Optional` tag | English in fullwidth parens | Template-mandated |
| Subsection titles (`2.1`, `5.1.1`, …) | English head + optional `— Chinese` subtitle | Index legibility + business specificity |
| Prose / descriptions / problem statements | Chinese | PM's working language |
| FR / US / AC IDs | English code | Cross-system traceability |
| Domain nouns (ShortName, Breakdown, BD, ZP/ZT, CHCC, etc.) | English/code as established | Match production usage |
| System names (QIMAlabs, AIMS, NAS) | English | Match production usage |
| Punctuation between Chinese clauses | Chinese fullwidth `：` `，` `。` | Reader expectation |
| Punctuation between English clauses or after English label | Halfwidth `:` `,` `.` | Standard English |
| Lists, tables | bilingual freely; column headers can be Chinese (`角色`/`姓名`) or English (`Item`/`Owner`) — match the canonical PRD's choice per table | Pattern-match |

**Anti-pattern** — translating column headers between drafts (one PRD says `Owner`, another says `负责人`). Stay consistent with the canonical PRD's per-table choice.

---

## 5 · Punctuation & typography

| Rule | Right | Wrong |
|---|---|---|
| Mandatory tag | `# 1. Overview（Mandatory）` | `# 1. Overview (Mandatory)` |
| Module separator | `Module A — 前置准备系统` | `Module A: 前置准备系统` / `Module A - 前置准备系统` |
| Optional with reason | `（Optional —— 本 PRD 保留因风险较多）` | `(Optional - many risks)` |
| Label colon (Chinese label) | `**v1 成功标准**：HZ 化学称样组...` | `**v1 成功标准**: ...` |
| Label colon (English label) | `Target：HZ BD 主管...` (Chinese body OK) or `Owner: Suki` (English body) | mixed |
| Numeric ranges | `2 \~ 3 sprints`, `8.5 & < 9 → 12 months` | `2 to 3`, `2-3` |
| Comparison operators | `≥ 95%`, `≤ 30 分钟`, `< 8.5` | `>= 95%` |
| Arrows for transformation | `→` (e.g. `T- 前缀和 -10-R 后缀 → 26031452`) | `->` |
| Approx | `\~ 300` | `~300`, `约 300` |
| Italic closing line | `_文档结束。..._` | `**文档结束**` |

---

## 6 · §1 Overview meta-table — EXACT spec

```markdown
| 字段 | 内容 |
| --- | --- |
| **Document Owner** | {Name}（{Title}） |
| **Date** | YYYY-MM-DD |
| **Version** | v0.1（Draft — {what's pending}） |
| **Target System** | {QIMAlabs / QIMAone / etc.} |
| **Phase** | {QIMA program phase, e.g. Phase 2（Task Assignment / 仪器连接 / 自动报告）} |
| **相关资料** | {meeting names, doc links — semicolon-separated} |
```

Rules:
- Six rows, in this order, no extras unless the canonical PRD has them.
- Field names bolded.
- `Date` is ISO `YYYY-MM-DD`.
- `Version` always carries the bracketed status (`Draft — ...` / `Reviewed — ...`).

---

## 7 · §11.1 Open Questions — EXACT spec

```markdown
| # | 问题 | 谁答 | 阻塞 v1？ |
| --- | --- | --- | --- |
| Q1 | {question, prose} | {name(s)} | 否，但影响 {what} |
| Q2 | {question} | {name(s)} | **是 —— 建议在 dev kickoff 前完成** |
```

The blocker column has only two grammatical shapes:
- `否，但影响 {downstream impact}` — non-blocking
- `**是 —— {when/who must resolve}**` — blocking, bolded entirely

No bare `Yes` / `No` / `是` / `否`.

---

## 8 · Footer & marginalia

The canonical PRD ends with one italic line:

```
_文档结束。请 dev 在评估时按 FR-ID 拆分工作量并填入表格（Suki 会准备一个工作量收集表）。_
```

Match this shape — italic, single sentence or short paragraph, names a concrete next-action by the doc owner.

The horizontal rule `---` is used liberally between top-level sections and before appendices. Between subsections inside a section, no `---`.

---

## 9 · Validation checklist (used by Phase 4.7 review-expert)

Before sign-off, the review-expert verifies:

- [ ] All 11 sections present, in canonical order, with the exact titles from §1.3 above
- [ ] §1 meta-table has all 6 required rows
- [ ] Mandatory/Optional tags use fullwidth parens
- [ ] Every FR ID in `**FR-{letter}{n}**` form, table column order matches §2
- [ ] Priority block placed above §5.1 (not below, not inline)
- [ ] §5.2 OOS items each have a `理由` cell that is non-empty (Pattern 4 from prd-patterns-from-best.md)
- [ ] §6.3 Interaction table present whenever §6 has any UI component
- [ ] §6.4 Edge Cases lists ≥ 5 items in bold-lead-in format
- [ ] §8.1 events all use snake_case dotted form (`namespace.action`)
- [ ] §8.2 split into `**Leading（…）**` and `**Lagging（…）**` blocks with bold metric labels
- [ ] §9.2 risks table has all 4 columns; 概率 = 高/中/低
- [ ] §10.3 has ≥ 3 gates with distinct signers in fullwidth parens
- [ ] §11.1 OQ blocker column uses the two grammatical shapes from §7 (no bare yes/no)
- [ ] Footer is italic, names a concrete next action by the doc owner
- [ ] Code identifiers backticked; PRD-internal terms not backticked
- [ ] Bilingual punctuation rules from §5 obeyed throughout

Any failure = a finding. Format violations are at minimum **Medium** priority; structural omissions (missing section, wrong section title) are **High**.

---

## 10 · Anti-patterns

- ❌ HTML tables, nested tables, or grid-merged cells
- ❌ Translating canonical column headers (e.g. `负责人` instead of `Owner` in §11.2)
- ❌ Halfwidth parens around `Mandatory` / `Optional` tags
- ❌ Hyphen `-` instead of em-dash `—` in module/page titles
- ❌ Bare `Yes`/`No` in OQ blocker column
- ❌ Missing priority block above §5.1
- ❌ FR table without §5.1.x module split when ≥ 8 FRs (canonical PRD splits at this threshold)
- ❌ §6 with prose only, no Interaction Specs table
- ❌ §9.2 with `High/Medium/Low` in 概率 column
- ❌ Inventing new section titles or numbering (`§5.3 Performance`, `§12 ROVO`)
- ❌ §1 meta-table missing `相关资料` row (this is the link-trail to source meetings)
