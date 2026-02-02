# Architecture

**Analysis Date:** 2025-02-02

## Pattern Overview

**Overall:** Obsidian Knowledge Base with Integrated Mind Maps

This is an Obsidian vault structured as an academic textbook companion for "Operations Research: An Introduction." The architecture follows a hierarchical chapter-based organization with bidirectional linking between conceptual mind maps and detailed content.

**Key Characteristics:**
- Chapter-centric modular organization
- Markmap mind maps with bidirectional anchor links to body text
- Co-located images and resources within chapter directories
- Processing skill definitions for automated content transformation
- Git-tracked documentation with ignored planning/artifact directories

## Layers

**Content Layer:**
- Purpose: Contains the primary educational content organized by textbook chapters
- Location: `CHAPTER [NUMBER] [Topic Name]/` and `APPENDIX [LETTER] [Topic Name]/`
- Contains: Markdown files with embedded markmap code blocks, LaTeX formulas, HTML tables, and block anchors
- Depends on: Images in subdirectories, external markmap rendering plugin
- Used by: Obsidian markmap plugin for visualization, readers for learning

**Visualization Layer:**
- Purpose: Provides hierarchical mind map representations of chapter content
- Location: Embedded within chapter markdown files as `` ```markmap `` `` code blocks
- Contains: Hierarchical node structures with bidirectional links using `[[#^anchorId|Display Name]]` syntax
- Depends on: Content layer block anchors (`^anchorId`)
- Used by: Obsidian markmap plugin for interactive visualization

**Resource Layer:**
- Purpose: Stores supplementary visual assets
- Location: `images/` subdirectories within each chapter, `_resources/` for some chapters
- Contains: JPG images (book figures, diagrams, tables) with standardized naming pattern `bo_d56m[a-z0-9_]+.jpg`
- Depends on: None (static assets)
- Used by: Content layer via markdown image syntax

**Processing Layer:**
- Purpose: Defines automated content transformation skills
- Location: `.trae/skills/obsidian-markmap-processor/SKILL.md`
- Contains: Skill definitions for markmap generation, anchor linking, and table standardization
- Depends on: Content layer markdown files
- Used by: AI agents/automation tools for content processing

**Planning Layer:**
- Purpose: Stores execution plans and processing artifacts
- Location: `.trae/documents/` and `.planning/`
- Contains: Task lists, execution plans, codebase analysis documents
- Depends on: Content layer for analysis
- Used by: Planning workflows, AI agents

**Metadata Layer:**
- Purpose: Provides alias definitions and cross-references
- Location: Separate markdown files within chapter directories (e.g., `sensitivity analysis.md`)
- Contains: YAML frontmatter with aliases for multi-language support
- Depends on: Content layer
- Used by: Obsidian's linking system for searchability

## Data Flow

**Content Creation Flow:**

1. Chapter markdown files are created with structured content
2. Markmap code blocks are added summarizing content hierarchy
3. Block anchors (`^anchorId`) are added to body text paragraphs
4. Markmap nodes reference anchors using `[[#^anchorId|Display Name]]`` syntax
5. Images are placed in `images/` subdirectories

**Processing Flow:**

1. Processing plans are created in `.trae/documents/`
2. The `obsidian-markmap-processor` skill is invoked
3. HTML tables are converted to markdown format
4. Markmap code blocks are generated or updated
5. Bidirectional anchor links are created between markmap and body text
6. Results are written back to chapter files

**Navigation Flow:**

1. Reader views markmap visualization in Obsidian
2. Clicking markmap node navigates to corresponding body text anchor
3. Block anchors in body text link back to markmap nodes
4. Images load from local `images/` directories

**State Management:**
- Content is static (no runtime state)
- Version control via Git
- Planning documents track pending transformations
- Block anchors maintain referential integrity between layers

## Key Abstractions

**Chapter:**
- Purpose: Represents a textbook chapter or appendix with all associated content
- Examples: `CHAPTER 1 What Is Operations Research?/`, `CHAPTER 21 Nonlinear Programming Algorithms/`
- Pattern: Each chapter is a self-contained directory with markdown file and resources

**Markmap Node:**
- Purpose: Hierarchical concept representation with bidirectional linking
- Examples: `# [[#^chapter|CHAPTER 1: What Is Operations Research (OR)?]]`
- Pattern: Uses `[[#^anchorId|Display Name]]` syntax for Obsidian block references

**Block Anchor:**
- Purpose: Unique identifier linking body text to markmap nodes
- Examples: `^chapter`, `^wwii`, `^postwar`
- Pattern: Letter-only IDs (A-Za-z) placed at end of paragraphs

**Image Asset:**
- Purpose: Visual figures from textbook
- Examples: `bo_d56m41n7aajc73800n1g_5_348_1687_1169_477_0.jpg`
- Pattern: Standardized naming with book/page/figure encoding

**Processing Skill:**
- Purpose: Reusable content transformation logic
- Examples: `.trae/skills/obsidian-markmap-processor/SKILL.md`
- Pattern: YAML frontmatter with metadata + markdown documentation

## Entry Points

**Chapter Content Files:**
- Location: `CHAPTER [NUMBER] [Topic Name]/CHAPTER [NUMBER] [Topic Name].md`
- Triggers: Obsidian file open, markmap plugin render
- Responsibilities: Main content delivery, markmap definition, anchor targets

**Skill Definitions:**
- Location: `.trae/skills/obsidian-markmap-processor/SKILL.md`
- Triggers: AI agent invocation, manual processing requests
- Responsibilities: Define transformation logic for markmap generation and linking

**Planning Documents:**
- Location: `.trae/documents/plan_*.md`
- Triggers: Planning phase workflows
- Responsibilities: Track transformation tasks and execution plans

**Codebase Analysis Documents:**
- Location: `.planning/codebase/ARCHITECTURE.md`, `.planning/codebase/STRUCTURE.md`
- Triggers: GSD mapping commands
- Responsibilities: Document architecture for other phases

## Error Handling

**Strategy:** Static content with transformation-time validation

**Patterns:**
- HTML table conversion failures: Tables remain in HTML format, logged for manual review
- Block anchor conflicts: Letter-only IDs prevent numeric collisions; uniqueness validated during link creation
- Missing image references: Obsidian shows broken image placeholder; no runtime failure
- Markmap rendering errors: Displayed as raw code block if markmap plugin unavailable

## Cross-Cutting Concerns

**Linking:** Bidirectional Obsidian block references using `[[#^anchorId|Display Name]]`` syntax
**Validation:** Block anchor uniqueness checked during processing; letter-only IDs enforced
**Content Preservation:** Original content maintained during transformations; HTML tables converted to markdown
**Version Control:** Git tracks content changes; `.trae/` and `.planning/` excluded from commits via `.gitignore`
**Multi-language Support:** Alias definitions in separate files provide Chinese alternatives

---

*Architecture analysis: 2025-02-02*
