---
description: Run an evidence-based QIMA design critique using Figma, Confluence business rules, code evidence, and Jira history.
---

Invoke the `design-critique` skill to review a design with QIMA business and implementation context.

Follow the skill's workflow:
1. Read the Figma node metadata, screenshot, and design context
2. Match screen terms against Confluence PRDs / Tech Designs, Jira issues, and relevant frontend or backend code
3. Extract business rules, implementation evidence, and historical decisions
4. Review the design across interaction flow, visual consistency, copy, spacing, and business correctness
5. Generate a self-contained HTML report with severity-grouped findings and clickable evidence links

If the required Figma URL is missing, ask for it before proceeding. If Confluence page ID or repo path is missing, infer where possible; otherwise ask before making evidence-backed claims.

User arguments: $ARGUMENTS
