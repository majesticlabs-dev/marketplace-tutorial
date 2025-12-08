# Majestic Marketplace Tutorial

Load config: @.agents.yml

An interactive Slidev presentation for onboarding engineers to Majestic Marketplace plugins.

## WHAT (Architecture)

**Tech Stack:**
- Slidev presentation framework
- Node.js with pnpm package manager
- Markdown-based slides with Vue components

**Project Structure:**
```
.
├── slides.md        # Main presentation content
├── style.css        # Custom presentation styles
├── package.json     # Dependencies and scripts
└── README.md        # Setup and navigation guide
```

## WHY (Purpose)

**What This Does:**
- Interactive tutorial covering Majestic Marketplace plugins
- Seven parts: Installation → Core Workflow → Plugin Deep Dives → Examples → Reference
- Developer-friendly presentation with progressive reveals, code highlighting, diagrams

**Key Content:**
- `slides.md` - All presentation slides (Part 1-7)
- `style.css` - Custom styling for presentation theme

## HOW (Workflows)

### Development

```bash
# Start dev server (auto-opens browser)
pnpm dev

# View in browser: http://localhost:3030
```

### Building

```bash
# Build static SPA
pnpm build

# Export to PDF
pnpm export
```

### Navigation

- **Arrow keys / Space** - Navigate slides
- **O** - Slide overview
- **D** - Dark mode toggle
- **G** - Jump to slide

### Content Guidelines

When editing `slides.md`:
- Use `<v-clicks>` for progressive reveals
- Code blocks auto-highlighted with Shiki
- Mermaid diagrams for architecture flows
- Two-column layouts with `<div class="grid">`

### Verification

After content changes:
1. Run `pnpm dev` to preview
2. Check all slides render correctly
3. Verify code examples are accurate
4. Test navigation and transitions
