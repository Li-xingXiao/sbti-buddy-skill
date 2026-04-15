<div align="center">

<img src="assets/sbti-buddy.jpg" alt="SBTI Buddy Banner" width="100%">

<br>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-14b8a6?logo=anthropic&logoColor=white)](https://claude.ai/claude-code)
[![GitHub stars](https://img.shields.io/github/stars/Li-xingXiao/sbti-buddy-skill?style=social)](https://github.com/Li-xingXiao/sbti-buddy-skill)

**Personality tests capture a moment. Your AI conversations reveal who you really are.**

**性格测试只能测出一瞬间的你。和 AI 的长期对话，才是真实的你。**

[English](#what-is-sbti-buddy) · [中文](#sbti-buddy-是什么) · [Quick Start](#quick-start--快速开始)

</div>

---

## What is SBTI Buddy?

A **Claude Code skill** built on [SBTI-Test](https://sbti.fancc.de5.net/) — a personality framework designed specifically for programmers. While the original SBTI uses a questionnaire, SBTI Buddy skips the form entirely: it reads your AI conversation history and **automatically** determines your type. No questionnaire needed.

It generates:

- **🎴 Programmer Personality Type** — 27 programmer-specific archetypes across 5 behavioral models and 15 dimensions. Not generic MBTI — types like `CTRL (Ctrl+S the Architect)`, `DEAD (404 the Unmotivated)`, `MONK (Vim僧 the Terminal Sage)`
- **🐾 Animated ASCII Buddy** — a companion that lives in your Claude Code statusline. Powered by a background daemon for smooth, continuous animation — blinks, talks, wiggles ears, and sways even while you're typing
- **🧠 Companion Skill** — auto-installed skill that gives your buddy a voice. It comments on your code (in character), reminds you to rest after 10pm, and celebrates your achievements
- **🎙️ Communication Style Adaptation** — Claude adapts how it talks to you based on your personality: verbosity, tone, assertiveness, proactivity, and decision framing. **Only changes communication style — never affects reasoning or technical accuracy**
- **📈 Evolution Tracking** — your type changes over time. SBTI Buddy records every shift and shows your programmer growth timeline
- **🏆 15 Achievements** — unlock badges like `🦉 Night Owl`, `💀 Back from Dead`, `🧘 Code Monk`
- **🖼️ Social Media Share Card** — one command to export a stunning 1200×630px PNG card with your type, stats, evolution timeline, and a fresh AI-generated roast. Ready for Twitter/WeChat/Discord

> **Why no questionnaire?** Personality tests measure how you *think* you are in that moment. But your real coding personality shows in thousands of conversations — how you ask for help, how you respond to errors, how you communicate with AI. That can't be faked. SBTI Buddy reads the truth from your history.

---

## SBTI Buddy 是什么？

一个基于 [SBTI测试](https://sbti.fancc.de5.net/) 构建的 **Claude Code 技能**。SBTI 是专为程序员设计的人格框架，原版需要做测试题，而 SBTI Buddy 完全跳过问卷——直接读取你的 AI 对话历史，**自动**判定你的类型。不需要做任何测试题。

它会生成：

- **🎴 程序员人格类型** — 27 种程序员专属人格原型，覆盖 5 大行为模型、15 个维度。不是泛泛的 MBTI，而是 `CTRL（拿捏者）`、`DEAD（404 开发者）`、`MONK（Vim僧）` 这样的程序员特有类型
- **🐾 动态 ASCII 伙伴** — 住在你 Claude Code 状态栏里的小伙伴。后台守护进程驱动，持续流畅动画——眨眼、说话、甩耳朵、摇头，打字时也在动
- **🧠 伴侣技能** — 自动安装的技能，让你的 buddy 拥有独特的声音。它会用角色语气评论你的代码，晚上 10 点后提醒你休息
- **🎙️ 沟通风格适配** — Claude 会根据你的性格调整跟你说话的方式：详细程度、语气温度、推荐力度、主动性、决策框架。**只改变沟通风格，不影响推理和技术判断**
- **📈 进化追踪** — 你的类型会随时间变化。SBTI Buddy 记录每次转变，展示你的程序员成长轨迹
- **🏆 15 个成就** — 解锁 `🦉 夜猫子`、`💀 起死回生`、`🧘 代码僧侣` 等徽章
- **🖼️ 社交媒体分享卡** — 一条命令导出精美 1200×630px PNG 卡片，包含你的类型、数据、进化时间线和 AI 现场生成的吐槽。直接发朋友圈/Twitter/Discord

> **为什么不做测试题？** 性格测试只能测出你「此刻觉得自己是什么样的人」。但你真实的编程人格，藏在成千上万次对话里——你怎么求助、怎么应对报错、怎么和 AI 沟通。这些没法伪装。SBTI Buddy 从你的历史中读出真相。

---

**Input:** Your `~/.claude/history.jsonl` (read-only, never sent anywhere)

**Output:**

| Output | What you get |
|--------|-------------|
| 🎴 ASCII Share Card | Your SBTI type, DNA pattern, dimension bars — paste anywhere |
| 🖼️ Social Media PNG | 1200×630px dark-themed card with avatar, stats, roast — share on Twitter/WeChat |
| 🐾 Animated Buddy | ASCII companion that lives in your Claude Code statusline |
| 🧠 Companion Skill | Auto-installed skill — buddy reacts, comments, tracks your mood |
| 🎙️ Communication Style | Claude adapts tone, verbosity, assertiveness to your personality (style only, not reasoning) |
| 📈 Evolution Log | Type change history — watch yourself grow over time |

<div align="center">
<img src="assets/demo/achievements.png" alt="Everything SBTI Buddy Does" width="600">
</div>

<div align="center">

**📸 What it looks like / 运行效果**

<img src="assets/demo/share-card.png" alt="SBTI Share Card" width="700">

<sub>Social media share card — type, dimensions, evolution history, AI roast / 社交媒体分享卡</sub>

</div>

<details>
<summary><b>🐾 Meet the buddies (click to expand)</b></summary>

<br>

<table>
<tr>
<td align="center"><img src="assets/gifs/CTRL.gif" width="120"><br><b>CTRL</b><br><sub>The Architect</sub></td>
<td align="center"><img src="assets/gifs/BOSS.gif" width="120"><br><b>BOSS</b><br><sub>The Tech Lead</sub></td>
<td align="center"><img src="assets/gifs/DEAD.gif" width="120"><br><b>DEAD</b><br><sub>The 404 Dev</sub></td>
<td align="center"><img src="assets/gifs/MONK.gif" width="120"><br><b>MONK</b><br><sub>Terminal Sage</sub></td>
<td align="center"><img src="assets/gifs/SEXY.gif" width="120"><br><b>SEXY</b><br><sub>The Lambda</sub></td>
</tr>
<tr>
<td align="center"><img src="assets/gifs/SHIT.gif" width="120"><br><b>SHIT</b><br><sub>Angry Shipper</sub></td>
<td align="center"><img src="assets/gifs/MUM.gif" width="120"><br><b>MUM</b><br><sub>Error Handler</sub></td>
<td align="center"><img src="assets/gifs/MALO.gif" width="120"><br><b>MALO</b><br><sub>Chaos Monkey</sub></td>
<td align="center"><img src="assets/gifs/JOKE-R.gif" width="120"><br><b>JOKE-R</b><br><sub>Debug Comedian</sub></td>
<td align="center"><img src="assets/gifs/HHHH.gif" width="120"><br><b>HHHH</b><br><sub>Happy Coder</sub></td>
</tr>
</table>

*10 of 27 types shown. The rest? Discover yours by running `sbti`.*

*展示了 27 种中的 10 种。剩下的？运行 `sbti` 亲自探索。*

</details>

---

## Quick Start / 快速开始

**Claude Code (marketplace):**

```bash
# Step 1: Add marketplace
/plugin marketplace add Li-xingXiao/sbti-buddy-skill

# Step 2: Install
/plugin install sbti-buddy@sbti-buddy

# Step 3: Run
sbti
```

**Claude Code (manual):**

```bash
git clone https://github.com/Li-xingXiao/sbti-buddy-skill.git
cp -R sbti-buddy-skill/skills/sbti-buddy ~/.claude/skills/sbti-buddy
# Then in Claude Code:
sbti
```

---

## How It Works / 工作流程

<div align="center">
<img src="assets/demo/analysis-pipeline.jpg" alt="SBTI Analysis Pipeline" width="700">
</div>

---

## 27 Programmer Types / 27 种程序员人格

| Category | Types |
|----------|-------|
| ⚡ **High-Function Leadership** | `CTRL` Ctrl+S · `BOSS` Root · `GOGO` CI/CD · `ATM-er` CashFlow |
| 🧠 **High-Cognition Independent** | `WOC!` Sudo! · `THIN-K` Stack溢 · `SHIT` CoreDump · `POOR` malloc失败 |
| 💚 **Warm Healing** | `MUM` Try-Catch · `THAN-K` ThankU.js · `SEXY` Lambda · `LOVE-R` Merge恋 |
| ⚖️ **Balanced Middle** | `FAKE` .env · `OG8K` Legacy · `MALO` Chaos猴 · `JOKE-R` Bug丑 |
| 😵 **Low-Function Struggling** | `IMFW` Ghost线程 · `IMSB` /dev/null · `DEAD` 404 · `SOLO` Daemon |
| 🔧 **Specialist** | `ZZZZ` Sleep(∞) · `MONK` Vim僧 · `FU?K` rm -rf · `OH-NO` Segfault |
| ✨ **Special** | `HHHH` Hello World · `DIOR-s` Refactor君 |

> 🌙 **Easter egg**: If >50% of your messages are sent between 00:00–05:00, you unlock the **Late Night Coder** badge — with a special dark-circles avatar overlay.

Each type comes with: ASCII avatar · programmer-flavored intro · coding portrait · buddy catchphrase · dev style label.

<div align="center">
<img src="assets/demo/types-gallery.jpg" alt="27 Programmer Archetypes Gallery" width="700">
<br>
<sub>All 27 types — categorized by behavioral pattern / 全部 27 种人格原型一览</sub>
</div>

---

## The 5 Models / 五大模型

| Model | Dimensions | What it measures |
|-------|-----------|-----------------|
| **S** — Self-Image | Code Confidence · Requirements Clarity · Technical Ambition | How you see yourself as a programmer |
| **E** — AI Relationship | AI Trust · Conversation Depth · Independence | How you interact with AI tools |
| **A** — Tech Worldview | Tech Optimism · Code Standards · Project Direction | Your philosophy about code and technology |
| **Ac** — Execution Style | Growth vs Safety · Decision Speed · Task Completion | How you get things done |
| **So** — Communication | Initiative · AI Boundary · Expression Style | How you communicate and collaborate |

Each dimension is scored **0–100**, mapped to **L/M/H**, forming a 15-dimensional DNA pattern like `HHM-HMH-MMH-HHH-MHM`.

<div align="center">
<img src="assets/demo/radar-chart.jpg" alt="SBTI Dimension Profile" width="700">
<br>
<sub>Radar chart + 15 sub-dimension breakdown / 雷达图 + 15 维度细分</sub>
</div>

---

## Buddy System / 伙伴系统

### 🐾 Animated Statusline Buddy

Your buddy lives in the Claude Code statusline — not just a static image.

| Mode | Behavior |
|------|----------|
| **Active** (Claude responding) | Fast cycling (0.4s/frame): blink → talk → ear wiggle → hair sway |
| **Idle** (between responses) | Moderate cycling (1.2s/frame) with mood-based expressions matching time of day |

Powered by a background animation daemon. `PreToolUse`/`PostToolUse` hooks trigger active mode; the daemon auto-starts on first tool call and self-terminates after 1 hour of inactivity.

### 😊 Mood System

| Time | Mood | Expression |
|------|------|-----------|
| 06:00–12:00 | Energized | `◉▽◉` |
| 12:00–18:00 | Focused | `◉_◉` |
| 18:00–22:00 | Winding down | `◉◡◉` |
| 22:00–06:00 | Night owl | `◉ᵕ◉` + rest reminder |

### 🎙️ Communication Style Adaptation

After analysis, Claude adapts **how it communicates** based on 5 personality dimensions:

| Attribute | Driven by | Example |
|-----------|-----------|---------|
| **Verbosity** | E2 (Conversation Depth) | H → detailed step-by-step · L → concise one-liners |
| **Tone** | So3 (Expression Style) | H → warm, encouraging · L → dry, matter-of-fact |
| **Assertiveness** | S1 (Code Confidence) | H → "use X" · L → "you could try X or Y" |
| **Proactivity** | So1 (Initiative) | H → offers related context · L → answers exactly what's asked |
| **Decision Framing** | Ac2 (Decision Speed) | H → picks best option · L → compares alternatives |

> **Important:** This only changes how Claude *talks* to you — tone, detail level, directness. It **never** affects reasoning, technical accuracy, or decision-making quality. Think of it as adjusting the communication channel, not the brain.
>
> **重要说明：** 这只会改变 Claude *跟你说话的方式*——语气、详细程度、直接程度。**不会**影响推理能力、技术准确性或决策质量。可以理解为调整了沟通频道，而不是大脑。

<div align="center">
<img src="assets/demo/ability.png" alt="Communication Style Adaptation" width="600">
<br>
<sub>Default Claude vs adapted for your type / 默认 Claude vs 适配你的类型后</sub>
</div>

### 📈 Evolution

Your type isn't static — it evolves as you grow. Every analysis is recorded. Run `sbti timeline` to see your journey:

```
  2026-01 ──●── DEAD (404)
             │   "HTTP 404: Motivation Not Found"
  2026-02 ──●── IMFW (Ghost线程)
             │   "Um...I'll try, might not work though..."
  2026-04 ──●── CTRL (Ctrl+S)  ← NOW
                 "Saved. Next."
```

### 🏆 Achievements (15 total)

`🎯 First Analysis` · `🔄 Type Shift` · `🪨 Stable Core` · `🦉 Night Owl` · `🌐 Polyglot` · `🤿 Deep Diver` · `🌈 Full Spectrum` · `⚡ Max Power` · `🎭 Identity Crisis` · `💀 Back from Dead` · `🧘 Code Monk` · `🎮 The Controller` · `✨ Perfectionist` · `🏎️ Speed Demon` · `🐺 Lone Wolf`

---

## Commands / 命令

| Command | What it does |
|---------|-------------|
| `sbti` | Full analysis → type + card + buddy + companion skill |
| `sbti card` | Show your ASCII share card with current mood |
| `sbti timeline` | View your type evolution history |
| `sbti spectrum` | Top 5 matching types with similarity bars |
| `sbti match <type>` | Compare compatibility by type code, e.g. `sbti match DEAD` |
| `sbti match <pattern>` | Compare by dimension pattern, e.g. `sbti match HHM-HMH-MMH-HHH-MHM` |
| `sbti match <path>` | Compare by importing the other person's `profile.json` |
| `sbti roast` | Your buddy roasts your coding style |
| `sbti fortune` | Daily coding fortune based on your type |
| `sbti share` | Export a 1200×630px PNG share card (HTML → Chrome headless → PNG) |
| `update my sbti` | Manual incremental update (new messages only, fast) |
| *(auto)* | Auto-updates on session start if 50+ new messages & 24h since last check |

> **How to match with a friend:** Both of you run `sbti` first. Then share your type code (from `sbti card`), pattern string (from `sbti spectrum`), or `~/.claude/sbti-buddy/profile.json` file. The more detail you share, the more precise the match.
>
> **怎么跟朋友匹配：** 双方都先跑一次 `sbti`，然后分享类型码（从 `sbti card` 获取）、pattern 字符串（从 `sbti spectrum` 获取）、或直接发送 `~/.claude/sbti-buddy/profile.json` 文件。分享的信息越详细，匹配越精准。

<details>
<summary><b>📸 Command examples / 命令运行示例 (click to expand)</b></summary>

<br>

<table>
<tr>
<td align="center" valign="top"><b><code>sbti</code></b><br><sub>Full analysis / 完整分析</sub><br><img src="assets/command_picture/1.png" width="400"></td>
<td align="center" valign="top"><b><code>sbti card</code></b><br><sub>Buddy card / 伙伴卡片</sub><br><img src="assets/command_picture/2.png" width="400"></td>
</tr>
<tr>
<td align="center" valign="top"><b><code>sbti timeline</code></b><br><sub>Evolution history / 进化轨迹</sub><br><img src="assets/command_picture/3.png" width="400"></td>
<td align="center" valign="top"><b><code>sbti spectrum</code></b><br><sub>Top 5 types / 类型光谱</sub><br><img src="assets/command_picture/4.png" width="400"></td>
</tr>
<tr>
<td align="center" valign="top"><b><code>sbti match &lt;type&gt;</code></b><br><sub>Match by type / 按类型匹配</sub><br><img src="assets/command_picture/5.png" width="400"></td>
<td align="center" valign="top"><b><code>sbti match &lt;pattern&gt;</code></b><br><sub>Match by pattern / 按模式匹配</sub><br><img src="assets/command_picture/6.png" width="400"></td>
</tr>
<tr>
<td align="center" valign="top"><b><code>sbti match &lt;file&gt;</code></b><br><sub>Match by profile / 导入匹配</sub><br><img src="assets/command_picture/7.png" width="400"></td>
<td align="center" valign="top"><b><code>sbti roast</code></b><br><sub>Buddy roast / 伙伴吐槽</sub><br><img src="assets/command_picture/8.png" width="400"></td>
</tr>
<tr>
<td align="center" valign="top"><b><code>sbti fortune</code></b><br><sub>Daily fortune / 今日运势</sub><br><img src="assets/command_picture/9.png" width="400"></td>
<td align="center" valign="top"><b><code>update my sbti</code></b><br><sub>Incremental update / 增量更新</sub><br><img src="assets/command_picture/11.png" width="400"></td>
</tr>
</table>

<div align="center">
<img src="assets/demo/type-match.jpg" alt="Type Compatibility Match" width="700">
<br>
<sub><code>sbti match DEAD</code> — 15-dimension compatibility comparison / 15 维度兼容性对比</sub>
</div>

</details>

---

## Privacy / 隐私

- Only reads local history files — **nothing is sent externally**
- API keys, tokens, passwords, file paths, PII are **auto-redacted** from all analysis
- Companion skill contains **zero raw messages** — only abstracted personality traits
- All processing happens in your Claude Code session

---

## Requirements / 环境要求

- Claude Code
- 20+ messages of conversation history
- That's it. No API keys, no accounts, no dependencies.

---

## Supported Languages / 支持语言

Signal detection works across **9 languages** — your buddy speaks your language:

`🇨🇳 中文` · `🇺🇸 English` · `🇯🇵 日本語` · `🇰🇷 한국어` · `🇪🇸 Español` · `🇫🇷 Français` · `🇩🇪 Deutsch` · `🇧🇷 Português` · `🇷🇺 Русский`

---

## Roadmap

- [x] 27 programmer archetypes with ASCII avatars
- [x] 5-model, 15-dimension behavioral analysis
- [x] Euclidean distance type matching (raw score centroids)
- [x] Animated statusline buddy (active + idle modes)
- [x] Companion skill auto-installation
- [x] Mood system with time-based expressions
- [x] Evolution tracking + timeline visualization
- [x] 15 achievement system
- [x] 9-language support
- [x] ASCII share card generation
- [x] Incremental update (new messages only)
- [x] Auto-update on session start (50+ new msgs, 24h cooldown)
- [x] Communication style adaptation (style only, not reasoning)
- [x] Background animation daemon (continuous smooth animation)
- [x] Social media share card PNG (`sbti share`)


---

## References

- [SBTI (Social and Behavioral Traits Index)](https://sbti.fancc.de5.net/) — the original programmer personality test this skill is built on
- [VibePortrait](https://github.com/dadwadw233/VibePortrait) — AI conversation portrait skill, inspiration for README design

---

<div align="center">

**Personality tests ask who you think you are. Your conversations show who you actually are.**

**性格测试问的是你觉得自己是谁。你的对话，展示的是你真正是谁。**

<br>

