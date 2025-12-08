# Majestic Marketplace Tutorial

An interactive tutorial for onboarding experienced software engineers to the Majestic Marketplace Claude Code plugins.

## Quick Start

```bash
# Install dependencies
pnpm install  # or: bun install

# Start the presentation (opens browser)
pnpm dev  # or: bun dev
```

## Navigation

- **Arrow keys** or **Space** - Navigate slides
- **O** - Toggle slide overview
- **D** - Toggle dark mode
- **F** - Toggle fullscreen
- **G** - Go to specific slide

## Building for Production

```bash
# Build static SPA
pnpm build  # or: bun run build

# Export to PDF
pnpm export  # or: bun run export
```

## Content Covered

### Part 1: Installation & Setup
- Installing the marketplace and plugins
- Project configuration (`.agents.yml`)

### Part 2: Core Workflow
- Plan → Build → Review → Ship cycle
- Each phase explained with examples

### Part 3: majestic-engineer
- Architecture overview
- Key commands, agents, and skills
- Research and quality assurance

### Part 4: majestic-rails
- DHH/37signals philosophy
- Rails-specific agents and skills
- Hotwire, Stimulus, and database optimization

### Part 5: majestic-tools
- Discovery and analysis tools
- External LLM reviews (Codex, Gemini)
- Meta commands for creating extensions

### Part 6: Real-World Examples
- New feature end-to-end
- Debugging production issues
- Query optimization

### Part 7: Quick Reference
- Command cheat sheet
- Agent cheat sheet
- Skill cheat sheet
- Configuration reference

## Customization

Edit `slides.md` to customize the presentation. Slidev uses Markdown with Vue components for interactivity.

Key features:
- `<v-clicks>` - Progressive reveal
- Code highlighting with line numbers
- Mermaid diagrams for architecture
- Two-column layouts

## Tech Stack

- [Slidev](https://sli.dev/) - Developer-friendly presentation framework
- [Shiki](https://shiki.matsu.io/) - Syntax highlighting
- [Mermaid](https://mermaid.js.org/) - Diagrams
- [UnoCSS](https://unocss.dev/) - Utility CSS

## License

MIT
