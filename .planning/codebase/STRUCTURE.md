# Codebase Structure

**Analysis Date:** 2025-02-02

## Directory Layout

```
[project-root]/
├── .git/                    # Git repository metadata
├── .gitignore               # Excludes .trae/ and .planning/
├── .planning/               # Planning and codebase analysis documents
│   └── codebase/           # Architecture and structure documentation
├── .trae/                  # AI agent processing artifacts
│   ├── documents/          # Execution plans and task lists
│   └── skills/             # Reusable processing skill definitions
│       └── obsidian-markmap-processor/
│           └── SKILL.md    # Markmap processing instructions
├── CHAPTER 1 What Is Operations Research?/
│   ├── CHAPTER 1 What Is Operations Research?.md
│   ├── sensitivity analysis.md
│   ├── images/             # Chapter-specific figures
│   └── _resources/         # Additional resources
├── CHAPTER 2 Modeling with Linear Programming/
│   ├── CHAPTER 2 Modeling with Linear Programming.md
│   └── images/
├── [CHAPTER 3-21]          # Similar structure for each chapter
├── APPENDIX A Statistical Tables/
│   └── images/
└── APPENDIX B Partial Answers to Selected Problems1/
    └── images/
```

## Directory Purposes

**Root Directory:**
- Purpose: Container for entire Obsidian vault
- Contains: 21 chapter directories, 2 appendix directories, configuration directories
- Key files: `.gitignore`, chapter markdown files

**`.planning/`:**
- Purpose: Stores planning artifacts and codebase analysis
- Contains: `codebase/` subdirectory with architecture documents
- Generated: Yes (by GSD mapping commands)
- Committed: No (excluded by `.gitignore`)

**`.trae/`:**
- Purpose: AI agent workspace for processing tasks
- Contains: Execution plans, skill definitions, processing artifacts
- Generated: Yes (by AI agents and planning workflows)
- Committed: No (excluded by `.gitignore`)

**`.trae/documents/`:**
- Purpose: Execution plans and task lists for content processing
- Contains: `plan_*.md` files with Chinese and English task descriptions
- Key files: `plan_20260130_081836.md`, `Process Chapter 12 - Deterministic Dynamic Programming Note.md`

**`.trae/skills/`:**
- Purpose: Reusable skill definitions for automated content transformation
- Contains: Named skill directories with SKILL.md files
- Key files: `obsidian-markmap-processor/SKILL.md`

**`CHAPTER [NUMBER] [Topic Name]/`:**
- Purpose: Self-contained chapter content with associated resources
- Contains: Main markdown file, images, optional supplementary files
- Key files: `CHAPTER [NUMBER] [Topic Name].md` (main content), `images/*.jpg`
- Generated: No (manually created or imported)
- Committed: Yes

**`APPENDIX [LETTER] [Topic Name]/`:**
- Purpose: Supplementary materials (statistical tables, problem answers)
- Contains: Main markdown file, images
- Key files: `APPENDIX [LETTER] [Topic Name].md`, `images/*.jpg`
- Generated: No
- Committed: Yes

**`images/` (within chapters):**
- Purpose: Chapter-specific visual assets from textbook
- Contains: JPG images with standardized naming pattern
- Naming pattern: `bo_d56m[a-z0-9_]+.jpg` (encodes book/page/figure info)
- Generated: No (imported from source)
- Committed: Yes

**`_resources/` (within some chapters):**
- Purpose: Additional resources or nested directory structures
- Contains: Varies by chapter (some chapters have this, others don't)
- Generated: No
- Committed: Yes

## Key File Locations

**Entry Points:**
- `CHAPTER 1 What Is Operations Research?/CHAPTER 1 What Is Operations Research?.md`: Introduction to OR concepts
- `CHAPTER 2 Modeling with Linear Programming/CHAPTER 2 Modeling with Linear Programming.md`: LP modeling foundations
- `.trae/skills/obsidian-markmap-processor/SKILL.md`: Content transformation skill definition

**Configuration:**
- `.gitignore`: Git exclusions (`.trae/`, `.planning/`)

**Core Logic:**
- `CHAPTER [N] [Topic]/CHAPTER [N] [Topic].md`: All chapter content (21 chapters)
- Each chapter file contains: markmap code block, body text with block anchors, LaTeX formulas, tables

**Testing:**
- Not applicable (static content vault)

## Naming Conventions

**Files:**
- Chapter markdown: `CHAPTER [NUMBER] [Full Topic Name].md` (matches directory name)
- Appendix markdown: `APPENDIX [LETTER] [Full Topic Name].md` (matches directory name)
- Images: `bo_d56m[a-z0-9_]+.jpg` (machine-generated, includes book/page/figure encoding)
- Skills: `SKILL.md` (uppercase, in skill-named subdirectory)
- Plans: `plan_YYYYMMDD_HHMMSS.md` (timestamped) or descriptive name with `.md` extension

**Directories:**
- Chapters: `CHAPTER [NUMBER] [Full Topic Name]/` (number + title, space-separated)
- Appendices: `APPENDIX [LETTER] [Full Topic Name]/` (letter + title, space-separated)
- Skills: Descriptive lowercase hyphenated name (e.g., `obsidian-markmap-processor/`)
- Planning: `.planning/codebase/`, `.trae/documents/`, `.trae/skills/`

## Where to Add New Code

**New Chapter:**
- Primary code: Create `CHAPTER [N] [Topic Name]/CHAPTER [N] [Topic Name].md`
- Images: Place in `CHAPTER [N] [Topic Name]/images/`
- Follow structure: Include markmap code block at top, body text with block anchors

**New Appendix:**
- Implementation: Create `APPENDIX [LETTER] [Topic Name]/APPENDIX [LETTER] [Topic Name].md`
- Images: Place in `APPENDIX [LETTER] [Topic Name]/images/`

**New Processing Skill:**
- Implementation: Create `.trae/skills/[skill-name]/SKILL.md`
- Follow pattern: YAML frontmatter + markdown documentation (see `obsidian-markmap-processor/SKILL.md`)

**New Execution Plan:**
- Implementation: Create `.trae/documents/plan_YYYYMMDD_HHMMSS.md` or descriptive `.md` file
- Can be in English or Chinese (existing plans use both)

**Codebase Analysis:**
- Implementation: `.planning/codebase/[DOCUMENT].md` (e.g., `ARCHITECTURE.md`, `STRUCTURE.md`)
- Use templates from GSD mapper agent

**Utilities:**
- Shared helpers: Not applicable (no code utilities, this is a content vault)

**Supplementary Notes:**
- Implementation: Place `.md` file within appropriate chapter directory
- Example: `CHAPTER 1 What Is Operations Research?/sensitivity analysis.md`
- Use YAML frontmatter for aliases if multi-language support needed

## Special Directories

**`.planning/`:**
- Purpose: GSD planning system workspace
- Generated: Yes
- Committed: No (excluded by `.gitignore`)

**`.trae/`:**
- Purpose: AI agent workspace for task execution
- Generated: Yes
- Committed: No (excluded by `.gitignore`)

**`.git/`:**
- Purpose: Git version control metadata
- Generated: Yes (by `git init`)
- Committed: N/A (version control database)

**`_resources/` (within chapters):**
- Purpose: Additional chapter resources (usage varies)
- Generated: No
- Committed: Yes

---

*Structure analysis: 2025-02-02*
