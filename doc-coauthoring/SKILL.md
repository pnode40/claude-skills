---
name: doc-coauthoring
description: Guide users through a structured workflow for co-authoring documentation. Use when user wants to write documentation, proposals, technical specs, decision docs, or similar structured content. This workflow helps users efficiently transfer context, refine content through iteration, and verify the doc works for readers. Trigger when user mentions writing docs, creating proposals, drafting specs, or similar documentation tasks.
---

# Doc Co-Authoring Workflow

Structured three-stage workflow for collaborative document creation. Act as an active guide through each stage.

## When to Offer This Workflow

**Trigger conditions:**
- User mentions writing documentation: "write a doc", "draft a proposal", "create a spec", "write up"
- User mentions specific doc types: "PRD", "design doc", "decision doc", "RFC"
- User seems to be starting a substantial writing task

**Initial offer:**
Offer the user a structured workflow. Explain the three stages briefly:
1. **Context Gathering** — user dumps context, Claude asks clarifying questions
2. **Refinement & Structure** — build each section through brainstorming and iteration
3. **Reader Testing** — test with a fresh Claude instance to catch blind spots

Ask if they want the structured workflow or prefer to work freeform. If they decline, work freeform. If they accept, proceed to Stage 1.

## Stages

| Stage | Reference | Goal |
|-------|-----------|------|
| Stage 1: Context Gathering | `references/stage-1-context-gathering.md` | Close the gap between what the user knows and what Claude knows |
| Stage 2: Refinement & Structure | `references/stage-2-refinement-structure.md` | Build the document section by section through brainstorming, curation, and iteration |
| Stage 3: Reader Testing | `references/stage-3-reader-testing.md` | Verify the doc works for readers using a fresh Claude with no context |

Load the reference file for the current stage when entering it. Do not load all three upfront.

## General Guidance

- Be direct and procedural — don't try to "sell" the approach, just execute it
- Always give the user agency to skip stages or work freeform
- If the user seems frustrated, acknowledge it and suggest ways to move faster
- Don't let context gaps accumulate — address them as they come up
- Use `str_replace` for all edits; never reprint the whole document
