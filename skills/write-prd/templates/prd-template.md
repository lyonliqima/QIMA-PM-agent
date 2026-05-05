# PRD Template — QIMA Standard (Draft version)

Extracted from `qima-prd-writing-guide` and adapted for the write-prd skill. **Length budget: ≤ 250 lines body / ≤ 6 Confluence pages.** Anything technical goes in Appendix or stays in the Tech Design page.

---

## How to use this template

**Placeholders** — replace these tokens verbatim:

- `{{FIELD}}` — single-value placeholder (fill or delete the line)
- `{{LIST:item-kind}}` — repeat the row/bullet once per item
- `⚠️ Open question — <text>` — unresolved item surfaced in Checkpoint A but not blocking draft
- `<!-- IMG:filename.png -->` — Figma image marker; replaced in Phase 4 (see figma-handling.md)

**Voice rules (from `voice-and-register.md`, hard gate)**:

- PM voice. No repo names, no service names, no API paths, no field names, no commit / branch / PR, no "killswitch" / "ETag" / "CDN" / "snake_case event".
- ≤ 3 Jira ticket references in the whole document, all in §1 or Appendix.
- Stakeholders: team + lead, NOT repo list.
- If technical detail is required, link to Tech Design or move to Appendix · For engineering reference.

**Formatting** — this template renders as Confluence Cloud content:

- Use Markdown headings (`#`, `##`, `###`)
- Use markdown tables (pipes), NOT HTML tables (Confluence renders both, but markdown is shorter)
- Paragraphs ≤ 3 lines each
- Inline links: `[label](url)` — NOT bare URLs
- No decorative emojis beyond ⚠️ for Open questions
- No border-left callouts, no gradient headings

**Empty-section policy** — if a section truly has no content, write:

> *Not applicable for this release — reason: {{REASON}}.*

Don't delete the heading; reviewers rely on section order being stable.

---

## Template body starts below

```markdown
# 1. Overview（Mandatory）

| 字段 | 内容 |
| --- | --- |
| **Document Owner** | {{PM_NAME}}（{{TITLE}}） |
| **Date** | {{YYYY-MM-DD}} |
| **Version** | v0.1（Draft — {{what's pending}}） |
| **Target System** | {{myQIMA / QIMAlabs / QSP / etc.}} |
| **Phase** | {{e.g. Phase 1 — Inspection 在线报告重构}} |
| **相关资料** | {{≤ 6 links: Tech Design / Figma / 主要 UX research / Prototype / Epic}} |

One paragraph (3–5 sentences): **what** is being built, **for whom**, **why now**. A reader who only reads this paragraph should understand the essence.

---

# 2. Background & Objective（Mandatory）

## 2.1 Business Problem / Opportunity

3 bold-lead-in paragraphs (≤ 3 lines each), each citing 1 source:

1. **{{Pain 1 short label}}**：{{evidence + 1-line implication}}
2. **{{Pain 2 short label}}**：{{evidence + 1-line implication}}
3. **{{Pain 3 short label}}**：{{evidence + 1-line implication}}

## 2.2 Primary Objective

- **North Star（Lagging）**：{{e.g. 客户 NPS 提升}}
- **Leading proxy（30 天内）**：3–4 数字目标，每条 1 行

## 2.3 Why Now

3–4 bullets — design ready / data signals / dependency timing / competitive.

---

# 3. Stakeholders（Mandatory）

| 角色 | 姓名 | 职责 |
| --- | --- | --- |
| Product Owner | {{PM}} | {{1 line}} |
| Engineering Lead | {{Eng Lead}} | {{1 line}} |
| Design Lead | {{Designer}} | {{1 line}} |
| QA Lead | {{QA}} | {{1 line}} |
| Sponsor / Stakeholder | {{Name}} | {{1 line}} |

**Rule**: ≤ 8 rows. NOT a list of repos / services per person. Name + role + 1 sentence responsibility.

---

# 4. User Stories / Use Cases（Mandatory）

## 4.1 Target Users & Personas

| Persona | 描述（1 line） | 在流程中的动作（1 line） |
| --- | --- | --- |

≤ 5 personas.

## 4.2 User Stories

≤ 7 stories. Format:

> **US-N**：As a **{role}**, I want to {action}, so that {value}.

---

# 5. Requirements（Mandatory）

**优先级说明**：

- **P0** = MVP 必做，v1 上线前提
- **P1** = 快速跟进，v1 后一个 sprint 内补
- **P2** = 架构预留 / 未来

## 5.1 Functional Requirements and Priority

≤ 12 rows total. If you have more, you're writing a dev spec — go back and group.

| ID | 功能 | 优先级 | 说明 / 备注 |
| --- | --- | --- | --- |
| **FR-1** | {{1-line功能名}} | P0 | {{≤ 2 sentences. 描述客户看到什么 / 能做什么。NOT 描述 API 或字段}} |

If FRs naturally group into 2–3 modules, use sub-headings `### 5.1.1 Module A — {name}` etc., but keep the table within each module ≤ 6 rows.

## 5.2 Out of Scope（v1 明确不做）

| Item | 理由（1 line） |
| --- | --- |

≤ 8 rows. Each row = 1 deferred / excluded item + reason.

---

# 6. Design

> 所有 §6 frame 链接均锁定在 Figma section [{{section-name}}]({{section-URL}}) 内（在 Phase 0 intake 时由 PM 提供；frame 搜索范围限定于此 section，不全局搜索）。

## 6.1 Page 1 — {{name}}

≤ 3 sentences description.

> **Figma frame**: [{{page-1-name}}]({{full Figma URL with ?node-id=<frame-id>}})

