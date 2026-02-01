# External Integrations

**Analysis Date:** 2025-02-02

## APIs & External Services

**None detected**

This is a local-first Obsidian vault with no external API integrations. All content is stored as markdown files locally and synchronized via OneDrive cloud storage.

## Data Storage

**Primary Storage:**
- Local filesystem markdown files (`.md`)
- Location: Obsidian vault root directory
- Organized by chapter directories (e.g., `CHAPTER 1 What Is Operations Research?/`)

**Cloud Storage:**
- OneDrive (Personal)
- Path: `/Users/leida/Library/CloudStorage/OneDrive-Personal/Obsidian/Books/OR/Intro/Operations Research An Introduction`
- Syncs entire vault across devices

**File Storage:**
- Local filesystem only
- No external file storage services

**Caching:**
- None (Obsidian handles caching internally)

## Authentication & Identity

**Auth Provider:**
- None (local-only vault)
- No user accounts or authentication required
- OneDrive handles authentication for cloud sync (operating system level)

**Implementation:**
- Direct filesystem access
- No login/authentication within the vault

## Monitoring & Observability

**Error Tracking:**
- None

**Logs:**
- None (Obsidian may have internal logs, but not vault-level)
- No custom logging implemented

## CI/CD & Deployment

**Hosting:**
- Local files (not hosted)
- OneDrive provides cloud backup and sync
- Obsidian Community Publish could be used for publishing (not currently configured)

**CI Pipeline:**
- Git for version control (GitHub or other git host)
- Branch: `main`
- Recent commits show document update workflow

**Build Process:**
- None (static markdown files)

## Environment Configuration

**Required env vars:**
- None

**Secrets location:**
- No secrets required for vault operation

**Configuration Files:**
- `.gitignore` - Specifies that `.trae/` directory should not be committed
- `.trae/` directory contains AI assistant skills (excluded from git)

## Webhooks & Callbacks

**Incoming:**
- None

**Outgoing:**
- None

**External References:**
The markdown files contain HTTP/HTTPS URLs as bibliographic references and footnotes, including:
- Academic journal references (e.g., INFORMS Interfaces journal)
- Educational resources (e.g., university TSP problem databases)
- News articles and blog posts

These are reference links only, not active integrations.

## Special Integrations

**markmap Visualization:**
- Renders mind maps from markdown code blocks
- Format: ```markmap``` blocks with YAML configuration
- Supports:
  - Hierarchical node structures
  - LaTeX formulas (`$$` and `$` delimiters)
  - Bidirectional links to content via `[[#^anchorId|Display Name]]` syntax
  - Custom height configuration (e.g., `height: 643`)

**Bidirectional Linking (Obsidian-native):**
- Wiki-links: `[[filename]]` or `[[#^blockId]]`
- Block IDs: `^anchorId` placed at end of paragraphs
- Markmap nodes link to body content via `[[#^anchorId|Display Name]]`

**.trae AI Assistant Framework:**
- Location: `.trae/skills/` and `.trae/documents/`
- Custom skill definition format with YAML frontmatter
- Example skill: `obsidian-markmap-processor` for processing markmap diagrams
- Document plans stored as markdown (e.g., `plan_20260130_081836.md`)

## Content Sources

**Primary Source Material:**
- Textbook: "Operations Research: An Introduction"
- Content organized into 21 chapters plus 2 appendices
- Chapter topics include:
  - Linear Programming (Chapters 2-4, 7)
  - Network Models (Chapter 6)
  - Integer Programming (Chapter 9)
  - Heuristic Programming (Chapter 10)
  - Traveling Salesperson Problem (Chapter 11)
  - Dynamic Programming (Chapter 12)
  - Inventory Models (Chapters 13, 16)
  - Probability (Chapter 14)
  - Decision Analysis (Chapter 15)
  - Markov Chains (Chapter 17)
  - Queuing Systems (Chapter 18)
  - Simulation (Chapter 19)
  - Optimization Theory (Chapters 20-21)
  - Statistical Tables (Appendix A)
  - Selected Answers (Appendix B)

---

*Integration audit: 2025-02-02*
