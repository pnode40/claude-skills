# Stage 2: Refinement & Structure

**Goal:** Build the document section by section through brainstorming, curation, and iterative refinement.

## Setup

Explain the per-section process to the user:
1. Clarifying questions about what to include
2. Brainstorm 5-20 options
3. User curates (keep/remove/combine)
4. Draft the section
5. Refine through surgical edits

Start with whichever section has the most unknowns (core proposal for decision docs, technical approach for specs). Write summary/intro sections last.

## Determine Structure

**If the document structure is clear:** Ask which section to start with and suggest the highest-unknown section first.

**If the user doesn't know what sections they need:** Suggest 3-5 sections appropriate for the doc type. Ask if the structure works or needs adjustment.

## Create Scaffold

Once structure is agreed, create the document with placeholder text for all sections.

**If artifacts available:** Use `create_file` with all section headers and `[To be written]` placeholders.

**If no artifacts:** Create a markdown file in the working directory (e.g., `decision-doc.md`, `technical-spec.md`) with the same structure.

**Key instruction for user (state this once when starting the first section):**
Ask them to indicate changes rather than edit the doc directly — this helps learn their style for future sections. Example: "Remove the X bullet — already covered by Y" or "Make the third paragraph more concise."

## Per-Section Cycle

Repeat for each section:

### 1. Clarifying Questions
Announce the section. Ask 5-10 specific questions about what to include. Shorthand answers are fine.

### 2. Brainstorm
Generate 5-20 numbered options for the section based on complexity. Dig into context shared that might have been forgotten, and angles not yet mentioned. Offer to brainstorm more if they want.

### 3. Curation
Ask which points to keep, remove, or combine. Request brief justifications to learn priorities.

Examples: "Keep 1,4,7,9" / "Remove 3 (duplicates 1)" / "Combine 11 and 12"

If user gives freeform feedback instead of numbered selections, parse their preferences and apply them.

### 4. Gap Check
Ask if anything important is missing before drafting.

### 5. Draft
Use `str_replace` to replace the section placeholder with drafted content. Provide artifact link if applicable.

Ask them to read through it and share what to change.

### 6. Iterate
Apply feedback with `str_replace` — never reprint the whole doc. If user edits directly and asks for a read, note the changes and incorporate that into future sections.

After 3 consecutive iterations with no substantial changes, ask if anything can be removed without losing important information.

Confirm section complete. Ask if ready for the next section.

## Near Completion

At 80%+ of sections done, re-read the entire document and check for:
- Flow and consistency across sections
- Redundancy or contradictions
- Generic filler — every sentence should carry weight

Provide feedback, make any final adjustments.

## Exit Condition

All sections drafted and refined, full document reviewed for coherence.

Ask if ready to move to Stage 3, or if they want to refine anything else. When ready, load `references/stage-3-reader-testing.md`.
