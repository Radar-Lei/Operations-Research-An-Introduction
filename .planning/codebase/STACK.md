# Technology Stack

**Analysis Date:** 2025-02-02

## Languages

**Primary:**
- Markdown (`.md`) - All content storage and documentation

**Secondary:**
- YAML (`.yaml`, `.yml`) - Configuration and frontmatter metadata
- JSON (`.json`) - Configuration files

## Runtime

**Environment:**
- Obsidian (markdown-based knowledge management application)
- Cross-platform desktop application (Windows, macOS, Linux)
- Mobile apps (iOS, Android)

**Package Manager:**
- None (Obsidian plugin ecosystem uses community plugins)

## Frameworks

**Core:**
- Obsidian - Knowledge base and note-taking platform
  - Local-first markdown storage
  - Plugin architecture for extensibility
  - Bidirectional linking via `[[wikilinks]]`
  - Block ID references via `^anchorId` syntax

**Visualization:**
- markmap - Mind map visualization from markdown content
  - Rendered via code blocks marked as ```markmap
  - Supports hierarchical node structures
  - LaTeX formula rendering with `$$` and `$` delimiters
  - Configurable height settings

**Custom Tooling:**
- `.trae/` framework - Custom AI assistant skill system
  - Location: `.trae/skills/`
  - Skills defined as markdown documents with YAML frontmatter
  - Example: `.trae/skills/obsidian-markmap-processor/SKILL.md`

## Key Dependencies

**Critical:**
- Obsidian - Core platform for markdown storage and linking
- markmap - Mind map visualization from markdown code blocks

**Documentation:**
- None (native markdown only)

## Configuration

**Environment:**
- Obsidian vault configuration (typically in `.obsidian/` directory - not present in this vault)
- Git version control for content tracking

**Build:**
- None (static markdown files)

**Ignored Files:**
- `.gitignore` excludes `.trae/` directory from version control

## Platform Requirements

**Development:**
- Obsidian desktop app (optional, for GUI editing)
- Any text editor for direct markdown editing
- Git for version control

**Production:**
- Obsidian app (desktop or mobile) for viewing and editing
- Alternatively, any markdown viewer
- For markmap rendering: Obsidian with markmap plugin or compatible viewer

**File Structure:**
- Content organized by textbook chapters
- Each chapter contains:
  - Primary chapter notes (e.g., `CHAPTER 1 What Is Operations Research?.md`)
  - Supplementary notes (e.g., `sensitivity analysis.md`)
  - Embedded markmap code blocks for visual summaries
  - Block IDs (`^anchorId`) for bidirectional linking between markmap nodes and content

---

*Stack analysis: 2025-02-02*
