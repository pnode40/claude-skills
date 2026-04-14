---
name: recursive-optimization
description: "Silently runs a 4-step internal loop before responding to any complex request: (1) Architect — full solution design with tactical breakdown per component, (2) Adversarial Review — critique the plan for gaps, edge cases, and structural flaws, (3) Revise — fix all critical/high issues before executing, (4) Execute — deliver only the final output. Use for ANY complex output: code generation, prompt engineering, frameworks, strategies, templates, documents, briefs, checklists, and system designs. Trigger whenever the request has multiple components, involves an external system (Perplexity, Copilot, GPT, Cursor), or would benefit from getting it right on the first pass rather than iterating. When in doubt, run the loop — the cost of skipping it is a weaker output."
---

# Recursive Optimization Skill

## Purpose

Enforce a silent 4-step internal loop before delivering any complex output. The user sees only the final result — no scaffolding, no intermediate thinking, no "here's my plan" preamble.

---

## The Loop (Execute Entirely in Background)

### Step 1 — Architect

Before writing a single line of output:

- Map the full solution scope
- Break into discrete components
- Define the execution order and dependencies between components
- Identify the 2–3 highest-risk areas most likely to fail, underperform, or be misunderstood
- Note any assumptions being made that the user hasn't explicitly confirmed

### Step 2 — Adversarial Review

Switch to critical reviewer. Attack the plan across these dimensions:

| Dimension | Questions to Answer |
|-----------|-------------------|
| **Completeness** | Does it do everything the prompt asked for? What's missing? |
| **Edge Cases** | What inputs, states, or scenarios will break this? |
| **Structure** | Is there redundancy? Logical gaps? Wrong sequence? |
| **Usability** | Is it actually usable or just technically correct? |
| **Efficiency** | Anything bloated, over-engineered, or unnecessarily complex? |
| **Fit** | Is the format right for the target system or audience? |

Rank all issues found: **Critical → High → Medium → Low**

### Step 3 — Revise

- Fix all Critical and High issues before proceeding
- Fix Medium issues if effort is minimal
- Flag remaining trade-offs for the delivery note

### Step 4 — Execute

Produce the final output only. Apply these format rules:

**For code:** Deliver in a fenced code block with language tag.

**For prompts targeting external systems** (Perplexity, Copilot, GPT, Cursor, etc.): Deliver in a fenced code block, plain text inside, no markdown formatting within the block unless the target system renders it.

**For frameworks, strategies, templates:** Deliver as structured markdown — headers, numbered steps, or tables as appropriate to the content type.

**For documents/briefs:** Deliver as clean prose with minimal decoration unless structure is essential to usability.

---

## Delivery Format

After the final output, append a brief note (3–5 lines max):

```
---
**What changed after internal review:** [1–3 specific things revised between the initial plan and this output]
**Known trade-offs:** [anything intentionally left out or simplified, and why]
**Validate first:** [the single most important thing to test or confirm before using this]
```

If nothing changed after review (rare), say so — don't fabricate revisions.

---

## Override

If the user says **"skip optimization"** or **"quick draft"** — skip Steps 1–3 and deliver Step 4 directly. No delivery note required.

---

## Scope: When This Loop Applies

**Always run the loop for:**
- Code (any language, any length over ~10 lines)
- Prompts for external AI systems
- Multi-component frameworks or strategies
- Templates intended for repeated use
- Documents, briefs, or reports
- System designs or architectures

**Skip the loop for:**
- Short conversational replies
- Simple factual answers
- Clarifying questions
- Single-sentence or single-step outputs
