# Requirements: 运筹学知识库 Markmap 增强

**Defined:** 2025-02-01
**Core Value:** 每个章节都有完整的 markmap 思维导图，与正文内容双向链接，实现快速导航和知识关联

## v1 Requirements

### Markmap Structure

- [ ] **MARK-01**: 在文件顶部创建完整的 markmap 代码块，包含 YAML frontmatter 配置
- [ ] **MARK-02**: markmap 包含章节标题和所有主要小节（12.1-12.4）
- [ ] **MARK-03**: markmap 包含所有5个DP应用模型的节点
- [ ] **MARK-04**: markmap 包含所有例题节点（例题 12.1-1, 12.2-1, 12.3-1 到 12.3-4, 12.4-1）
- [ ] **MARK-05**: markmap 使用正确的层次结构（# ## ### ####）对应章节层级
- [ ] **MARK-06**: markmap 高度参数设置为合适的值（参考第1章的 643）

### Content Anchors

- [ ] **ANCHOR-01**: 为所有主要小节标题添加块锚点（^xxx 格式，仅字母）
- [ ] **ANCHOR-02**: 为所有例题标题添加块锚点
- [ ] **ANCHOR-03**: 为所有5个DP模型子小节添加块锚点
- [ ] **ANCHOR-04**: 块锚点 ID 仅包含字母 [A-Za-z]+，无数字、下划线、连字符
- [ ] **ANCHOR-05**: 块锚点放置在段落/标题末尾

### Bidirectional Links

- [ ] **LINK-01**: 所有 markmap 节点使用 [[#^anchorId|Display Name]] 链接到正文
- [ ] **LINK-02**: markmap 顶层节点链接到章节标题
- [ ] **LINK-03**: markmap 小节节点链接到对应的小节标题锚点
- [ ] **LINK-04**: markmap 例题节点链接到对应的例题标题锚点

### Content Coverage

- [ ] **COV-01**: markmap 覆盖 Real-Life Application 部分
- [ ] **COV-02**: markmap 覆盖 12.1 递归性质和例题 12.1-1
- [ ] **COV-03**: markmap 覆盖 12.2 前向和后向递归和例题 12.2-1
- [ ] **COV-04**: markmap 覆盖 12.3 所有5个DP应用模型
- [ ] **COV-05**: markmap 覆盖 12.3 所有例题（12.3-1 到 12.3-4）
- [ ] **COV-06**: markmap 覆盖 12.4 维度灾难问题和例题 12.4-1

### Format Consistency

- [ ] **FMT-01**: markmap 格式与第1章保持一致
- [ ] **FMT-02**: YAML frontmatter 格式正确（markmap: height: xxx）
- [ ] **FMT-03**: markmap 代码块使用 ```markmap``` 标记
- [ ] **FMT-04**: 显示名称不包含 LaTeX 公式（提高可读性）

## v2 Requirements

暂无

## Out of Scope

| Feature | Reason |
|---------|--------|
| 修改第12章正文内容 | 只添加 markmap 和锚点，不改变原有内容 |
| 处理其他章节 | v1 仅处理第12章 |
| 修改章节结构 | 保持原有组织方式 |
| 创建新的内容 | 仅对现有内容添加导航结构 |
| 自动化脚本 | 手动处理单个章节 |

## Traceability

| Requirement | Phase | Status |
|-------------|-------|--------|
| MARK-01 | Phase 1 | Pending |
| MARK-02 | Phase 1 | Pending |
| MARK-03 | Phase 1 | Pending |
| MARK-04 | Phase 1 | Pending |
| MARK-05 | Phase 1 | Pending |
| MARK-06 | Phase 1 | Pending |
| ANCHOR-01 | Phase 1 | Pending |
| ANCHOR-02 | Phase 1 | Pending |
| ANCHOR-03 | Phase 1 | Pending |
| ANCHOR-04 | Phase 1 | Pending |
| ANCHOR-05 | Phase 1 | Pending |
| LINK-01 | Phase 1 | Pending |
| LINK-02 | Phase 1 | Pending |
| LINK-03 | Phase 1 | Pending |
| LINK-04 | Phase 1 | Pending |
| COV-01 | Phase 1 | Pending |
| COV-02 | Phase 1 | Pending |
| COV-03 | Phase 1 | Pending |
| COV-04 | Phase 1 | Pending |
| COV-05 | Phase 1 | Pending |
| COV-06 | Phase 1 | Pending |
| FMT-01 | Phase 1 | Pending |
| FMT-02 | Phase 1 | Pending |
| FMT-03 | Phase 1 | Pending |
| FMT-04 | Phase 1 | Pending |

**Coverage:**
- v1 requirements: 26 total
- Mapped to phases: 26
- Unmapped: 0 ✓

---
*Requirements defined: 2025-02-01*
*Last updated: 2025-02-01 after initial definition*
