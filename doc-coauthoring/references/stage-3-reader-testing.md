# Stage 3: Reader Testing

**Goal:** Verify the document works for readers using a fresh Claude instance with no context from this conversation.

Explain to the user: this catches blind spots — things that make sense to the authors but might confuse others.

---

## If Sub-Agents Are Available (e.g., Claude Code)

Perform testing directly without user involvement.

**Step 1 — Predict Reader Questions**
Generate 5-10 questions readers would realistically ask when trying to find or understand this document.

**Step 2 — Test with Sub-Agent**
For each question, invoke a sub-agent with only the document content and the question (no conversation context). Summarize what Reader Claude got right/wrong for each.

**Step 3 — Additional Checks**
Invoke a sub-agent to check for: ambiguity, false assumptions, internal contradictions. Summarize issues found.

**Step 4 — Fix**
If issues found, list them and loop back to Stage 2 refinement for the problematic sections. Re-test after fixes.

---

## If No Sub-Agents Available (e.g., claude.ai web interface)

The user will need to test manually.

**Step 1 — Predict Reader Questions**
Generate 5-10 questions readers would realistically ask.

**Step 2 — Setup Testing**
Instruct the user to:
1. Open a fresh Claude conversation
2. Paste or share the document content
3. Ask Reader Claude the generated questions

For each question, ask Reader Claude to provide:
- The answer
- Anything that was ambiguous or unclear
- What knowledge/context the doc assumes readers already have

**Step 3 — Additional Checks**
Also ask Reader Claude:
- "What in this doc might be ambiguous or unclear to readers?"
- "What knowledge or context does this doc assume readers already have?"
- "Are there any internal contradictions or inconsistencies?"

**Step 4 — Iterate**
Ask what Reader Claude struggled with. Fix those gaps in Stage 2, then re-test.

---

## Exit Condition

Reader Claude consistently answers questions correctly and surfaces no new gaps or ambiguities.

---

## Final Review

When Reader Testing passes:

1. Recommend a final read-through by the user — they own this document
2. Suggest double-checking facts, links, and technical details
3. Ask them to verify it achieves the intended impact

Ask if they want one more review, or if the work is done.

**Final tips to share on completion:**
- Consider linking this conversation in an appendix so readers can see how the doc was developed
- Use appendices for depth without bloating the main doc
- Update the doc as real reader feedback comes in
