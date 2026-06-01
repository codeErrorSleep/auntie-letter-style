# Auntie Letter Style · 给阿嬷的情书风格

> 把粗俗 / 现代 / 网络中文, 一键改写成"半文半白、克制深情、有画面有距离感"的句子。

一份面向 AI Agent 的 **skill 文件**, 编码了 2026 电影「给阿嬷的情书」里那种"江上明月、寨前溪声"的口感。
让 LLM 改写大白话时, 自动调用这种调子 — 而不是堆典故、装文言。

```
原句: 卧槽, 这也太牛了
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. 此景入目, 如惊雷过耳。三分醒, 七分不敢信。
2. 闻讯心骤停一拍。世间竟有此等事? 回头看, 仍觉不真。
3. 此事若惊涛拍岸, 直教山河失色, 人间无言。
```

```
原句: 我想你了
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. 江上月初升, 恰似君眉目。念你。
2. 夜里翻书翻到"思"字, 满页都是你。
3. 望尽千山, 皆是归途; 望尽千江, 皆是吾心所向。
```

---

## 适用场景

✅ 朋友圈 / 情书 / 群聊嘴替的雅化
✅ 「雅言」「古风翻译」类工具的 prompt 模板
✅ LLM 输出中文时希望更有质感的 prompt 工程师
✅ 任何想"说人话但说漂亮点"的场景

❌ 长篇翻译 / 学术写作 / 商务邮件
❌ 格律严格的旧体诗创作
❌ 需要"严肃正式"的官方文案

---

## 安装

### Codex

把本仓库安装到 Codex 的 skills 目录, 然后重启 Codex:

```bash
mkdir -p ~/.codex/skills/auntie-letter-style
cp SKILL.md README.md EXAMPLES.md ~/.codex/skills/auntie-letter-style/
```

开发时如果想让本地修改立即同步, 可以改用软链:

```bash
mkdir -p ~/.codex/skills
ln -s "$(pwd)" ~/.codex/skills/auntie-letter-style
```

> 如果目标目录已存在, 先删除旧目录或换一个 skill 名称。Codex 会从 `~/.codex/skills/<skill-name>/SKILL.md` 加载本地 skills。

### Claude Code

把 `SKILL.md` 复制或软链到 `~/.claude/skills/auntie-letter-style/`:

```bash
mkdir -p ~/.claude/skills/auntie-letter-style
cp SKILL.md ~/.claude/skills/auntie-letter-style/SKILL.md
```

### OpenCode 调试方式

OpenCode 的 superpowers skill 目录通常在 package cache 里, 路径会随版本变化。仅建议本地调试时使用:

```bash
SUPERPOWERS_DIR="$(ls -d ~/.cache/opencode/packages/superpowers@*/node_modules/superpowers/skills 2>/dev/null | head -n 1)"
test -n "$SUPERPOWERS_DIR" || { echo "先运行一次 opencode 初始化 superpowers"; exit 1; }
mkdir -p "$SUPERPOWERS_DIR/auntie-letter-style"
ln -s "$(pwd)/SKILL.md" "$SUPERPOWERS_DIR/auntie-letter-style/SKILL.md"
```

> 如果找不到 superpowers 目录, 跑一次 `opencode` 让它初始化即可。

### 直接当 Prompt 模板

把 `SKILL.md` 里的"风格签名 + 改写流程"整段贴进你的 LLM system prompt 即可。
不需要 agent 框架, 任何支持自定义系统提示词的工具都能用。

---

## 使用

### 自动模式 (推荐)

装好后, 当你的 prompt 里出现:
- 「把这句雅化一下」
- 「用给阿嬷的情书风格改写」
- 「来点古风」
- 「写得像情书」

agent 会自动调用本 skill, 输出 **3 条**调性略有不同的变体。

### 手动调用

在 OpenCode / Claude Code 里直接说:
> 用 auntie-letter-style 把"今天加班到 11 点"改写一下

或在 prompt 里显式注入:
> 请按以下风格规则改写: [粘贴 SKILL.md 的"风格签名"和"改写流程"两节]

### 输出格式

默认每条 **15-40 字**, 适合单行复制。
如需更长, 在 prompt 里说"每条 60-80 字"即可。

---

## 风格签名 (5 条判别标尺)

| 维度 | 规则 |
|------|------|
| **节奏** | 4 字短句堆叠 + 对偶, 末句白话短句收束 |
| **意象** | 明月 / 溪水 / 江海 / 七夕; 动作: 行、闻、念、望、归 |
| **情感** | 克制, 点到为止; 用距离/物件承载思念, 不用直白抒情 |
| **时空** | 必有具体时刻 (入夜/当夜/梦醒) + 场景 (江上/寨前/窗前) |
| **语域** | 半文半白, 不堆生僻字, 不全篇文言 |

完整风格分析 → [`SKILL.md`](./SKILL.md) · 更多样例 → [`EXAMPLES.md`](./EXAMPLES.md)

---

## 为什么不是"普通文言文"

| 维度 | 普通文言 | 给阿嬷的情书风格 |
|------|---------|----------------|
| 词汇 | 堆"茕茕孑立"等生僻 | 日常字撑起意境 |
| 抒情 | "吾思卿甚笃" | "念你" / "好梦" |
| 收尾 | 全篇文言到底 | 文言 + 一句白话 |
| 节奏 | 追求对仗工整 | 短句节奏 + 不强求工整 |
| 情感 | 庄重肃穆 | 克制温柔、有"距离感" |

差别就一句话: **普通文言是想"显摆", 给阿嬷是想"留白"。**

---

## 文件结构

```
auntie-letter-style/
├── README.md       # 本文件
├── SKILL.md        # 核心 skill 定义 (agent 直接加载这个)
├── EXAMPLES.md     # 83 条分类样例库 (19 个细分场景)
├── LICENSE         # MIT
├── CHANGELOG.md    # 更新记录
└── .gitignore
```

---

## 贡献

欢迎 PR! 三种贡献方式:

1. **新样例**: 在 `EXAMPLES.md` 里加新的 before/after 对照
2. **风格变体**: 在 `SKILL.md` 的"变体表"里加新的调性
3. **Bug 反馈**: 实际用着别扭的句子, 提 issue 附原文 + 期望输出

---

## 灵感来源

-   电影「**给阿嬷的情书**」(2026) — 整本 skill 的风格锚点
-   项目 **雅言** — 一款把现代口语翻译成古诗词/成语/方言/英文金句的工具 (本 skill 是其核心 prompt 的提炼版)

---

## License

MIT © 2026
