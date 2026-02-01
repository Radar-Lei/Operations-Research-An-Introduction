# Coding Conventions

**Analysis Date:** 2025-02-02

## Project Type

**Obsidian Knowledge Base / Markdown Documentation**

This is a documentation project for an Operations Research textbook, not a traditional software codebase. The conventions below describe the markdown and Obsidian-specific patterns used throughout the notes.

## Naming Patterns

**Files:**
- Chapter files: Pattern `CHAPTER {Number} {Title}.md` within matching directory
- Appendix files: Pattern `APPENDIX {Letter} {Title}.md` within matching directory
- Example: `CHAPTER 12 Deterministic Dynamic Programming/CHAPTER 12 Deterministic Dynamic Programming.md`
- Note files: lowercase with spaces: `sensitivity analysis.md`
- Directory names match their primary file name exactly

**Directories:**
- Pattern: `{Type} {Number} {Title}/` or `{Type} {Title}/`
- Chapter directories: `CHAPTER 1 What Is Operations Research?/`
- Appendix directories: `APPENDIX A Statistical Tables/`
- Subdirectories: `images/` for chapter images, `_resources/` for embedded resources

**Block IDs (Anchors):**
- Pattern: `^[a-zA-Z]+` - letters only, no numbers, hyphens, or underscores
- Unique within each file
- Placed at end of paragraphs/sections
- Examples: `^chapter`, `^recursive`, `^knapsackmodel`, `^weyerhaeuser`

## Code Style

**Markdown Structure:**
- Level 1 headers (`#`) for chapter titles in markmap
- Level 2-6 headers (`##` through `######`) for body content hierarchy
- Space after `#` in headers: `## Header Title` (not `##Header Title`)

**Markmap Code Blocks:**
```markdown
```markmap
---
markmap:
  height: 643
---
# [[#^anchorId|Display Name]]
## [[#^anchorId|Subtitle]]
### [[#^anchorId|Section]]
```
```
- Height commonly: 643 or 720 pixels
- Uses YAML frontmatter within code block
- All nodes link to body text via `[[#^anchorId|Display Name]]` format

**LaTeX/Math Notation:**
- Inline math: `$...$` single dollar signs
- Display math: `$$...$$` double dollar signs on separate lines
- Example: `$f_i(x_i) = \max\{r_im_i + f_{i+1}(x_i - w_im_i)\}$`

**Tables:**
- Standard markdown pipe format: `| Header | Header |`
- Alignment row: `|---|---:|---:|` (left, right, right)
- No trailing spaces after pipe separators
- HTML `<table>` tags should be converted to markdown format

## Import Organization

**Obsidian Wiki Links:**
- Internal links: `[[filename]]` or `[[filename|Display Text]]`
- Block references: `[[#^anchorId]]` or `[[#^anchorId|Display Text]]`
- Headers as anchors: `[[#header]]` format

**Image References:**
- Relative paths: `![alt text](images/filename.jpg)`
- Obsidian embed format: `![[image-filename]]` also used

**Aliases (Frontmatter):**
```markdown
---
aliases:
  - Alternative Name
  - 别名
---
```

## Error Handling

**No Error Handling Required**
This is static documentation. No code execution means no runtime error handling patterns.

**Content Validation:**
- All markmap node links must have corresponding block IDs in body text
- Block IDs must be unique within file
- Block IDs must contain only letters `[A-Za-z]+`

## Logging

**Not Applicable**
Static markdown documentation does not use logging.

## Comments

**Markdown Comments:**
- HTML comments: `<!-- comment -->`
- Used sparingly in this codebase

**Block ID "Comments":**
- Block IDs serve as inline anchors, not traditional comments
- Placed at end of content blocks to enable linking from markmap

## Frontmatter

**YAML Frontmatter Pattern:**
```markdown
---
aliases:
  - English Alias
  - Chinese Alias
---
```

**Obsidian Properties:**
- `aliases`: array of alternative titles
- Used primarily for shorter note files, not main chapter files

## Function Design

**Not Applicable**
No executable functions - this is a documentation repository.

## Module Design

**Chapter File Structure:**
1. Level 2 header with chapter title and block ID: `## CHAPTER X Title ^anchor`
2. Summary section (if present): bullet points of key concepts
3. Markmap code block with hierarchical mind map
4. Body content with:
   - Real-life application section
   - Numbered sections (e.g., `### 12.1 Recursive Nature`)
   - Examples with headers
   - Formulas in LaTeX
   - Tables in markdown format
   - Case studies at end
   - Problems section

**Section Organization:**
- Main sections: `## Section Title ^anchorId`
- Subsections: `### Subsection Title ^anchorId`
- Examples: `## Example X.Y-Z (Description) ^anchorId`
- Real-life applications: `## Real-Life Application—Title ^anchorId`

**Markmap Integration:**
- Markmap comes after summary (or at top if no summary)
- Every markmap node links to body text via `[[#^anchorId|Display Name]]`
- Block IDs placed at end of corresponding paragraphs in body

## Link Patterns

**Bidirectional Linking:**
- Markmap node: `### [[#^knapsack|Knapsack Model]]`
- Body text: ends with `^knapsack`
- This creates clickable mindmap navigation

**Cross-Chapter References:**
- Use `[[Chapter File Name]]` format
- Can include block reference: `[[Chapter File Name#^anchorId]]`

## Content Localization

**Language:**
- Primary: English (chapter content)
- Secondary: Chinese (planning documents in `.trae/`)
- Aliases may include Chinese translations

**Numbering:**
- Chapter sections use decimal notation: `12.3.1`, `12.3.2`, etc.
- Examples use chapter.example format: `Example 12.3-1`
- Problems use section notation: `Problems (8-1–8-25)`

## Special Patterns

**Aha! Moment Sections:**
- Pattern: `## Aha! Moment: Title`
- Historical context or interesting facts
- Examples: "Aha! Moment: Ada Lovelace & Algorithms", "Aha! Moment: Spammers Go Markovian!"

**Real-Life Application Sections:**
- Pattern: `## Real-Life Application—Title ^anchor`
- Case studies from industry
- Include year, company, and savings/impact when available

**Excel/Software Moments:**
- Pattern: `### Excel Moment` or `### AMPL Moment` or `### TORA Moment`
- Refer to spreadsheet files or software implementations

**Case Studies:**
- Located at end of chapters
- Detailed problem descriptions
- Mathematical model formulation
- Analysis and results

---

*Convention analysis: 2025-02-02*
