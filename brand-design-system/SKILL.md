---
name: brand-design-system
description: |
  品牌设计规范助手。从 VoltAgent/awesome-design-md 仓库获取各种品牌的官方设计规范，
  包括颜色、字体、排版、图标等，用于创建符合品牌风格的设计作品。
  
  **使用场景**：
  - 用户说"品牌设计规范"、"设计风格"、"品牌颜色"
  - 用户说"用 Apple 风格"、"用 Stripe 风格"
  - 用户说"查看 xxx 品牌设计"
  - 用户需要某个品牌的视觉规范
  
  **支持的品牌**：airbnb, airtable, apple, bmw, cal, claude, clay, clickhouse, 
  cohere, coinbase, composio, cursor, elevenlabs, expo, ferrari, figma, framer, 
  hashicorp, ibm, intercom, kraken, lamborghini, linear.app, lovable, minimax, 
  mintlify, miro, mistral.ai, mongodb, notion, nvidia, ollama, opencode.ai, 
  pinterest, posthog, raycast, renault, replicate, resend, revolut, runwayml, 
  sanity, sentry, spacex, spotify, stripe, supabase, superhuman, tesla, together.ai, 
  uber, vercel, voltagent, warp, webflow, wise, x.ai, zapier
license: MIT
---

# 品牌设计规范

从 [VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md) 获取各种品牌的官方设计规范。

## 快速参考

| 任务 | 操作 |
|------|------|
| 列出品牌 | 说"有哪些品牌"或"支持哪些品牌" |
| 查看品牌规范 | 说"查看 Apple 设计规范" |
| 应用风格 | 说"用 Stripe 风格设计" |
| 颜色规范 | 说"Apple 的主色是什么" |

## 支持的品牌

| 类别 | 品牌 |
|------|------|
| **科技/AI** | anthropic, claude, cohere, minimax, mistral.ai, nvidia, ollama, opencode.ai, replicate, together.ai, x.ai |
| **设计/开发** | figma, framer, linear.app, raycast, sanity, vercel, voltagent, warp |
| **金融** | coinbase, revolut, stripe, wise |
| **消费** | airbnb, airtable, apple, bmw, clickhouse, cursor, expo, ferrari, ibm, intercom, lamborghini, lovable, mintlify, miro, mongodb, notion, pinterest, posthog, renault, resend, sentry, spacex, spotify, supabase, superhuman, tesla, uber, webflow, zapier |
| **汽车** | bmw, ferrari, lamborghini, renault, spacex, tesla |
| **音频/视频** | elevenlabs, runwayml |

---

## 数据源

设计规范来自开源仓库：

```
https://github.com/VoltAgent/awesome-design-md/tree/main/design-md/{品牌名}/
```

每个品牌通常包含：
- `DESIGN.md` - 完整设计规范
- `README.md` - 品牌介绍
- `preview.html` / `preview-dark.html` - 交互式预览

---

## 使用流程

### 1. 获取品牌规范

当用户请求某个品牌的设计规范时：

1. 从 GitHub 读取对应品牌的 `DESIGN.md`
2. 提取关键信息（颜色、字体、间距等）
3. 返回给用户

### 2. 应用品牌风格

当用户要求按某品牌风格设计时：

1. 获取品牌设计规范
2. 提取关键视觉元素：
   - 主色 / 辅助色 / 强调色
   - 字体（标题 / 正文）
   - 圆角 / 间距规范
   - 按钮样式
3. 生成符合规范的设计

### 3. 颜色查询

直接查询品牌颜色：

| 品牌 | 主色 | 强调色 |
|------|------|--------|
| Apple | #000000, #f5f5f7 | #0071e3 |
| Stripe | #635bff | #00d4ff |
| Figma | #0ACF83 | #A259FF |
| Vercel | #000000 | #333333 |

---

## 技术实现

### 读取设计规范

使用 Browser 工具读取：

```
https://raw.githubusercontent.com/VoltAgent/awesome-design-md/main/design-md/{brand}/DESIGN.md
```

### 常见设计元素

| 元素 | 说明 |
|------|------|
| Primary Color | 主色 |
| Secondary Color | 辅助色 |
| Accent Color | 强调色 |
| Typography | 字体规范 |
| Spacing | 间距系统 |
| Border Radius | 圆角 |
| Shadows | 阴影 |

---

## 示例

### 查询 Apple 设计规范

**用户**："查看 Apple 设计规范"

**回复**：

```
🍎 Apple Design System

主色：#000000 (Pure Black)
背景：#f5f5f7 (Light Gray)
强调色：#0071e3 (Apple Blue)

字体：
- 标题：SF Pro Display (或 DM Sans)
- 正文：SF Pro Text (或 Manrope)

间距：8px 基础单位
圆角：8px / 12px / 980px (药丸)
```

### 用 Stripe 风格设计

**用户**："用 Stripe 风格设计一个按钮"

**回复**：根据 Stripe 品牌规范生成对应样式的按钮代码

---

## 关键规则 ⚠️

1. **优先使用官方规范**：从 DESIGN.md 读取最新规范
2. **准确匹配品牌**：使用正确的品牌名称（注意大小写和连字符）
3. **保留引用**：标注设计规范的来源
4. **一致性**：同一品牌的所有元素保持统一风格

---

## 相关链接

- [awesome-design-md 仓库](https://github.com/VoltAgent/awesome-design-md)
- [Apple DESIGN.md](https://github.com/VoltAgent/awesome-design-md/blob/main/design-md/apple/DESIGN.md)
- [Stripe DESIGN.md](https://github.com/VoltAgent/awesome-design-md/blob/main/design-md/stripe/DESIGN.md)
- [Figma DESIGN.md](https://github.com/VoltAgent/awesome-design-md/blob/main/design-md/figma/DESIGN.md)

---

*获取各大品牌设计规范，打造专业设计。*
