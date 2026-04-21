# Claude Skills — Development Methodology

## Baseline Coding Behaviors

These principles apply to **every task**, trivial or complex, whether or not `/build` is invoked.

**Tradeoff:** These guidelines bias toward caution over speed. For truly trivial tasks, use judgment.

### 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

### 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

### 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

## Design Methodology Skills

The design methodology is a structured workflow for significant software work. It is composed of
one orchestrating skill and a set of domain-expert skills it invokes:

### Orchestrator

| Skill | Role |
|-------|------|
| `build` | Sequences the full methodology: brainstorm → plan → TDD implementation → code review → verify → finish branch. Invoke with `/build`. |

### Domain Experts (invoked by `/build` during Phase 3)

| Skill | When invoked |
|-------|-------------|
| `react-expert` | React components, hooks, Server Components, Next.js |
| `typescript-pro` | TypeScript type system, generics, branded types |
| `fullstack-guardian` | Full-stack features with auth, validation, or security concerns |
| `ui-ux-pro-max` | UI layouts, interaction design, component patterns |
| `ui-styling` | shadcn/ui, Radix UI, Tailwind CSS, theming |
| `webapp-testing` | Playwright-based UI verification and test automation |
| `debugging-wizard` | Bugs encountered mid-implementation |

### Supporting Methodology Skills

| Skill | When used |
|-------|-----------|
| `planning-with-files` | Complex multi-step work requiring persistent task tracking across sessions |

---

## When to suggest /build

When the user describes work that is clearly significant in scope — a new feature, a new project,
a major architectural change, or anything spanning multiple files or systems — proactively suggest
invoking the `/build` skill before proceeding:

> "This sounds like a significant build. Want me to kick off `/build` to run it through the full
> methodology (brainstorm → plan → TDD implementation → review → verify)?"

Let the user decide. If they say no, proceed normally. Do not force the workflow.

**Suggest /build when the user:**
- Describes building something new ("add X feature", "create a Y system", "implement Z")
- Mentions a major change affecting multiple parts of the codebase
- Starts a greenfield project or a significant new module

**Do not suggest /build for:**
- Bug fixes with a clear, obvious cause
- Single-file edits or small refactors
- Documentation, config, or formatting changes
- Anything the user describes as "quick" or "minor"
