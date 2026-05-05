---
description: Produce a structured code base understanding brief for a QIMA feature or module — repo map, architecture, team ownership, key APIs, related Tech Designs and Jira tickets.
---

Invoke the `codebase-understanding` skill to produce a structured 10-section code base brief for a QIMA feature, module, or system area.

Follow the skill's workflow:
1. Identify aliases (English / Chinese / code names / Jira labels)
2. Run parallel discovery — Confluence Tech Design pages, GitHub repos via QSP `Repos.md` inventory, Jira epics / stories / bugs, service catalog, team-to-repo map
3. Synthesize into the 10-section markdown brief (≤ 300 lines)
4. Save to working folder + copy to user's Cowork mounted folder; return `computer://` link + 5-bullet summary

Output is a navigation map, not a tech design. Repo names, service names, API paths are part of the deliverable's substance — allowed in this brief (unlike in the main PRD body).

User arguments: $ARGUMENTS