{{full Figma URL on its own line — Figma for Confluence plugin auto-detects and renders as inline live embed}}

**Rule** — Each `## 6.x Page N` MUST carry **two anchors**:

1. A `> **Figma frame**:` line with the **deep-link** (text form) — fallback if the Figma plugin macro fails to render
2. **The same URL on its own line directly underneath** — this is what the Figma for Confluence plugin pattern-matches to render the inline live frame embed

The frame node-id must come from inside the user-provided Figma **section** (recorded above). Never link to the file root; never use a node from a different section. If a node-id can't be resolved within the section, write `> **Figma frame**: ⚠️ TBD — not in section; ask design lead` and add to §11.1 OQ.

## 6.2 Page 2 — {{name}}

> **Figma frame**: [{{page-2-name}}]({{Figma URL with ?node-id=...}})

{{Figma URL on its own line}}

(repeat per page; ≤ 4 pages total)

## 6.3 Key Interaction Specs

| 元素 | 交互 | 行为 |
| --- | --- | --- |

≤ 10 rows.

## 6.4 Edge Cases

≤ 8 bold-lead-in items, each ≤ 1 sentence.

1. **{{label}}**：{{behavior}}

---

# 7. Acceptance Criteria（Optional — keep if PM wants explicit pass/fail）

≤ 1 AC per FR. Format:

> **AC-N（FR-X：{{label}}）**
> - Given {{precondition}}
> - When {{action}}
> - Then {{observable result}}

---

# 8. Analytics & Tracking（Mandatory）

## 8.1 Events to Track

| 事件 | 触发时机 | 关键字段（业务字段名，NOT snake_case payload） |
| --- | --- | --- |

≤ 12 rows.

## 8.2 Success Metrics

**Leading（30 天内）**：

- **{{metric}}**：{{target with number, e.g. ≥ 60%}}
- ≤ 4 items

**Lagging（3 个月）**：

- **{{metric}}**：{{target}}
- ≤ 3 items

## 8.3 Measurement Method

≤ 4 sentences: 数据从哪来 / 仪表盘谁建 / 复盘节奏。

---

# 9. Dependencies & Risks（Optional — 视项目复杂度保留）

## 9.1 Dependencies

| Dep | 说明（1 line） | Owner |
| --- | --- | --- |

≤ 8 rows. Use **bucket names** (Frontend / Backend / Mail / Legal / BI / Platform), NOT repo lists.

## 9.2 Risks & Mitigations

| 风险 | 影响 | 概率 | Mitigation |
| --- | --- | --- | --- |

≤ 6 rows. 概率 = 高 / 中 / 低（single hanzi, NOT High / Medium / Low）.

---

# 10. Rollout & Release Plan（Mandatory）

## 10.1 Phasing（建议）

**Phase A — {{name}}**

- Target：{{whom}}
- Scope：{{FR list, by ID}}
- 估时：{{honest estimate or 待 dev 评估}}

(repeat for Phase B, C; usually 2–3 phases max)

## 10.2 Beta / Pilot Plan

≤ 5 numbered steps from internal dogfood → GA.

## 10.3 Release Gates

3 gates with **named signers**:

1. **Tech Gate**（{{Eng Lead}} + {{QA Lead}}）：{{exit criterion with number}}
2. **Business Gate**（{{Sponsor}}）：{{exit criterion}}
3. **Data Gate**（{{PM}} + {{BI}}）：{{exit criterion}}

---

# 11. Open Questions & Next Steps（Optional — 通常保留）

## 11.1 Open Questions

| # | 问题 | 谁答 | 阻塞 v1？ |
| --- | --- | --- | --- |
| Q1 | {{question}} | {{name}} | {{否，但影响 …}} or **是 —— {{reason}}** |

≤ 6 rows. 阻塞列只允许两种语法（见 format-conventions §7）。

## 11.2 Next Steps

| Step | Owner | When |
| --- | --- | --- |

≤ 6 rows.

---

## Appendix A — Source-of-truth links （可选）

≤ 10 rows. 1 row per source. NOT a per-claim citation map.

| Type | Source | Link |
| --- | --- | --- |

---

## Appendix B — Decision log（可选）

≤ 6 rows. 主要的"考虑过 A 选了 B"的决策。

| 决策 | 选项 A | 选项 B | Chosen | Reasoning | Reopen trigger |
| --- | --- | --- | --- | --- | --- |

---

## Appendix C — For engineering reference（可选 — 仅当 PM 主动放进去时）

> **Default = 不写这一节。** 如果 PRD 里出现了路由 / 字段 / 服务名等技术细节，但 PM 又不想砍掉，把它们放在这里，正文保持业务语言。
> 大多数情况：直接 `详见 [Tech Design]({{link}})`，不要在 PRD 里复制 tech 细节。

---

_文档结束。{{1 句话 next action by 文档 owner}}_

```

---

## Notes for the agent (not part of the PRD body)

When filling the template:

1. **Hard length cap** — ≤ 250 lines body. If you exceed, cut Section 5 / 6 / 7 first; technical detail belongs in Tech Design.
2. **Voice gate** — before publish, scan against `voice-and-register.md`. Strip / move banned items.
3. **Never invent citations** — unsupported claims → `⚠️ Open question` in §11.1.
4. **IMG markers** match filenames in `~/Desktop/<feature>-figma/` exactly.
5. **No inline CSS, no border-left, no gradients** — Confluence applies its own styling.
6. **Default = drop §7 and Appendix C** — PMs rarely need both. Keep §7 only if the PM explicitly asks for explicit Given/When/Then.
