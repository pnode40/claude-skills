# Claude Skills — Development Methodology

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
