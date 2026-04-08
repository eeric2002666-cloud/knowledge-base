---
name: llm-wiki-knowledge-base
description: |
  基于 Karpathy LLM Wiki 模式的个人知识库系统。
  
  **使用场景**：
  - 用户说"加入知识库"、"添加到知识库"
  - 用户说"整理知识库"、"搜索知识库"
  - 用户说"回顾知识"、"我的知识库"
  - 用户说"把这个结论存到知识库"
  - 用户说"知识库健康检查"
  - 用户分享链接/文件/笔记，要求存入知识库
  
  **核心功能**：
  (1) 一键摄入链接/文件/笔记/对话结论
  (2) 增量编译到互联的 Wiki 页面
  (3) 搜索、回顾和知识迭代
  (4) 问答结果写回 Wiki（知识通过使用增长）
  (5) 定期健康检查
license: MIT
---

# LLM Wiki 知识库系统

基于 Karpathy 的 LLM Wiki 模式：不是简单 RAG 索引，而是**增量编译**一个持久、互联的 Markdown 知识库。

## 快速参考

| 任务 | 操作 |
|------|------|
| 添加内容 | 接收用户内容，提取要点，更新 Wiki |
| 搜索 | 读 index.md → 读相关 Wiki 页面 → 合成答案 |
| 保存结论 | 询问用户 → 存到 sources/ → 整合到 Wiki |
| 整理 | 分类内容 → 更新 index → 追加 log |
| 健康检查 | 检查矛盾/过时/孤立页面/坏链 |

## 核心理念

| 传统 RAG | LLM Wiki |
|----------|----------|
| 每次查询重新检索 | 知识编译一次，持续更新 |
| 碎片化答案 | 已有的交叉引用 |
| 无积累 | 越用越丰富 |

**关键**：Wiki 是持久、复合的产物。每次问答都是知识增长的机会。

---

## 存储结构

```
knowledge-base/
├── index.md            # 内容索引（按类型/标签）
├── log.md              # 成长时间线
├── schema.md           # 页面格式规范
├── sources/            # 原始源（不可变）
│   └── {年}/
│       ├── links/
│       ├── documents/
│       ├── notes/
│       └── conclusions/
├── wiki/               # LLM 编译的维基
│   ├── entities/       # 实体页（人物/产品/公司）
│   ├── concepts/       # 概念页（原理/方法）
│   ├── summaries/      # 摘要页（源文档摘要）
│   └── synthesis/      # 综合页（跨主题）
└── notes/              # 个人笔记
```

---

## 核心文件格式

### index.md

```markdown
# 知识库索引

## 实体 (entities/)
- [[Apple Design]] - Apple 设计系统规范 (3 sources)

## 概念 (concepts/)
- [[LLM Wiki]] - Karpathy 的知识库模式

## 源 (sources/)
- 2026-04: Apple Design System, LLM Wiki Pattern
```

### log.md

```markdown
# 知识库日志

## [2026-04-08] ingest | Apple Design System
## [2026-04-08] query | 如何构建落地页
## [2026-04-08] writeback | 落地页实现要点
```

### schema.md

```markdown
# 知识库规范

## 页面格式 (Frontmatter)
- **title**: 页面标题
- **type**: entity | concept | summary | synthesis | conclusion
- **tags**: [#标签1, #标签2]
- **sources**: 关联的源文件
- **last_updated**: YYYY-MM-DD

## 命名惯例
- 实体用 [[Name]] 格式
- 概念用 [[概念名称]] 格式
```

---

## 操作流程

### 1. Ingest（摄入）⚠️

用户添加内容时，按以下步骤处理：

1. **接收内容**：用户发送链接/文件/笔记/结论
2. **提取信息**：LLM 读取内容，提取：
   - 标题
   - 核心要点（3-5 条）
   - 关联概念
   - 建议标签
3. **确定类型**：
   - 人物/产品/公司 → `wiki/entities/`
   - 原理/方法/模式 → `wiki/concepts/`
   - 源文档摘要 → `wiki/summaries/`
   - 跨主题分析 → `wiki/synthesis/`
