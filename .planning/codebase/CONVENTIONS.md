# Coding Conventions

**Analysis Date:** 2025-02-02

## Project Type

This is an **Obsidian Vault** for academic notes, not a traditional software codebase. The content consists of:

- Markdown notes (.md files)
- Image resources (PNG/JPG files in `images/` subdirectories)
- Markmap mind map definitions
- Obsidian block references

## Naming Patterns

**Files:**
- Chapter notes: `{CHAPTER/APPENDIX NUMBER} {Topic}.{ext}` (e.g., `CHAPTER 1 What Is Operations Research?.md`)
- Resources: `images/` subdirectory per chapter
- Block IDs: Letter-only anchors (e.g., `^chapter`, `^wwii`, `^introduction`)

**Directories:**
- Pattern: `{CHAPTER/APPENDIX NUMBER} {Topic}/` (exact match to main subject)
- All chapter folders follow numbered sequence (1-21)
- Each chapter contains an `images/` subdirectory

**Block Anchors:**
- Format: `^[letters]` - ONLY letters allowed [A-Za-z]+
- No numbers, underscores, or hyphens in block IDs
- Must be unique within each file
- Placed at END of paragraph/section

## Markdown Structure

**Header Levels:**
```
# CHAPTER/Topic level           ## Main sections
### Subsections                 #### Details
```

**Markmap Integration:**
- Markmap code blocks at top of file
- Uses YAML frontmatter with `height: 643` or similar
- Bidirectional linking: `[[#^anchorId|Display Name]]`

**Mathematical Notation:**
- Inline: `$formula$`
- Display: `$$formula$$`
- LaTeX syntax for mathematical expressions

**Link Formats:**
- Internal block refs: `[[#^anchorId|Display Text]]`
- Same-file links: `[[#heading|Display Text]]`
- Cross-file: `[[File Name|Display Text]]`

## Code Style

**Formatting:**
- No formal linter configured
- Manual formatting following Obsidian best practices
- Standard Markdown syntax

**Table Format:**
```markdown
| Header 1 | Header 2 |
|----------|----------|
| Cell     | Cell     |
```
- Pipe `|` delimiters
- Header separator with `|---|` or alignment markers
- Right-align numbers: `|---:|`

## Block ID Conventions

**Generation Rules:**
- Use descriptive names: `^introduction`, `^problemdefinition`
- Compound words: `^airtickets`, `^gardenfencing`, `^sensitivity`
- Abbreviations: `^wwii`, `^ada`, `^or` (for "Operations Research")
- Always lowercase letters only

**Placement:**
- At end of paragraph/section
- Before blank line if present
- After punctuation

**Examples from codebase:**
```
The first formal activities of Operations Research (OR) were initiated in England during World War II. ^wwii

This chapter introduces the basic terminology of OR. ^terminology

It stresses that defining the problem correctly is the most important phase. ^problemdefinition
```

## Markmap Node Conventions

**Link Syntax:**
- Always use bidirectional format: `[[#^anchorId|Display Name]]`
- Display name excludes LaTeX formulas
- Preserve header levels (#, ##, ###)

**Example:**
```markdown
## [[#^wwii|Origins & Purpose]]
### Started in WWII Britain: scientific allocation of war resources
```

## Image Conventions

**Naming:**
- Auto-generated names: `bo_d56m3qjef24c73bhe5mg_15_483_200_715_417_0.jpg`
- Stored in chapter-specific `images/` subdirectories
- Relative references from markdown files

**Syntax:**
```markdown
![alt text](images/filename.jpg)
```

## File Organization

**Chapter Structure:**
```
CHAPTER N Topic/
├── CHAPTER N Topic.md          # Main note file
├── images/                      # Image resources
│   └── *.jpg
└── _resources/                  # Additional resources (some chapters)
```

**Special Directories:**
- `.trae/` - Configuration for AI assistant (ignored by git)
- `.planning/` - Project planning documents (ignored by git)
- `.git/` - Git repository

## Content Patterns

**Section Transitions:**
- Numbered sections (e.g., `### 1.1 INTRODUCTION`)
- Anchor IDs tied to sections
- Block references from markmap

**Bibliography:**
- Standard academic format
- At end of chapter files
- Numeric citations `${}^{1}$`

**Problems:**
- Numbered lists starting from 1
- Sub-problems with (a), (b), etc.
- Difficulty markers: `*` for challenging problems

## Import Organization

Not applicable - no code imports in this markdown documentation vault.

## Error Handling

Not applicable - documentation project with no executable code.

## Logging

Not applicable - no application code.

## Comments

**When to Comment:**
- Block IDs serve as inline anchors
- Markmap nodes provide structural commentary
- HTML comments avoided in favor of markdown syntax

## JSDoc/TSDoc

Not applicable - markdown content, not typed code.

## Function Design

Not applicable - no functions in markdown documentation.

## Module Design

**Exports:**
- Not applicable - static markdown files

**Barrel Files:**
- Not applicable

---

*Convention analysis: 2025-02-02*
