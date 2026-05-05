# Voice & Register — PRD 正文语言规范（HARD GATE）

PRD 的读者是 PM / Design / 业务 lead / 客户代表 —— **不是工程师**。技术实现属于 Tech Design 文档，PRD 只指向它。

> **本规则是 hard gate**：Phase 4 起草后、Phase 4.7 review 前，按这份清单扫一遍正文；任何残留物移到 *Appendix · For engineering reference* 或直接删除。Phase 4.7 reviewer 会再扫一次。

---

## 0. 长度与篇幅上限

PRD 正文（不含 Appendix）：

- **目标 ≤ 250 行 markdown / ≤ 6 页 Confluence**
- **§5.1 FR 表**：≤ 12 行；超过 12 条说明你在写 dev spec，回到 PM 抽象层
- **§6 Edge Cases**：≤ 8 条；剩余的列入 Appendix
- **§11.1 Open Questions**：≤ 6 条；每条 ≤ 1 句

如果超出上限，先剪 §5、§6、§7（AC）—— 多数膨胀来自这三节复制 Tech Design 内容。

---

## 1. 禁止出现在正文的内容

| 禁止 | 例子 | 改写方式 |
| --- | --- | --- |
| **微服务链路 / repo 名** | `psi-web-cloud → final-report-service-cloud → aca-new` | "验货数据从现场采集 → 组装报告 → 在线呈现" |
| **Jira 工单号堆叠** | "SP-32258 / SP-32257 / SP-32296 / SP-32308 / SP-33093 / SP-33240..." | 全文最多 **3 个** Jira 引用，且只在 §1 meta-table 与 Appendix 里出现 |
| **代码 / 组件 / 函数名** | `V2Header`, `ReportPageV5`, `inspection-report.service` | "顶部决策栏"，"报告主页面" |
| **API / 字段路径** | `keyIndicator.aqlLevel = "reference"`, `productReferenceWorkmanShipResult[]` | "Workmanship 结果按 product / reference 两种维度展示" |
| **运维 / 实现术语** | route component swap, killswitch, ETag, CDN, immutable cache, monorepo, microservice, snake_case event | "切版方式"、"灰度回退开关"、"缓存策略" |
| **DB / Schema 描述** | "新增 `client_rating_feedback` 字段" | "新增评分反馈" |
| **commit / branch / PR** | `commit a3f29b on develop` | 完全不出现在 PRD |

---

## 2. Stakeholders 表

只列**团队名 + 负责人**。**不要**把 repo / service 名列在 Responsibility 列里。

| Role | Name | Responsibility |
| --- | --- | --- |
| Backend Lead | Hydie Chan（Titan TL） | 报告服务与网关 |
| Frontend Lead | Eric Wang | 前端实现与协调 |

不允许这种写法：~~"Eric Wang — `aca-new` + `report-service-cloud` + `gateway-service-cloud`"~~。

---

## 3. Dependencies 写法

分桶概述，**不点名 repo**：

- Frontend（报告呈现组件）
- Backend（结论聚合接口、AI Summary 字段）
- Platform（租户级开关、运营配置）
- Mail（邮件模板，Phase 2）
- Legal（AI 免责文案签字）
- BI（埋点契约 + dashboard）

具体 service 名 / 端点 / 函数路径 → Tech Design。

---

## 4. §1 相关资料 行（meta-table）

最多 **6 个链接**，每个 1 行：Tech Design / Figma / 主要 UX Audit / 主要 memo / Prototype / Epic（如果引用）。**不要** 把 8–12 条资料全列出来 —— Source ledger 在最后单独列。

---

## 5. 如必须保留技术细节

放 **Appendix · For engineering reference**，与正文分离，或直接指向 Tech Design：

> 详见 [Tech Design — Smart Report] Confluence 4559699969

如果 PM 要求 dev-ready handoff，运行 `ticket-breakdown` skill —— 那是专门做这事的，不要把 PRD 撑大。

---

## 6. 允许的例外

- **§6 Design** 可引用 Figma 节点 ID（设计师之间需要对齐）。**实际上每个 §6.x Page N 必须带 Figma deep-link**（含 `?node-id=…`）—— 让 reviewer 一键跳到对应 frame；只链到 file 根目录是 finding，要修。详见 `figma-handling.md` Step 2。
- **§9.1 Dependencies** 可列 "Backend / Frontend / Mail" 等大模块名
- **§1 meta-table 相关资料** 可点名 1 个 Tech Design 链接
- **§11.1 Open Questions** 可引用 1 个 Jira ticket（如 *"权限模型决定见 SP-32254"*）—— 仅限作为追踪锚点
- **专有产品名**（myQIMA / QIMAone / QIMAlabs / Smart Report / PSI / AQL / POM / CAP）保留

---

## 7. 审稿快查清单

正文搜一下，命中即改：

- [ ] `cloud` —— 几乎肯定是 service 名
- [ ] `service` —— 同上
- [ ] `route` / `endpoint` / `payload` / `schema` / `JSON`
- [ ] `repo` / `commit` / `branch` / `PR` / `Lambda`
- [ ] `SP-` 出现 ≥ 4 次（按规则压到 ≤ 3）
- [ ] 反引号 `code identifiers` 出现 ≥ 6 次（按规则压到 ≤ 3 —— 仅产品名 / 关键 enum）
- [ ] "snake_case" / "camelCase" / "kebab-case" 任一
- [ ] "killswitch" / "feature flag" / "ETag" / "CDN" / "lazy load"

清单里命中的，全删或挪 Appendix。
