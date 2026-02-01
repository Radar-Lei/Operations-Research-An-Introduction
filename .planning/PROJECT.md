# 运筹学知识库 Markmap 增强

## What This Is

为《运筹学导论》知识库的章节添加 markmap 思维导图，提供层次化的知识导航和快速内容定位。这是一个基于 Obsidian 的个人学习知识库，使用 markmap 插件可视化章节结构。

## Core Value

每个章节都有完整的 markmap 思维导图，与正文内容双向链接，实现快速导航和知识关联。

## Requirements

### Validated

- ✓ Markdown 格式的章节内容（21章 + 2附录）
- ✓ Obsidian 知识库集成
- ✓ Markmap 插件已安装
- ✓ 图像存储在 images/ 子目录
- ✓ 现有章节包含 markmap 示例（第1章等）

### Active

- [ ] 为第12章添加完整的 markmap 代码块
- [ ] markmap 包含所有主要小节（12.1-12.4）
- [ ] markmap 包含所有5个DP应用模型
- [ ] markmap 包含所有例题节点
- [ ] 正文段落添加块锚点（^xxx 格式，仅字母）
- [ ] markmap 节点使用 [[#^xxx|显示名]] 链接到正文
- [ ] 格式与第1章保持一致
- [ ] markmap 高度设置为合适的值

### Out of Scope

- 修改其他章节的内容
- 修改第12章的正文内容（只添加 markmap 和锚点）
- 修改章节结构或重新组织内容
- 处理其他章节（仅第12章）

## Context

**现有知识库结构：**
- 21个章节目录 + 2个附录
- 每个章节包含：主 .md 文件、images/ 子目录
- 已有代码库映射：.planning/codebase/ (ARCHITECTURE.md, STRUCTURE.md, STACK.md)
- 现有 skill：.trae/skills/obsidian-markmap-processor/

**第12章内容：**
- 标题：Deterministic Dynamic Programming（确定性动态规划）
- 主要小节：
  - 12.1 递归性质（含最短路径例题）
  - 12.2 前向和后向递归（含例题）
  - 12.3 DP应用（5个模型：背包、劳动力、设备更换、投资、库存）
  - 12.4 维度灾难问题（含例题）

**参考格式：**
- 第1章有完整的 markmap 作为模板
- 使用 YAML frontmatter 设置 markmap 高度
- 层次结构：# ## ### 对应章节-小节-子小节
- 例题独立节点

**已知约束：**
- 块锚点 ID 必须仅包含字母（无数字、下划线、连字符）
- markmap 代码块在文件顶部
- 双向链接语法：[[#^anchorId|Display Name]]

## Constraints

- **格式**: 必须与第1章 markmap 格式保持一致 — 确保视觉和功能一致性
- **锚点规则**: 块锚点 ID 仅限字母 [A-Za-z]+ — Obsidian 链接语法要求
- **工具**: 使用 Obsidian markmap 插件渲染 — 现有基础设施
- **范围**: 仅处理第12章 — 避免范围蔓延

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| 完整详细的 markmap | 第12章内容丰富，5个DP模型需要清晰导航 | — Pending |
| 包含所有例题节点 | DP是方法性内容，例题展示算法步骤 | — Pending |
| 双向链接到正文 | 与已有章节保持一致，提供快速跳转 | — Pending |

---
*Last updated: 2025-02-01 after initialization*
