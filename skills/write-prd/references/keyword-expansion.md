# Keyword expansion — QIMA naming patterns

A feature in QIMA typically has **4-6 different names** scattered across sources. Searching only the canonical product name recovers roughly half the relevant context. This reference documents QIMA's recurring naming patterns and how to expand a seed term into a complete keyword map.

---

## Why expansion is mandatory

Observed naming drift across QIMA sources:

| Layer | Typical name form | Example (Package Charge) |
|---|---|---|
| PRD / product doc | Full product name, Title Case | "Package Charge Management" |
| Marketing / external | Shortened marketing name | "Package Fee" |
| Jira epic | Title with abbreviation suffix | "Package Charge Mgmt (PCM)" |
| Jira labels | lowercase-hyphen | `package-charge`, `billing` |
| Code repo name | kebab-case with version/module | `charge-service-cloud`, `billing-v2` |
| Chinese discussion | Direct translation or colloquial | "包装计费", "打包费用" |
| Engineering shorthand | Acronym | "PCM", "Charge v2" |
| Stakeholder references | Informal | "那个计费的东西", "老王的项目" |

Searching only "Package Charge Management" misses all 7 other layers.

---

## Expansion procedure

### Step 1 — Classify the seed

Identify which of these the seed term belongs to:

- **Product name** (e.g., "Package Charge Management") → need to expand DOWN to code names
- **Code / module name** (e.g., "billing-service") → need to expand UP to product name
- **Acronym** (e.g., "PCM") → need BOTH directions
- **Chinese term** (e.g., "计费") → need to find English equivalents

### Step 2 — Apply QIMA naming rules

**Rule 1 · English ↔ Chinese pairing**
Always generate both. If the seed is English, add the likely Chinese term(s); if Chinese, add English. Common QIMA domain pairs:

| Domain | English | Chinese |
|---|---|---|
| Inspection | inspection, audit, check | 验货, 审核 |
| Report | report, lab report, test report | 报告, 检测报告 |
| Sample | sample, specimen | 样品 |
| Lab | laboratory, QIMAlabs | 实验室 |
| Package / Charge | package, parcel, charge, fee, billing | 包装, 计费, 费用 |
| Inspector | inspector, auditor | 验货员, 审核员 |
| Order | order, booking | 订单, 预约 |
| Factory | factory, supplier | 工厂, 供应商 |

**Rule 2 · Version and module suffixes**
QIMA codebases commonly use `-v1` / `-v2` / `-cloud` / `-service` / `-web` suffixes. If the seed refers to an existing system, add variants:

- `<name>-service-cloud` — backend service
- `<name>-web-cloud` or `<name>-web` — frontend
- `<name>-v2` / `<name>-next` — rewrite project
- `<name>-external-service-cloud` — external-facing API

Example: seed "sample" expands to `sample-service-cloud`, `Sample-WEB`, `sample-v2`.

**Rule 3 · Team ownership as keyword**
The owning team name is a strong retrieval signal in Teams chats and Confluence. Use the team-to-project map (see `find-right-team/teams.md`) in reverse:

| Team | Typical domains |
|---|---|
| Apollo | audit, inspection, IRP, IPTB, PSI, factory |
| Titan | auth, e-signature, lab, sample, program, report, user |
| Loong | (check team mapping) |

If seed is "lab report", Titan is the likely owner → add "Titan" and "Titan team" as retrieval keywords for Teams / Confluence.

**Rule 4 · Acronym expansion**
QIMA acronyms in circulation — check these first:

| Acronym | Full form |
|---|---|
| PRD | Product Requirements Document |
| QSP | QIMA Service Platform |
| PSI | Pre-Shipment Inspection |
| GI | General Instruction |
| JTBD | Jobs to be Done |

If the seed is an acronym not in this table, ASK the user — and when they tell you, **append the new entry to this table and save the file**. This table is a living dictionary; every new acronym learned in a conversation should be persisted here for future runs.

**Rule 5 · Stakeholder names as keywords**
Pull likely stakeholder names from:
- Jira epic assignees / reporters (via `searchJiraIssuesUsingJql`)
- Confluence page contributors (via `searchConfluenceUsingCql`)
- Team leads from the team-project map

Stakeholder names appearing in Teams/Outlook are strong signals the context is relevant.

### Step 3 — Lightweight verification pass

Before committing to the keyword map, run these cheap queries in parallel:

```
# Jira — pull epic titles/labels
searchJiraIssuesUsingJql: text ~ "<seed>" OR labels = "<seed-kebab>"

# Confluence — pull page titles and labels
searchConfluenceUsingCql: text ~ "<seed>" AND type = page
```

Harvest additional variants from the results' titles, labels, and linked code repos. Add them to the map.

### Step 4 — Ask the user (one card)

Use `AskUserQuestion` with a single card:

> **"What other names might this feature have?"**
>
> I'll search all of these. Add any internal code names, past project names, team abbreviations, or Chinese terms.
>
> Current list: `[canonical] + [N auto-expanded variants]`

Cap at one round — do not loop.

---

## Output format — keyword-map.md

Save to the working directory as `keyword-map.md`:

```markdown
# Keyword map for <feature>

canonical:    Package Charge Management
en-variants:  package fee, parcel charge, shipping billing, package charge
zh-variants:  计费, 包装费, 包装计费, 打包费用
code-names:   PCM, charge-v2, billing-module
code-repos:   charge-service-cloud, billing-v2-web
jira-labels:  billing, package-charge, pcm
teams:        Apollo (owner), Titan (integration touchpoint)
stakeholders: <names from Jira + Confluence queries>

# Sources of these variants
- Jira epic QIMAL-1234 title
- Confluence page "Package Charge Capability – PRD"
- User clarification
```

Phase 1 scanners MUST join these variants with `OR` in their queries, not search canonical only.

---

## Stop conditions

Expansion is DONE when any of:

- Map has ≥ 3 English variants, ≥ 2 Chinese variants, ≥ 1 code name
- User confirms "that's all the names"
- Verification pass surfaces no new variants in two consecutive queries
- Time budget for this phase exceeded 5 minutes of tool calls

Do NOT loop forever pursuing completeness. Missing one variant is recoverable in Checkpoint A; burning the user's time is not.

---

## Anti-patterns

- ❌ Searching only the canonical product name in Phase 1
- ❌ Auto-translating Chinese to English via dictionary without checking QIMA's actual usage
- ❌ Asking the user to list ALL variants before any auto-expansion (lazy)
- ❌ Treating the keyword map as immutable — if Phase 1 surfaces a new name, append it
- ❌ Ignoring team names as retrieval keys — team names are high-signal in chat / Confluence

---

## Maintenance — living dictionary

This reference MUST grow over time. Whenever a user supplies a new QIMA-specific name, acronym, code repo suffix, team, or English↔Chinese term pair during a PRD run, **append it to the appropriate table in this file before ending the turn**. Do not keep the knowledge only in conversation memory — persist it here so the next run benefits.

Triggers to append:

- User expands an acronym you didn't know → append to **Rule 4** table
- User provides a Chinese term for an English concept (or vice versa) → append to **Rule 1** table
- User names a team and its domain → append to **Rule 3** table
- User reveals a repo naming convention (e.g., "we always suffix mobile apps with `-app`") → append to **Rule 2** list

Commit message convention (if version-controlled): `docs(keyword-expansion): add <term> from <context>`.
