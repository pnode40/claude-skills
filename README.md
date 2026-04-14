# Claude Code Skills

A curated collection of skills for [Claude Code](https://claude.ai/code) that extend Claude's capabilities with specialized knowledge, workflows, and domain expertise. Skills are auto-triggered based on context — no slash commands needed.

## Installation

Clone this repo and symlink each skill into `~/.claude/skills/`:

```bash
git clone https://github.com/pnode40/claude-skills.git ~/claude-skills
for skill in ~/claude-skills/*/; do
  ln -s "$skill" ~/.claude/skills/$(basename "$skill")
done
```

Skills are available immediately in any Claude Code session.

## How Skills Work

Claude reads the `description` field in each `SKILL.md` and automatically activates the relevant skill based on what you're working on. For example, open a `.tsx` file and `react-expert` activates. Mention a `.pdf` file and the `pdf` skill loads.

You can also invoke any skill explicitly with `/skill-name`.

## Skills

### Development

| Skill | Description |
|-------|-------------|
| `react-expert` | React 18+ components, hooks, Server Components, Next.js App Router, React 19 features |
| `typescript-pro` | Advanced TypeScript generics, type guards, branded types, tRPC end-to-end type safety |
| `fullstack-guardian` | Security-focused full-stack development across database, API, and UI layers |
| `webapp-testing` | Playwright-based testing for local web apps — screenshots, logs, UI verification |
| `debugging-wizard` | Systematic bug isolation via stack trace analysis, log correlation, and hypothesis-driven debugging |
| `spec-miner` | Reverse-engineer specs from legacy/undocumented codebases |

### Workflow & Methodology

| Skill | Description |
|-------|-------------|
| `build` | Full development methodology (brainstorm → plan → TDD → review → verify → finish) for significant features and new projects. Invoke with `/build`. |

### Architecture & Planning

| Skill | Description |
|-------|-------------|
| `planning-with-files` | File-based task planning (task_plan.md, findings.md, progress.md) for complex multi-step work |
| `mcp-builder` | Build MCP servers in Python (FastMCP) or TypeScript to integrate external APIs |
| `skill-creator` | Create and update Claude Code skills |
| `changelog-generator` | Auto-generate user-facing changelogs from git commit history |

### Design & UI

| Skill | Description |
|-------|-------------|
| `ui-ux-pro-max` | UI/UX intelligence: 50+ styles, 161 palettes, 99 UX guidelines across 10 stacks |
| `ui-styling` | shadcn/ui, Radix UI, Tailwind CSS — accessible components, dark mode, theming |
| `design` | Full design suite: logos, brand identity, banners, icons, social assets, HTML presentations |
| `design-system` | Three-layer token architecture (primitive→semantic→component), CSS variables, component specs |
| `banner-design` | Banners for social media, ads, and web in 13+ styles |
| `slides` | Strategic HTML presentations with Chart.js, design tokens, and copywriting formulas |
| `brand` | Brand voice, visual identity, messaging frameworks, style guides |

### Documents & Files

| Skill | Description |
|-------|-------------|
| `pdf` | Read, merge, split, watermark, encrypt, OCR, and create PDFs |
| `docx` | Create, read, edit, and format Word documents |
| `pptx` | Create, parse, edit, and combine PowerPoint presentations |
| `xlsx` | Read, edit, create, and convert spreadsheet files (.xlsx, .csv, .tsv) |

## Credits

Skills sourced from:
- [claudekit](https://github.com/anthropics/claudekit) — `banner-design`, `brand`, `design`, `design-system`, `slides`, `ui-styling`
- [Jeffallan](https://github.com/Jeffallan) — `react-expert`, `typescript-pro`, `fullstack-guardian`, `debugging-wizard`, `spec-miner`
- Community contributions — remaining skills

## License

Individual skills retain their original licenses. See each `SKILL.md` for details.