4. **更新 Wiki**：创建或更新相关页面，添加交叉引用
5. **更新索引**：添加到 `index.md`
6. **追加日志**：记录到 `log.md`

### 2. Query（查询）⚠️

用户提问时：

1. **搜索索引**：先读 `index.md` 找到相关页面
2. **读取 Wiki**：读取相关页面内容
3. **合成答案**：带引用生成答案，格式：
   > 根据 [[页面名称]]：{引用内容}
4. **Write-back**（重要！）：
   - 有价值的分析 → 新建 `wiki/synthesis/` 页面
   - 新洞察 → 更新相关 Wiki 页面
   - 发现的连接 → 添加交叉引用

### 3. Lint（健康检查）⚠️

运行 `知识库健康检查`：

```markdown
## 健康检查报告

### 矛盾检查
- [ ] {检查项}

### 过时检查
- [ ] {检查项}

### 孤立页
- [ ] {页面名} - 无 Inbound 链接

### 缺失概念
- [ ] {概念名} - 被提及但无专属页

### 链接检查
- [ ] {检查项}

### 建议
- {建议内容}
```

### 4. 对话结论保存

讨论得出重要结论时：

1. 主动询问：`"这个结论要存到知识库吗？"`
2. 用户确认后，保存到 `sources/conclusions/{年}/{标题}.md`
3. 提取核心要点，更新相关 Wiki 页面
4. 追加到 `log.md`

---

## 内容模板

### 源文件模板

```markdown
---
title: {标题}
type: link | document | video | audio | note | conclusion
tags: [#标签1, #标签2]
source_url: {URL}
added: {YYYY-MM-DD}
---

## 要点提炼
{LLM 提取的核心内容}

## 关联概念
- [[概念1]]
- [[概念2]]
```

### Wiki 页面模板

```markdown
---
title: {主题}
type: entity | concept | summary | synthesis | conclusion
tags: [#标签1, #标签2]
sources: [{源1}](), [{源2}]()
last_updated: {YYYY-MM-DD}
---

# {主题}

## 概述
{一句话描述}

## 核心要点
- 要点1
- 要点2

## 关联
- [[相关概念1]]
- [[相关概念2]]

## 回顾
- {YYYY-MM-DD}: {回顾笔记}
```

---

## 关键规则（Critical Rules）⚠️

1. **知识通过使用增长**：每次有价值的问答都应该考虑 Write-back
2. **交叉引用**：概念页之间必须互联，形成知识网络
3. **保持索引最新**：每次 Ingest 后更新 index.md
4. **日志追踪**：所有操作都记录到 log.md
5. **结论主动询问**：讨论得出结论时，主动提示用户保存
6. **健康检查定期做**：每月至少一次 Lint 检查

---

## 使用指令

| 指令 | 功能 |
|------|------|
| `添加 {内容}` | Ingest 新内容到知识库 |
| `搜索 {关键词}` | 在 Wiki 中搜索 |
| `回顾` / `本周新增` | 查看最近内容 |
| `整理知识库` | 分类 + 更新索引 |
| `健康检查` | 运行 Lint 检查 |
| `保存结论` | 保存当前讨论的结论 |
| `列出标签` | 查看所有标签 |

---

## Write-back 原则

**重要**：每次有价值的问答都应该考虑写回 Wiki。

### 何时 Write-back

- 用户问了一个需要综合分析的问题
- 答案包含多个源的内容整合
- 产生了新的洞察或结论
- 发现了概念之间的新联系

### Write-back 步骤

1. 创建 `wiki/synthesis/{新页面}.md` 或更新现有页面
2. 添加交叉引用到相关概念页
3. 更新 `index.md` 添加新页面
4. 追加 `log.md` 记录 Write-back

---

## 依赖

本 Skill 无需外部工具依赖，所有内容通过 Markdown 文件管理。

---

## 相关链接

- [Karpathy LLM Wiki 原文](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [OpenClaw 文档](https://docs.openclaw.ai)
- [Skill Hub](https://skills.sh/)
