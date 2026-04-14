<div align="center">

```
  ╭─────────────────────────────────────────────────────╮
  │                                                     │
  │   ███████╗██████╗ ████████╗██╗                      │
  │   ██╔════╝██╔══██╗╚══██╔══╝██║                      │
  │   ███████╗██████╔╝   ██║   ██║                      │
  │   ╚════██║██╔══██╗   ██║   ██║                      │
  │   ███████║██████╔╝   ██║   ██║                      │
  │   ╚══════╝╚═════╝    ╚═╝   ╚═╝                      │
  │              B U D D Y                              │
  │                                                     │
  │   Your AI conversations reveal who you really are.  │
  │   No questionnaire. No faking. Just you.            │
  │                                                     │
  │        \----/                                       │
  │       /^\  /^\    "Saved. Next."                    │
  │      < V    V >      — Ctrl+S (CTRL)               │
  │      (  ----  )                                     │
  │       \ -[]- /                                      │
  │       [ CTRL ]                                      │
  │                                                     │
  ╰─────────────────────────────────────────────────────╯
```

<br>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-14b8a6?logo=anthropic&logoColor=white)](https://claude.ai/claude-code)
[![Codex](https://img.shields.io/badge/Codex-skill-10a37f?logo=openai&logoColor=white)](https://github.com/openai/codex)
[![GitHub stars](https://img.shields.io/github/stars/Li-xingXiao/sbti-buddy-skill?style=social)](https://github.com/Li-xingXiao/sbti-buddy-skill)

**Personality tests capture a moment. Your AI conversations reveal who you really are.**

**性格测试只能测出一瞬间的你。和 AI 的长期对话，才是真实的你。**

[English](#what-is-sbti-buddy) · [中文](#sbti-buddy-是什么)

</div>

---

### ⚡ 30-Second Demo

```bash
# Install (one time)
cp -R skills/sbti-buddy ~/.claude/skills/sbti-buddy

# Run
sbti
```

**Input:** Your `~/.claude/history.jsonl` + `~/.codex/history.jsonl` (read-only, never sent anywhere)

**Output:**

| Output | What you get |
|--------|-------------|
| 🎴 ASCII Share Card | Your SBTI type, DNA pattern, dimension bars — paste anywhere |
| 🐾 Animated Buddy | ASCII companion that lives in your Claude Code statusline |
| 🧠 Companion Skill | Auto-installed skill — buddy reacts, comments, tracks your mood |
| 📈 Evolution Log | Type change history — watch yourself grow over time |

<details>
<summary><b>📸 What it looks like (click to expand)</b></summary>

<br>

```
╭──────────────────────────────────────────╮
│  ✦ SBTI BUDDY CARD                      │
│  ══════════════════                      │
│                                          │
│       \----/       CTRL                  │
│      /^\  /^\      (拿捏者)              │
│     < V    V >                           │
│     (  ----  )     Match:  91%           │
│      \ -[]- /     Style: Architect       │
│      [ CTRL ]      DNA: ██▓░██▓░██       │
│                                          │
│  "Master of the codebase, PR terminator" │
│                                          │
│  ─── Dimensions ─────────────────────    │
│  S  ██ ██ ██                             │
│  E  ██ ▓░ ██                             │
│  A  ▓░ ██ ██                             │
│  Ac ██ ██ ██                             │
│  So ▓░ ██ ▓░                             │
│                                          │
│  ★ ★ ★ ★ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆       │
│                                          │
│  Confidence: Deep Portrait               │
│  Generated:  2026-04-14                  │
╰──────────────────────────────────────────╯
```

*The card includes: SBTI type with programmer avatar · 5-model dimension DNA bars · dev style · match similarity · 15 achievement badges · confidence level.*

</details>

---

## What is SBTI Buddy?

A skill for **Claude Code** and **Codex**. It reads your AI conversation history — **no questionnaire needed** — and generates:

- **🎴 Programmer Personality Type** — 27 programmer-specific archetypes across 5 behavioral models and 15 dimensions. Not generic MBTI — types like `CTRL (Ctrl+S the Architect)`, `DEAD (404 the Unmotivated)`, `MONK (Vim僧 the Terminal Sage)`
- **🐾 Animated ASCII Buddy** — a companion that lives in your Claude Code statusline. It blinks when idle, animates while Claude responds, and changes mood throughout the day
- **🧠 Companion Skill** — auto-installed skill that gives your buddy a voice. It comments on your code (in character), reminds you to rest after 10pm, and celebrates your achievements
- **📈 Evolution Tracking** — your type changes over time. SBTI Buddy records every shift and shows your programmer growth timeline
- **🏆 15 Achievements** — unlock badges like `🦉 Night Owl`, `💀 Back from Dead`, `🧘 Code Monk`

> **Why no questionnaire?** Personality tests measure how you *think* you are in that moment. But your real coding personality shows in thousands of conversations — how you ask for help, how you respond to errors, how you communicate with AI. That can't be faked. SBTI Buddy reads the truth from your history.

---

## SBTI Buddy 是什么？

一个 **Claude Code / Codex 技能**。读取你的 AI 对话历史——**不需要做任何测试题**——自动生成：

- **🎴 程序员人格类型** — 27 种程序员专属人格原型，覆盖 5 大行为模型、15 个维度。不是泛泛的 MBTI，而是 `CTRL（拿捏者）`、`DEAD（404 开发者）`、`MONK（Vim僧）` 这样的程序员特有类型
- **🐾 动态 ASCII 伙伴** — 住在你 Claude Code 状态栏里的小伙伴。空闲时偶尔眨眼，响应时活蹦乱跳，全天候陪你 coding
- **🧠 伴侣技能** — 自动安装的技能，让你的 buddy 拥有独特的声音。它会用角色语气评论你的代码，晚上 10 点后提醒你休息
- **📈 进化追踪** — 你的类型会随时间变化。SBTI Buddy 记录每次转变，展示你的程序员成长轨迹
- **🏆 15 个成就** — 解锁 `🦉 夜猫子`、`💀 起死回生`、`🧘 代码僧侣` 等徽章

> **为什么不做测试题？** 性格测试只能测出你「此刻觉得自己是什么样的人」。但你真实的编程人格，藏在成千上万次对话里——你怎么求助、怎么应对报错、怎么和 AI 沟通。这些没法伪装。SBTI Buddy 从你的历史中读出真相。

---

## Quick Start / 快速开始

**Claude Code (manual):**

```bash
git clone https://github.com/Li-xingXiao/sbti-buddy-skill.git
cp -R sbti-buddy-skill/skills/sbti-buddy ~/.claude/skills/sbti-buddy
# Then in Claude Code:
sbti
```

**Codex:**

```bash
$skill-installer install https://github.com/Li-xingXiao/sbti-buddy-skill/tree/main/skills/sbti-buddy
# Then: Analyze my SBTI type
```

---

## How It Works / 工作流程

```
  📜 Your conversation history (~/.claude/history.jsonl)
                        │
          ┌─────────────▼──────────────┐
          │  Read messages (Quick/Full) │
          │  9 languages · 4 sources    │
          └─────────────┬──────────────┘
                        │
          ┌─────────────▼──────────────┐
          │  Score 15 dimensions        │
          │  5 models × 3 sub-dims     │
          │  S · E · A · Ac · So        │
          └─────────────┬──────────────┘
                        │
          ┌─────────────▼──────────────┐
          │  Manhattan distance match   │
          │  → Best of 27 types         │
          └─────────────┬──────────────┘
                        │
          ┌─────────────▼──────────────┐
          │  Generate outputs           │
          │  🎴 Card  🐾 Buddy  🧠 Skill│
          └─────────────┬──────────────┘
                        │
          ┌─────────────▼──────────────┐
          │  Install companion skill    │
          │  + statusline animation     │
          └────────────────────────────┘
```

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
| ✨ **Special** | `HHHH` Hello World · `DRUNK` Late Night Coder · `DIOR-s` Refactor君 |

Each type comes with: ASCII avatar · programmer-flavored intro · coding portrait · buddy catchphrase · dev style label.

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

---

## Buddy System / 伙伴系统

### 🐾 Animated Statusline Buddy

Your buddy lives in the Claude Code statusline — not just a static image.

| Mode | Behavior |
|------|----------|
| **Active** (Claude responding) | Frequent blink, talk, ear wiggle, hair sway |
| **Idle** (waiting for input) | Occasional blink (~6s), ear twitch (~15s) |

Powered by `PreToolUse`/`PostToolUse` hooks + statusline renderer — the same architecture as `/buddy`.

### 😊 Mood System

| Time | Mood | Expression |
|------|------|-----------|
| 06:00–12:00 | Energized | `◉▽◉` |
| 12:00–18:00 | Focused | `◉_◉` |
| 18:00–22:00 | Winding down | `◉◡◉` |
| 22:00–06:00 | Night owl | `◉ᵕ◉` + rest reminder |

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
| `sbti match` | Compare compatibility with another user |
| `sbti roast` | Your buddy roasts your coding style |
| `sbti fortune` | Daily coding fortune based on your type |
| `update my sbti` | Incremental update (new messages only, fast) |

---

## Privacy / 隐私

- Only reads local history files — **nothing is sent externally**
- API keys, tokens, passwords, file paths, PII are **auto-redacted** from all analysis
- Companion skill contains **zero raw messages** — only abstracted personality traits
- All processing happens in your Claude Code session

---

## Requirements / 环境要求

- Claude Code or Codex
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
- [x] Manhattan distance type matching
- [x] Animated statusline buddy (active + idle modes)
- [x] Companion skill auto-installation
- [x] Mood system with time-based expressions
- [x] Evolution tracking + timeline visualization
- [x] 15 achievement system
- [x] 9-language support
- [x] ASCII share card generation
- [x] Incremental update (new messages only)
- [ ] Community type sharing platform
- [ ] Cross-machine buddy sync via GitHub
- [ ] Team compatibility dashboard

---

<div align="center">

**Personality tests ask who you think you are. Your conversations show who you actually are.**

**性格测试问的是你觉得自己是谁。你的对话，展示的是你真正是谁。**

<br>

```
       \----/
      /^\  /^\
     < V    V >    "Saved. Next."
     (  ----  )
      \ -[]- /
      [ CTRL ]
```

</div>
