---
description: Break a Confluence PRD into a Jira Epic and implementation tickets, then write created ticket links back to the PRD after user approval.
---

Invoke the `ticket-breakdown` skill to convert a Confluence PRD into Jira implementation work.

Follow the skill's workflow:
1. Read the Confluence PRD and extract functional requirements, priorities, dependencies, design links, and open questions
2. Plan one Jira Epic plus Front-end, Back-end, API/Contract, and optional QA/Test tickets
3. Present the full Epic/ticket creation plan to the user and stop for explicit approval
4. After approval, create the Epic and tickets in Jira, associate all tickets to the Epic, and link dependencies
5. Append or replace the PRD's `Development Tickets` section with the created Epic/ticket links

The user's initial request is not approval to create Jira issues. Do not call Jira write tools until the user confirms the creation plan.

User arguments: $ARGUMENTS
