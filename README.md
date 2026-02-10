# Claude Code Skills Collection

> 个人收集的 Claude Code Skills，让 AI 协作更智能、更懂你。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude-Code-orange.svg)](https://claude.ai/code)

---

## 为什么是这套 Skills？

**核心理念：AI 不应该是工具，而应该是懂你的伙伴。**

这套 Skills 的设计原则是**用户体验优先**：

- **零配置启动** - 不需要复杂设置，给个链接就开始工作
- **智能意图识别** - AI 自动判断你是想"快速存档"还是"深度学习"
- **优雅降级** - 即使某个环节失败，也能给出备选方案
- **可复用产出** - 不是一次性对话，而是生成可保存的知识资产

---

## Skills 列表

### 1. Capture - 知识捕获与学习系统

统一的捕获入口：智能判断用户意图，自动选择「快速存档」或「深度学习」模式。

**触发词**：保存/捕获/学习/理解/存储/记录/存档/收藏 + 链接

**核心功能**：
- 自动识别链接类型（Twitter/X、YouTube、文章）
- 智能判断用户意图（快速存档 vs 深度学习）
- 抓取内容并保存到 Obsidian
- 支持中文/英文内容
- 优雅降级：Token 失效时自动切换备选方案

---

### 2. Feynman-Johari - 双向费曼学习伙伴

结合费曼技巧与乔哈里窗框架的深度学习工具，通过互动式提问帮助用户深度理解概念。

**触发词**：帮我学习/帮我理解/费曼技巧/给我讲讲/教我...

**核心原则**：
- 降维：用类比、可视化逻辑简化复杂概念
- 反向输出：强迫用户用自己话复述
- 场景锚定：知识与用户经验绑定
- 结构化产出：生成可复用的知识资产

**四阶段流程**：
1. 蒸馏与诊断（识别盲点）
2. 互动修正与场景绑定
3. 结构化结晶（生成知识卡片）
4. 应用迁移（连接实际场景）

---

## 效果预览

<!-- TODO: 添加截图或 GIF 演示 -->

```
用户：学习这个 https://x.com/someone/status/123

AI：[自动识别为深度学习模式]
     正在抓取内容...
     让我通过几个问题帮你理解这个概念...

     [费曼学习流程]

     ✅ 已生成学习笔记并保存到 Obsidian
```

---

## 快速开始

### 前置要求

- Claude Code 已安装
- Obsidian（可选，用于保存知识卡片）

### 一键安装

```bash
# 克隆仓库
git clone https://github.com/yingcheng1026/tongpin-skills.git

# 复制 skills 到你的 Claude Code 目录
mkdir -p ~/.claude/skills
cp -r tongpin-skills/capture-skill ~/.claude/skills/capture/
cp -r tongpin-skills/feynman-johari-skill ~/.claude/skills/feynman-johari/

# 重启 Claude Code
```

---

## 依赖说明

### Capture Skill 依赖

| 依赖 | 用途 | 来源 | 必需 |
|------|------|------|------|
| **Bun** | 运行 x-to-markdown 脚本 | [bun.sh](https://bun.sh/) | ✅ 是 |
| **X Auth Token** | 抓取 Twitter 内容 | 自己获取 | ⚠️ 可选（建议） |
| **x-to-markdown** | 将 X 文章转为 Markdown | [宝玉/baoyu-danger-x-to-markdown](https://github.com/bravealy/baoyu-danger-x-to-markdown) | ✅ 是 |
| **youtube-transcript** | 下载 YouTube 字幕 | Claude Code 内置 | ✅ 是 |

#### 如何获取 X Auth Token

1. 打开 Chrome，登录 X (twitter.com)
2. 按 `Cmd + Option + I` 打开开发者工具
3. 切换到 **Network** 标签
4. 刷新页面，点击任意请求
5. 在 **Headers** 中找到：
   - `cookie: auth_token=xxxxx`
   - `ct0=xxxxx`

> 💡 **提示**：Token 会定期失效，如果抓取失败请重新获取。

### Feynman-Johari Skill 依赖

**无额外依赖** ✅

---

## 使用示例

### Capture Skill

```bash
# 快速存档
保存这个：https://x.com/elonmusk/status/123

# 深度学习
学习这个：https://x.com/someone/status/456

# YouTube 视频
理解这个视频：https://youtube.com/watch?v=xxx
```

### Feynman-Johari Skill

```bash
# 概念学习
用户：帮我理解「共识升级」这个概念

AI：让我用几个问题帮你理清思路...
[通过苏格拉底式提问引导深度思考]
```

---

## 自定义配置

### 修改 Obsidian 保存路径

编辑 `capture-skill/SKILL.md` 文件，找到 `保存路径` 部分：

```markdown
## 保存路径
~/Library/CloudStorage/OneDrive-个人/Obsidian Vault/📥Inbox/
```

改为你自己的 Obsidian Vault 路径。

---

## 常见问题

### Q: Capture Skill 报错 "Token 失效" 怎么办？

A: X 的 Token 会定期失效，按照上面的「如何获取 X Auth Token」步骤重新获取即可。

### Q: YouTube 字幕下载失败？

A: 可能是视频没有字幕，或者地区限制。可以尝试使用 VPN 或选择其他视频。

### Q: 如何修改保存路径？

A: 编辑 `capture-skill/SKILL.md` 文件，找到 `保存路径` 部分，修改为你自己的路径。

### Q: Skill 没有被加载？

A: 确保 SKILL.md 文件在正确的目录：`~/.claude/skills/<skill-name>/SKILL.md`

---

## 路线图

- [ ] 添加更多内容源支持（播客、PDF）
- [ ] 支持自定义标签系统
- [ ] 添加 Webhook 通知
- [ ] 支持多语言输出

---

## 贡献

欢迎提交 Issue 和 Pull Request！

如果你有改进建议或发现了 bug，请：
1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启一个 Pull Request

---

## 致谢

本项目依赖以下优秀的开源项目：

- **[宝玉/baoyu-danger-x-to-markdown](https://github.com/bravealy/baoyu-danger-x-to-markdown)** - X to Markdown 转换工具
- **[Claude Code](https://claude.ai/code)** - Anthropic 的 AI 编程助手

---

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

## 作者

同频共振 @ [Twitter/X](https://x.com/wngyngchng5388)

---

<div align="center">

**⭐ 如果这个项目对你有帮助，请给一个 Star！**

**💬 有问题？在 Twitter 上找我聊聊**

</div>
