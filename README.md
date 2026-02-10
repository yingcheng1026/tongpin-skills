# Claude Code Skills Collection

个人收集的 Claude Code Skills，用于提升 AI 协作效率。

## Skills 列表

### 1. Capture - 知识捕获与学习

统一的捕获入口：智能判断用户意图，自动选择「快速存档」或「深度学习」模式。

**触发词**：保存/捕获/学习/理解/存储/记录/存档/收藏 + 链接

**功能**：
- 自动识别链接类型（Twitter/X、YouTube、文章）
- 智能判断用户意图（快速存档 vs 深度学习）
- 抓取内容并保存到 Obsidian
- 支持中文/英文内容

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

## 安装方法

### 方法 1：直接复制

```bash
# 复制 skill 到你的 Claude Code skills 目录
cp -r capture-skill/SKILL.md ~/.claude/skills/capture/SKILL.md
cp -r feynman-johari-skill/SKILL.md ~/.claude/skills/feynman-johari/SKILL.md
```

### 方法 2：克隆仓库

```bash
cd ~/.claude/skills
git clone https://github.com/yingcheng1026/tongpin-skills.git
```

---

## 使用示例

### Capture Skill

```bash
# 快速存档
保存这个：https://x.com/elonmusk/status/123

# 深度学习
学习这个：https://x.com/someone/status/456
```

### Feynman-Johari Skill

```
用户：帮我理解「共识升级」这个概念

AI：让我用几个问题帮你理清思路...
[通过苏格拉底式提问引导深度思考]
```

---

## 依赖要求

### Capture Skill 依赖
- **Bun** - 用于运行 x-to-markdown 脚本
- **X Auth Token** - 用于抓取 Twitter 内容（可选）

### Feynman-Johari Skill 依赖
- 无额外依赖

---

## 贡献

欢迎提交 Issue 和 Pull Request！

---

## 许可证

MIT License

---

## 作者

同频共振 @ [Twitter/X](https://x.com/wngyngchng5388)
