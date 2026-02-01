# Architecture

**Analysis Date:** 2025-02-02

## Pattern Overview

**Overall:** Hierarchical Knowledge Base (Obsidian Vault)

**Key Characteristics:**
- Flat directory structure with chapter-based organization
- Markdown-based documentation with embedded mind maps (markmap)
- Bidirectional linking between conceptual hierarchy and content
- Separation of content (chapters) from process metadata (.trae)

## Layers

**Content Layer:**
- Purpose: Educational content storage for Operations Research textbook
- Location: `[CHAPTER N <Topic>/, APPENDIX <Name>/]`
- Contains: Chapter notes, examples, problems, and supplementary materials
- Depends on: Markdown rendering, markmap visualization
- Used by: Obsidian reader, markmap processor skill

**Visualization Layer:**
- Purpose: Conceptual mapping and knowledge navigation
- Location: Embedded in each chapter's markdown file
- Contains: Hierarchical mind maps in markmap code blocks
- Depends on: Content layer (anchors to body text)
- Used by: Obsidian markmap plugin, skill processor

**Resource Layer:**
- Purpose: Asset storage (images, embedded resources)
- Location: `[images/, _resources/]` subdirectories within chapters
- Contains: Figures, diagrams, and auxiliary files
- Depends on: File system
- Used by: Markdown rendering (image references)

**Process Layer:**
- Purpose: Automation and skill definitions for content processing
- Location: `[.trae/]`
- Contains: Skill definitions, execution plans, and process documentation
- Depends on: Content layer (input files)
- Used by: Agent execution system

## Data Flow

**Content Creation Flow:**

1. Chapter markdown files created with content (definitions, examples, problems)
2. Markmap code blocks generated/edited to reflect chapter structure
3. Block anchors (`^id`) added to body text sections
4. Markmap nodes linked to anchors via `[[#^id|display name]]` syntax
5. Images stored in `images/` subdirectories and referenced in markdown

**Skill Processing Flow:**

1. Skill invoked on markdown file (e.g., obsidian-markmap-processor)
2. File parsed to extract existing markmap structure
3. Block IDs generated/validated for body text sections
4. Markmap nodes updated with bidirectional links
5. Tables standardized to markdown format
6. Modified file written back

**State Management:**
- Static content storage (no runtime state)
- Git-tracked changes for version control
- Process plans stored in `.trae/documents/` for workflow tracking

## Key Abstractions

**Chapter:**
- Purpose: Self-contained unit of OR knowledge
- Examples: `CHAPTER 1 What Is Operations Research?/`, `CHAPTER 12 Deterministic Dynamic Programming/`
- Pattern: One primary markdown file + optional assets subdirectory

**Markmap Node:**
- Purpose: Hierarchical concept representation with bidirectional linking
- Examples: `# [[#^chapter|CHAPTER 1: What Is Operations Research?]]`
- Pattern: Obsidian wiki-link syntax with block ID anchor

**Block Anchor:**
- Purpose: Linkable reference point in body text
- Examples: `^introduction`, `^models`, `^solving`
- Pattern: Caret + letter-only identifier at paragraph end

**Skill:**
- Purpose: Automated content processing capability
- Examples: `obsidian-markmap-processor`
- Pattern: YAML frontmatter + markdown documentation

## Entry Points

**Chapter Files:**
- Location: `[CHAPTER N <Topic>/<CHAPTER N <Topic>.md>]`
- Triggers: User opens in Obsidian or invokes skill
- Responsibilities: Content delivery, mind map visualization, knowledge navigation

**Skill Definitions:**
- Location: `[.trae/skills/<skill-name>/SKILL.md]`
- Triggers: Agent invocation based on user request
- Responsibilities: Define processing capabilities, execution patterns

**Execution Plans:**
- Location: `[.trae/documents/plan_<timestamp>.md]`
- Triggers: Generated during workflow execution
- Responsibilities: Track pending tasks, document transformation steps

## Error Handling

**Strategy:** Manual validation with skill-assisted checks

**Patterns:**
- Unique block ID enforcement (letter-only, no duplicates within file)
- Markmap-to-body anchor validation during skill execution
- HTML table conversion to markdown for rendering consistency

## Cross-Cutting Concerns

**Linking:** Obsidian wiki-link syntax `[[#^anchor|display]]` for bidirectional navigation

**Mathematical Notation:** LaTeX delimiters (`$$`, `$`) embedded in markdown for formulas

**Language:** Mixed English content with Chinese process documentation in `.trae/`

**Version Control:** Git with `.trae/` excluded (per `.gitignore`)

---

*Architecture analysis: 2025-02-02*
