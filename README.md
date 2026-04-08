[README.md](https://github.com/user-attachments/files/26559590/README.md)
# 🧠 LLM Wiki 知识库

> 基于 Karpathy LLM Wiki 模式的个人知识库管理系统

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skill Version](https://img.shields.io/badge/Version-1.0.0-blue.svg)](./llm-wiki-knowledge-base/_meta.json)

## 简介

基于 [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 模式构建的个人知识库系统。不同于传统 RAG 的每次查询重新检索，LLM Wiki 是**增量编译**一个持久、互联的 Markdown 知识库，让知识通过使用不断增长。

## 特性

| 特性 | 说明 |
|------|------|
| 📥 一键摄入 | 链接/文件/笔记/对话结论，直接发给 AI 就能存 |
| 🔄 增量编译 | 基于 LLM Wiki 模式，知识越积越多 |
| ✨ Write-back | 问答结果写回 Wiki，知识通过使用增长 |
| 🔍 智能搜索 | 在 Wiki 中快速找到相关内容，带交叉引用 |
| 🏥 健康检查 | 定期检查知识库矛盾、过时、孤立页面 |
| 💬 结论保存 | 与 AI 对话的结论自动保存，形成知识体系 |

## 安装

```bash
npx skills add laixialun/llm-wiki-knowledge-base
```

或从本地安装：

```bash
npx skills add /path/to/llm-wiki-knowledge-base
```

## 使用方式

| 操作 | 怎么说 |
|------|--------|
| 添加链接 | `把这个加到知识库：https://...` |
| 添加笔记 | `记一下：我的思考是...` |
| 保存结论 | `把这个结论存到知识库` |
| 搜索 | `搜索知识库 Apple` |
| 回顾 | `本周新增了什么` |
| 整理 | `整理知识库` |
| 健康检查 | `知识库健康检查` |

## 架构

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

## 核心理念

| 传统 RAG | LLM Wiki |
|----------|----------|
| 每次查询重新检索 | 知识编译一次，持续更新 |
| 碎片化答案 | 已有的交叉引用 |
| 无积累 | 越用越丰富 |

**关键**：Wiki 是持久、复合的产物。每次问答都是知识增长的机会。

## 操作流程

### 1. Ingest（摄入）

用户添加内容时：
1. 接收内容（链接/文件/笔记/结论）
2. LLM 提取关键信息
3. 更新 Wiki 页面
4. 更新 index.md
5. 追加 log.md

### 2. Query（查询）

1. 搜索 index.md 找到相关页面
2. 读取相关 Wiki 页面
3. 合成带引用的答案
4. **Write-back**：有价值的答案写回 Wiki

### 3. Lint（健康检查）

- 矛盾检查
- 过时检查
- 孤立页检查
- 缺失概念检查

## 相关资源

- [Karpathy LLM Wiki 原文](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [OpenClaw 文档](https://docs.openclaw.ai)
- [Skill Hub](https://skills.sh/)

## License

MIT License - see [LICENSE.txt](./llm-wiki-knowledge-base/LICENSE.txt)

---

*知识是活的，在使用中生长。*
