---
description: Start the QIMA PRD drafting workflow (context gathering → depth interview → Confluence-ready draft → auto-review).
---

Invoke the `write-prd` skill to draft a PRD end-to-end for the user.

Follow the skill's full workflow: aggregate context from local files, Outlook, Teams, SharePoint, Confluence, Figma, Notion, and QSP repos; run Phase 1.5 business-background mining and Phase 2.5 multi-turn depth interview; enforce QIMA's official 11-section PRD template; write the draft to the specified Confluence page; then auto-invoke `prd-critique` and iterate until no serious issues remain.

User arguments: $ARGUMENTS
