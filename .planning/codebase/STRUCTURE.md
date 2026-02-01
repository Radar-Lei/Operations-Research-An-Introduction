# Codebase Structure

**Analysis Date:** 2025-02-02

## Directory Layout

```
[project-root]/
├── [CHAPTER N <Topic>/]          # Chapter content directories (21 chapters)
├── [APPENDIX <Name>/]            # Appendix materials (2 appendices)
├── [.planning/]                  # Planning and analysis output
│   └── [codebase/]               # Codebase architecture documentation
├── [.trae/]                      # Process automation (git-ignored)
│   ├── [skills/]                 # Agent skill definitions
│   └── [documents/]              # Execution plans and workflow docs
├── [.git/]                       # Git repository
└── [.gitignore]                  # Git exclusions
```

## Directory Purposes

**CHAPTER N <Topic>:**
- Purpose: Self-contained educational unit for Operations Research topic
- Contains: Primary markdown file, images subdirectory, optional _resources
- Key files: `[CHAPTER N <Topic>.md]`, `[images/*.jpg]`, `[_resources/]`

**APPENDIX <Name>:**
- Purpose: Supplementary reference materials (statistical tables, answer keys)
- Contains: Primary markdown file, images subdirectory
- Key files: `[APPENDIX <Name>.md]`, `[images/*.jpg]`

**.planning/codebase:**
- Purpose: Architecture analysis and structure documentation (this directory)
- Contains: Analysis outputs (ARCHITECTURE.md, STRUCTURE.md, etc.)
- Key files: `[ARCHITECTURE.md]`, `[STRUCTURE.md]`

**.trae:**
- Purpose: Agent workflow automation and skill definitions
- Contains: Skills for markdown/markmap processing, execution plans
- Key files: `[skills/*/SKILL.md]`, `[documents/plan_*.md]`
- Generated: Yes (during workflow execution)
- Committed: No (excluded by .gitignore)

## Key File Locations

**Entry Points:**
- `CHAPTER 1 What Is Operations Research?/CHAPTER 1 What Is Operations Research?.md`: Introduction to OR concepts
- `CHAPTER 2 Modeling with Linear Programming/CHAPTER 2 Modeling with Linear Programming.md`: LP fundamentals
- `CHAPTER 3 The Simplex Method and Sensitivity Analysis/CHAPTER 3 The Simplex Method and Sensitivity Analysis.md`: Core algorithm

**Configuration:**
- `.gitignore`: Excludes `.trae/` directory from version control

**Core Logic:**
- All chapter markdown files: Educational content (21 chapters covering LP, DP, networks, queuing, etc.)
- Appendix files: Statistical tables, partial answers to problems

**Testing:**
- Not applicable (static documentation vault)

**Images:**
- `CHAPTER 1 What Is Operations Research?/images/bo_d56m41n7aajc73800n1g_5_348_1687_1169_477_0.jpg`: Figures and diagrams
- Similar `images/` subdirectories in each chapter/appendix

## Naming Conventions

**Files:**
- Markdown: `[Topic Name].md` (matches directory name)
- Pattern: Descriptive, space-separated, capital case
- Examples: `CHAPTER 2 Modeling with Linear Programming.md`

**Directories:**
- Chapters: `CHAPTER N <Topic>` where N is chapter number
- Appendices: `APPENDIX <Name>` or `APPENDIX <Name> <Description>`
- Pattern: Numeric prefix + descriptive name
- Examples: `CHAPTER 12 Deterministic Dynamic Programming`, `APPENDIX A Statistical Tables`

**Block IDs (within markdown):**
- Pattern: Letter-only identifiers (no numbers, underscores, hyphens)
- Examples: `^introduction`, `^models`, `^solving`
- Format: Caret prefix + lowercase letters

## Where to Add New Code

**New Chapter:**
- Primary content: `CHAPTER N <Topic>/CHAPTER N <Topic>.md`
- Images: `CHAPTER N <Topic>/images/`
- Resources: `CHAPTER N <Topic>/_resources/`

**New Appendix:**
- Implementation: `APPENDIX <Name>/APPENDIX <Name>.md`
- Images: `APPENDIX <Name>/images/`

**New Skill:**
- Implementation: `.trae/skills/<skill-name>/SKILL.md`
- Documentation: Include capabilities, usage patterns, examples

**Utilities/Plans:**
- Shared helpers: `.trae/documents/plan_<timestamp>.md` (execution tracking)

## Special Directories

**.trae:**
- Purpose: Agent automation infrastructure (skills, plans)
- Generated: Partially (plans are generated, skills are manual)
- Committed: No (excluded by .gitignore)

**.planning/codebase:**
- Purpose: Architecture analysis output
- Generated: Yes (by codebase mapper agent)
- Committed: Yes (tracked in git)

**_resources (within chapters):**
- Purpose: Embedded resources for Obsidian compatibility
- Generated: Yes (by Obsidian)
- Committed: Yes (typically)

---

*Structure analysis: 2025-02-02*
