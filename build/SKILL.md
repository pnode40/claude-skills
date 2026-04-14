---
name: build
description: "Full software development methodology for significant builds: new features, new projects, or major changes within an existing codebase. Runs a structured workflow of brainstorm, plan, TDD implementation via subagents, code review, verify, and branch finish. Invoke explicitly with /build when starting something significant. Do NOT use for minor tweaks, small bug fixes, single-file edits, or quick changes."
user-invocable: true
argument-hint: "[description of what you're building]"
---

# Build

This skill orchestrates a full development methodology for significant work. It sequences
structured phases and invokes domain-specific skills at each phase rather than jumping
straight to code.

## When to Use

Use `/build` for:
- New features of meaningful scope
- New projects or greenfield work
- Major architectural changes
- Anything involving multiple files, systems, or layers

Skip for:
- Single-line or single-file fixes
- Renaming, reformatting, or refactoring a small function
- Quick bug fixes with obvious solutions
- Documentation-only changes

---

## Phase 1: Brainstorm

**Goal:** Reach a validated design before any implementation begins.

1. Announce: *"Starting /build — Phase 1: Brainstorm"*
2. Explore the codebase for relevant context: existing patterns, similar features, tech stack in use.
3. Ask clarifying questions **one at a time** — never more than one per message. Stop when the
   problem is fully understood.
4. Propose 2–3 distinct approaches with concrete trade-offs for each.
5. Present the chosen design incrementally, section by section. Request approval after each section.
6. Write the agreed design to `docs/specs/{feature-name}.md`.
7. Self-review the spec: check for gaps, contradictions, undefined terms, and missing edge cases.
8. Request user review of the written spec.

**Hard gate:** Do NOT proceed to Phase 2 until the user has explicitly approved the spec. Do not
write any code, scaffold any files, or install any dependencies during this phase.

---

## Phase 2: Plan

**Goal:** A complete, executable implementation plan with no placeholders.

1. Announce: *"Phase 2: Planning"*
2. Map the full file structure that will be touched or created.
3. Break work into bite-sized tasks (2–5 minutes each), ordered so each task is independently
   verifiable. Follow TDD ordering: failing test → minimal implementation → verify → commit.
4. For each task, include:
   - Exact file paths
   - Complete code (no "add validation here" or "implement as needed")
   - The exact command to verify it works and its expected output
5. Self-review the plan against the spec: every requirement must be traceable to at least one task.
   Flag and resolve any gaps before proceeding.
6. Offer to proceed with Phase 3 or let the user review the plan first.

**Quality bar:** If any task contains a placeholder, a vague instruction, or an undefined type,
the plan is not ready. Rewrite until every task can be executed by someone with zero codebase context.

---

## Phase 3: Implement (Subagent-Driven + TDD)

**Goal:** Execute the plan task by task, with isolated subagents and two-stage review per task.

1. Announce: *"Phase 3: Implementation"*
2. Read the full plan once and extract all tasks into a TodoWrite tracker.
3. For each task, run this cycle:

   **a. Dispatch implementer subagent** with:
   - The full task text and relevant file context
   - Instruction to follow the TDD cycle: write failing test → minimal code to pass → refactor

   **b. TDD enforcement within each task:**
   - Write the failing test first. Run it. Confirm it fails for the right reason.
   - Write the minimum code to make it pass. Run tests. Confirm passing.
   - Refactor if needed. Confirm tests still pass.
   - Never skip watching the test fail — if you didn't watch it fail, you don't know it tests
     the right thing.

   **c. Dispatch spec compliance reviewer** — does the implementation match the plan task exactly?
   If issues found, implementer fixes and reviewer re-checks. Loop until passing.

   **d. Dispatch code quality reviewer** — is the code well-structured, idiomatic, and free of
   obvious issues? If issues found, implementer fixes and reviewer re-checks. Loop until passing.

4. Invoke domain skills as the work requires:
   - React components or hooks → `react-expert`
   - TypeScript type system work → `typescript-pro`
   - Full-stack features with auth, validation, or security → `fullstack-guardian`
   - UI components, theming, or layouts → `ui-ux-pro-max` / `ui-styling`
   - Playwright testing or UI verification → `webapp-testing`
   - Bugs encountered mid-implementation → `debugging-wizard`

5. After all tasks pass both reviewers, proceed to Phase 4.

---

## Phase 4: Code Review

**Goal:** A final independent review of all changes before finishing.

1. Announce: *"Phase 4: Code Review"*
2. Capture the starting and ending commit hashes for the work.
3. Dispatch a code reviewer subagent with:
   - The original spec (`docs/specs/{feature-name}.md`)
   - The implementation plan
   - The full diff (commit range)
   - Instructions to assess: spec coverage, correctness, security, edge cases, code quality
4. Triage feedback:
   - **Critical** (wrong behavior, security issue, spec violation) → fix immediately, re-review
   - **Important** (quality issue, edge case missed) → fix before finishing
   - **Minor** (style, naming, nitpick) → log for later, do not block
5. Fix all critical and important issues. Re-run the reviewer until clean.

---

## Phase 5: Verify

**Goal:** Evidence-based confirmation that everything works before claiming done.

1. Announce: *"Phase 5: Verify"*
2. Run the full test suite. Read the output. Confirm all tests pass.
3. Run any lint or type-check commands the project uses. Read the output.
4. For UI work, start the dev server and manually exercise the golden path and edge cases.
5. Do not express completion, satisfaction, or correctness until these commands have been run
   and their output confirms success. "Should work" and "I'm confident" are not verification.
6. If anything fails, use `debugging-wizard` to isolate the root cause before attempting a fix.

---

## Phase 6: Finish Branch

**Goal:** Clean branch completion with explicit user choice.

1. Announce: *"Phase 6: Finish Branch"*
2. Verify tests pass (do not skip — always re-run here).
3. Present exactly four options without elaboration:
   - Merge locally into main/master
   - Push and create a Pull Request
   - Keep the branch as-is for now
   - Discard the work
4. Execute the chosen option. For destructive actions (discard), require the user to type
   "discard" to confirm.
5. Clean up git worktrees only for merge and discard paths. Preserve them for PR and keep-as-is.

---

## General Rules

- Announce each phase transition explicitly so the user always knows where things stand.
- Never skip a phase because the task "seems simple" — the phases exist for that reason.
- Stop and surface blockers immediately rather than working around them.
- Ask rather than assume when the plan is ambiguous.
- Do not implement on main/master directly — use a git worktree or branch.
