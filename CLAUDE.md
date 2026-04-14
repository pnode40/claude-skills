# Claude Skills — Development Methodology

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
