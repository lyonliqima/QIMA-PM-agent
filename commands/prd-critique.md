---
description: Review an existing PRD against QIMA PMO/CPO quality gates, template rules, voice/register constraints, and best-PRD patterns.
---

Invoke the `prd-critique` skill to review a local PRD file or Confluence PRD URL.

Use this command when the user wants to:

- review or critique an existing PRD
- validate whether a PRD is ready for PM review or development handoff
- check QIMA template, format, voice/register, and hallucinated-specifics risks
- run the PRD quality loop after `/write-prd`

Important behavior:

- Read the entire PRD before forming findings.
- Do not edit the PRD.
- Do not create Jira tickets.
- Group findings by High / Medium / Low.
- Include exact sections, impact, and concrete fixes.
- Mark uncertainties as `Verification needed? yes` instead of guessing.

User arguments: $ARGUMENTS
