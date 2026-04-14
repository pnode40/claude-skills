# Stage 1: Context Gathering

**Goal:** Close the gap between what the user knows and what Claude knows, enabling smart guidance later.

## Initial Questions

Ask the user for meta-context about the document:

1. What type of document is this? (e.g., technical spec, decision doc, proposal)
2. Who's the primary audience?
3. What's the desired impact when someone reads this?
4. Is there a template or specific format to follow?
5. Any other constraints or context to know?

Inform them they can answer in shorthand or dump information however works best.

**If user provides a template or mentions a doc type:**
- Ask if they have a template document to share
- If they provide a link, use the appropriate integration to fetch it
- If they provide a file, read it

**If user mentions editing an existing shared document:**
- Read the current state via the appropriate integration
- Check for images without alt-text — if found, explain that Claude won't be able to see them when others paste the doc. Offer to generate alt-text if they paste each image into chat.

## Info Dumping

Encourage the user to dump all context they have:
- Background on the project/problem
- Related team discussions or shared documents
- Why alternative solutions aren't being used
- Organizational context (team dynamics, past incidents, politics)
- Timeline pressures or constraints
- Technical architecture or dependencies
- Stakeholder concerns

Advise them not to worry about organizing it — just get it all out.

**If integrations are available** (Slack, Teams, Google Drive, SharePoint, MCP servers): mention they can pull context directly.

**If no integrations and in Claude.ai:** suggest enabling connectors in Claude settings, or pasting content directly.

**During context gathering:**
- If user mentions team channels or shared docs and integrations are available: read them. If not: explain lack of access and ask them to paste content.
- If user mentions unknown entities/projects: ask if connected tools should be searched. Wait for confirmation before searching.
- Track what's been learned and what's still unclear.

## Clarifying Questions

When the user signals they've finished their initial dump (or after substantial context is provided), ask 5-10 numbered clarifying questions based on gaps.

Inform them they can answer in shorthand (e.g., "1: yes, 2: see #channel, 3: no because backwards compat"), link to docs, or keep info-dumping.

## Exit Condition

Sufficient context has been gathered when questions show understanding of edge cases and trade-offs without needing basics explained.

Ask if there's more context to add, or if it's time to move to Stage 2. When ready, load `references/stage-2-refinement-structure.md`.
