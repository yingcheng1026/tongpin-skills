---
name: capture
description: 知识捕获与学习系统。用户给链接时触发，智能判断意图，自动选择「快速存档」或「深度学习」模式。触发词：保存/捕获/学习/理解 + 链接。
allowed-tools: Bash, WebFetch, AskUserQuestion, Write, Read, Skill
---

# Capture - 知识捕获与学习

统一的捕获入口：智能判断用户意图，自动选择「快速存档」或「深度学习」。

---

## 触发方式

### 直接触发
用户给任意链接时自动触发：
- 直接粘贴 URL
- "帮我处理这个"
- "保存这个"
- "捕获这个"
- "学习这个"
- "理解这个"

### 智能意图识别
```
用户说"保存/记录/存档" → 快速模式（#待处理）
用户说"学习/理解/消化" → 深度模式（#已内化）
其他情况 → 询问用户
```

---

## 工作流程

```
用户给链接
    ↓
第1步：识别链接类型（Twitter/YouTube/文章）
    ↓
第2步：调用对应工具抓取内容
    ↓
第3步：判断用户意图
    ├─ 快速存档 → 提炼要点 → 保存（#待处理）
    └─ 深度学习 → 费曼学习法 → 保存（#已内化）
    ↓
第4步：保存到 Obsidian 收件箱
```

---

## 第1步：识别链接类型

```javascript
if (url.includes("x.com/") || url.includes("twitter.com/")) {
    type = "twitter";
} else if (url.includes("youtube.com/") || url.includes("youtu.be/")) {
    type = "youtube";
} else {
    type = "article";
}
```

---

## 第2步：抓取内容

### Twitter/X → 宝玉 x-to-markdown（优先）

**Token 配置**（需要定期更新）：
```bash
export X_AUTH_TOKEN="78776b44c2f5b6407f406ef8571ae6727bef7de9"
export X_CT0="74204a4bd6542f34d509415ec0802e3545ded6c7562fb2c9bb50f1e01518253eaad517b9c9b5f0d22e1d4dc58c6f92897c44b22d6f390191b116fb739f2d3ad778f455041b3ff0a84129bbc911a79a9f"
npx -y bun ~/.claude/skills/baoyu-skills/skills/baoyu-danger-x-to-markdown/scripts/main.ts <url> -o /tmp/x-content.md
```

**获取 Token 方法**：
1. 打开 Chrome，登录 X (twitter.com)
2. 按 `Cmd + Option + I` 打开开发者工具
3. 切换到 **Network** 标签
4. 刷新页面，点击任意请求
5. 在 **Headers** 中找到：
   - `cookie: auth_token=xxxxx`
   - `ct0=xxxxx`

**执行逻辑**：
1. 先用 x-to-markdown 抓取
2. 如果报错（401/403/token失效），用 WebFetch 作为备选
3. 如果 WebFetch 也失败，让用户手动粘贴原文内容

**绝对不能**：抓取失败后直接跳过原文，只保存摘要。原文内容是捕获的核心价值。

### YouTube → youtube-transcript skill

### 其他 → WebFetch

```
WebFetch({ url: url, prompt: "提取文章的完整内容" })
```

---

## 第3步：模式选择

### 自动判断
根据用户说的话自动选择：

| 用户说 | 模式 | 标签 |
|--------|------|------|
| "保存/记录/存档" | 快速 | #待处理 |
| "学习/理解/消化" | 深度 | #已内化 |
| 其他 | 询问 | - |

### 询问用户
无法判断时，用 AskUserQuestion：

| 选项 | 说明 |
|------|------|
| 快速存档 | 抓取 + AI 提炼要点，后续再深挖 |
| 深度学习 | 抓取 + 费曼学习法，现在就消化 |

---

## 第4步：保存格式

### 快速存档模式

```markdown
---
title: 标题文字
source: https://链接
author: 作者名
date: YYYY-MM-DD
tags:
  - 内容标签1
  - 内容标签2
  - 待处理
type: twitter/youtube/article
---

## 🎯 一句话总结
[AI 自动生成]

## 📌 核心观点
1. [观点1]
2. [观点2]
3. [观点3]

## 📄 原文内容
[完整抓取内容]
```

### 深度学习模式

```markdown
---
title: 标题文字
source: https://链接
author: 作者名
date: YYYY-MM-DD
tags:
  - 内容标签1
  - 内容标签2
  - 已内化
type: twitter/youtube/article
learned: true
learning_date: YYYY-MM-DD
---

## 🎯 一句话总结

## 📌 核心观点

## 🧠 费曼学习笔记
### 我学到了什么

### 我的理解

### 知识边界
[我知道什么 / 我不知道什么]

## 💎 金句摘录

## 🔗 关联思考

## 📄 原文内容
```

---

## 标签系统（与 Obsidian 手册对齐）

### 状态标签
| 标签 | 含义 |
|------|------|
| `#待处理` | 暂时保存、等待深挖 |
| `#已内化` | 已经理解并吸收 |
| `#待验证` | 需要实践验证 |

### 内容标签
`#产品` `#AI` `#投资` `#写作` `#复盘` `#方法` `#成长`

### 来源标签
`#flomo-sync` `#article` `#video` `#podcast` `#book` `#twitter`

---

## 保存路径

```
~/Library/CloudStorage/OneDrive-个人/Obsidian Vault/📥Inbox/
└── YYYY-MM-DD-[学习?]标题简述.md
```

- 深度学习：`YYYY-MM-DD-学习-标题.md`
- 快速存档：`YYYY-MM-DD-标题.md`

---

## 使用示例

### 场景 1：用户说"保存这个"
```
用户：帮我保存这个 https://x.com/elonmusk/status/123

Agent：
1. 识别意图 → 快速存档
2. 抓取内容
3. AI 提炼要点
4. 保存（#待处理）
```

### 场景 2：用户说"学习这个"
```
用户：学习这个 https://x.com/servasyy_ai/status/2020475413055885385

Agent：
1. 识别意图 → 深度学习
2. 抓取内容
3. 启动费曼学习法（feynman-johari skill）
4. 生成学习笔记
5. 保存（#已内化）
```

### 场景 3：用户只给链接
```
用户：https://youtube.com/watch?v=xxx

Agent：
1. 无法判断意图 → 询问用户
2. 用户选择模式
3. 继续处理...
```

---

## 相关 Skills

- **feynman-johari**: 费曼学习法
- **auto-memory**: 自动更新记忆档案
- **youtube-transcript**: YouTube 转文稿
