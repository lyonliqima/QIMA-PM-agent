# QIMA PM Skills (Claude Code plugin)

End-to-end PRD drafting, codebase understanding, and design workflow toolkit for QIMA Product Managers.

## Contents

- **Skill** `write-prd` — orchestrates context gathering, depth interview, Confluence-ready PRD writing, and the auto-review loop. Bundles `references/`, `scripts/`, and `templates/`.
- **Skill** `codebase-understanding` — produces a structured repo / team / architecture brief for a feature. Standalone, or invoked as Phase 1.X of `write-prd` when the PRD subject is technically novel or cross-system.
- **Skill** `prd-to-dev-ticket-breakdown` — breaks a Confluence PRD into a Jira Epic and FE / BE / API tickets, requires user approval before Jira writes, links tickets to the Epic, and writes the created ticket links back to the PRD.
- **Design skills** — `impeccable`, `critique`, `audit`, `polish`, `layout`, `typeset`, `adapt`, `animate`, `harden`, `optimize`, `clarify`, `colorize`, `bolder`, `quieter`, `distill`, `delight`, `overdrive`, and `shape` for frontend design work.
- **Skill** `business-aware-design-critique` — evidence-based QIMA design review that connects Figma, Confluence business rules, code implementation, and Jira history into an HTML report.
- **Agent** `prd-review-expert` — senior PMO/CPO-level reviewer. Auto-invoked after the initial draft; can also be called standalone on any PRD (local file or Confluence URL).
- **Slash command** `/write-prd` — entry point for the PRD workflow.
  - **Deprecated alias** `/qima-prd-skills` is kept through 0.9.x for muscle memory; will be removed in 1.0.
- **Slash command** `/codebase-understanding` — entry point for the architecture brief.

## Install (local)

```
/plugin install ~/Desktop/QIMA\ PM\ Agent
```

Or from the Claude Code UI: **Plugins → Install from local path** → select the `QIMA PM Agent` folder.

## Install from GitHub marketplace

```
/plugin marketplace add lyonliqima/QIMA-PM-agent
/plugin install qima-pm-skills@qima-pm-agent
```

## Usage

- Type `/write-prd` and describe the feature, or just say "write a PRD for X" / "起草 PRD" — the skill auto-triggers on natural-language phrasing too.
- For a standalone code-base brief: `/codebase-understanding [feature name]`.
- To create Jira implementation tickets from a PRD: `prd-to-dev-ticket-breakdown <confluence-prd-url> <jira-project-key> [design-url]`.
- For design work, ask naturally (for example, "critique this design", "make this page responsive", "polish this component", "add purposeful animation") or invoke a design skill by name when available.
- For evidence-based QIMA design review: `business-aware-design-critique <figma-url> [confluence-page-id] [repo-path]`.
- Once a draft exists, ask "review this PRD" or pass a Confluence URL to invoke `prd-review-expert` directly.

## Requirements

- Atlassian (Confluence/Jira) MCP connected
- Figma MCP + token at `~/.config/figma-token` (for design-driven PRDs and design critique)
- Outlook / Teams / SharePoint MCPs (optional, used for context mining)
- Notion MCP (optional)

## Renamed in 0.8.0

This plugin was previously published as `qima-prd-skills`. It was renamed to `qima-pm-skills` because its scope is broader than just PRDs — `codebase-understanding` is already in the box, and more PM workflows are coming. **No behavior change** in 0.8.0, just rename:

| Old | New |
|---|---|
| Plugin id `qima-prd-skills` | `qima-pm-skills` |
| Main skill `qima-prd-skills` | `write-prd` |
| Slash `/qima-prd-skills` | `/write-prd` (old slash kept as alias through 0.9.x) |

To upgrade locally: `/plugin uninstall qima-prd-skills && /plugin install ~/Desktop/QIMA\ PM\ Agent`.

## Version

0.10.0
