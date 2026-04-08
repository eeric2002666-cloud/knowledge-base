# 🧠 Knowledge Base

> 基于 Karpathy 的 LLM Wiki 模式构建的个人知识库管理系统

[![Skill installs](https://img.shields.io/badge/dynamic/json?label=installs&query=$.installs&url=https://skills.sh/api/skills/laixialun/knowledge-base)](https://skills.sh/skill/laixialun/knowledge-base)

## ✨ 特性

| 特性 | 说明 |
|------|------|
| 📥 一键添加 | 链接/文件/笔记/对话结论，直接发给 AI 就能存 |
| 🔍 智能搜索 | 在 wiki 中快速找到相关内容 |
| 💬 结论保存 | 与 AI 对话的结论自动保存，形成知识体系 |
| 🔄 增量编译 | 基于 LLM Wiki 模式，知识越积越多 |
| ✨ Write-back | 问答结果写回 wiki，知识通过使用增长 |
| 🏥 健康检查 | 定期检查知识库矛盾、过时、孤立页面 |

## 📦 安装

```bash
npx skills add laixialun/knowledge-base
```

## 🚀 使用方式

| 操作 | 怎么说 |
|------|--------|
| 添加链接 | `把这个加到知识库：https://...` |
| 添加笔记 | `记一下：我的思考是...` |
| 保存结论 | `把这个结论存到知识库` |
| 搜索 | `搜索知识库 Apple` |
| 回顾 | `本周新增了什么` |
| 整理 | `整理知识库` |
| 健康检查 | `知识库健康检查` |

## 🏗️ 架构

基于 [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 模式：

```
knowledge-base/
├── sources/        # 原始源（不可变）
│   └── {年}/
├── wiki/           # LLM 编译的维基
│   ├── entities/   # 实体页
│   ├── concepts/   # 概念页
│   ├── summaries/  # 摘要页
│   └── synthesis/  # 综合页
├── index.md        # 内容索引
├── log.md          # 成长日志
└── schema.md       # 规范定义
```

### 核心理念

| 传统 RAG | LLM Wiki |
|----------|----------|
| 每次查询重新检索 | 知识编译一次，持续更新 |
| 碎片化答案 | 已有的交叉引用 |
| 无积累 | 越用越丰富 |

**关键**：LLM 做繁琐的维护工作（总结、交叉引用），人类做思考和提问。

## 📚 相关资源

- [Karpathy LLM Wiki 原文](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [OpenClaw 文档](https://docs.openclaw.ai)
- [Skill Hub](https://skills.sh/)

## 📄 License

MIT
