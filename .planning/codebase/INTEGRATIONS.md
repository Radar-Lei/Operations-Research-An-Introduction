# External Integrations

**Analysis Date:** 2025-02-02

## APIs & External Services

**无检测到**

此项目是纯静态 Markdown 笔记库，不使用任何外部 API 或服务。

## Data Storage

**Databases:**
- 无（基于文件系统的 Markdown 存储）

**File Storage:**
- OneDrive (Microsoft OneDrive) - 云同步存储
  - 路径: `/Users/leida/Library/CloudStorage/OneDrive-Personal/Obsidian/Books/OR/Intro/Operations Research An Introduction`
  - 用途: 笔记备份和跨设备同步

**Caching:**
- 无

## Authentication & Identity

**Auth Provider:**
- 无（本地笔记系统）

**身份验证:**
- OneDrive 账户（用于云同步）
- 无应用级别身份验证

## Monitoring & Observability

**Error Tracking:**
- 无

**Logs:**
- 无（静态文件，无日志记录）

## CI/CD & Deployment

**Hosting:**
- 本地 Obsidian 应用
- OneDrive 云存储

**CI Pipeline:**
- 无（手动编辑笔记）

**自动化:**
- `.trae/skills/obsidian-markmap-processor/SKILL.md` - 自定义笔记处理技能
  - 处理 markmap 代码块
  - 创建思维导图
  - 建立正文与思维导图的双向锚点链接
  - 标准化表格格式

## Environment Configuration

**Required env vars:**
- 无

**Secrets location:**
- 无敏感信息

## Webhooks & Callbacks

**Incoming:**
- 无

**Outgoing:**
- 无

## Third-Party Tools

**Obsidian Plugins:**
- Markmap - 思维导图可视化
  - 用途: 将 markmap 代码块渲染为交互式思维导图
  - 配置: 在每个笔记文件中通过 YAML frontmatter 配置高度

**Version Control:**
- Git - 本地版本控制
  - 仓库: `/Users/leida/Library/CloudStorage/OneDrive-Personal/Obsidian/Books/OR/Intro/Operations Research An Introduction/.git`
  - 当前分支: main

## Content Integration

**教材来源:**
- "Operations Research: An Introduction" (运筹学导论)
- 包含 21 章内容 + 附录

**笔记结构:**
- 每章独立目录
- 每章包含主 Markdown 文件和配套图片
- 使用 markmap 思维导图总结章节内容
- 使用 Obsidian 块锚点 (`^anchorId`) 建立双向链接

---

*Integration audit: 2025-02-02*
