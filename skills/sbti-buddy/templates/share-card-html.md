# SBTI Share Card HTML Template

Reference template for the `sbti share` command. Claude reads this template, fills all placeholders from profile.json / evolution.json / buddy-frames.json, generates a type-specific roast, and writes a self-contained HTML file for Chrome headless screenshot.

---

## Card Specifications

- **Dimensions**: 1200 x 630 px (Twitter / OpenGraph standard)
- **Output**: `/tmp/sbti-share-card.html` → Chrome headless @ 2x DPR → `/tmp/sbti-share-card.png` (2400 x 1260 actual pixels)
- **Theme**: Dark terminal aesthetic
- **Constraints**: Self-contained HTML + inline CSS. No JavaScript, no external resources, no CDN links.

### Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `bg-primary` | `#0d1117` | Card background |
| `bg-secondary` | `#161b22` | Zone backgrounds, terminal box |
| `bg-terminal` | `#1e1e2e` | ASCII avatar area |
| `border` | `#30363d` | Borders, dividers |
| `text-primary` | `#e6edf3` | Main text |
| `text-muted` | `#8b949e` | Labels, footer |
| `accent` | `#58a6ff` | Type code, section headers |
| `avatar-green` | `#a6e3a1` | ASCII avatar text |
| `bar-low` | `#f97583` | Score bar (0-33) |
| `bar-mid` | `#e3b341` | Score bar (34-66) |
| `bar-high` | `#56d364` | Score bar (67-100) |
| `badge-gold` | `#ffd700` | Achievement stars |
| `roast-bg` | `#1c2128` | Roast box background |

### Font Stack

```css
body { font-family: 'Noto Sans CJK SC', 'Noto Sans CJK TC', 'Noto Sans CJK JP', 'Noto Sans CJK KR', 'Noto Sans', sans-serif; }
.avatar { font-family: 'Noto Sans Mono', 'DejaVu Sans Mono', monospace; }
```

---

## HTML Template

```html
<!DOCTYPE html>
<html lang="{{LANG}}">
<head>
<meta charset="UTF-8">
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }

html {
  background: #0d1117;
}

body {
  width: 1200px;
  height: 630px;
  overflow: hidden;
  background: linear-gradient(135deg, #0d1117 0%, #161b22 100%);
  color: #e6edf3;
  font-family: 'Noto Sans CJK SC', 'Noto Sans CJK TC', 'Noto Sans CJK JP', 'Noto Sans CJK KR', 'Noto Sans', sans-serif;
}

.card {
  display: grid;
  grid-template-columns: 300px 1fr 1fr;
  grid-template-rows: 1fr 44px;
  height: 100%;
  padding: 28px 32px 0 32px;
  gap: 0 28px;
}

/* === Zone A: Identity === */
.zone-a { display: flex; flex-direction: column; gap: 14px; }

.terminal-box {
  background: #1e1e2e;
  border: 1px solid #30363d;
  border-radius: 10px;
  overflow: hidden;
}
.title-bar {
  background: #2d333b;
  padding: 8px 12px;
  display: flex;
  align-items: center;
  gap: 6px;
}
.dot { width: 10px; height: 10px; border-radius: 50%; }
.dot.red { background: #f85149; }
.dot.yellow { background: #e3b341; }
.dot.green { background: #56d364; }
.title-text {
  margin-left: 8px;
  font-size: 11px;
  color: #8b949e;
  font-family: 'Noto Sans Mono', monospace;
}
.avatar {
  font-family: 'Noto Sans Mono', 'DejaVu Sans Mono', monospace;
  font-size: 14px;
  line-height: 1.3;
  color: #a6e3a1;
  padding: 10px 16px 12px;
  white-space: pre;
}

.type-info { padding: 0 4px; }
.type-code {
  font-size: 36px;
  font-weight: 800;
  color: #58a6ff;
  letter-spacing: 2px;
}
.type-name {
  font-size: 14px;
  color: #8b949e;
  margin-top: 2px;
}
.similarity {
  font-size: 13px;
  color: #8b949e;
  margin-top: 6px;
}
.similarity strong {
  color: #56d364;
  font-size: 18px;
}
.catchphrase {
  font-size: 12px;
  color: #8b949e;
  font-style: italic;
  margin-top: 8px;
  line-height: 1.4;
}

/* === Zone B: Stats === */
.zone-b { display: flex; flex-direction: column; gap: 12px; padding-top: 4px; }

.section-title {
  font-size: 12px;
  font-weight: 600;
  color: #58a6ff;
  text-transform: uppercase;
  letter-spacing: 2px;
  padding-bottom: 6px;
  border-bottom: 1px solid #30363d;
}
.score-bars { display: flex; flex-direction: column; gap: 10px; margin-top: 4px; }
.score-row { display: flex; align-items: center; gap: 8px; }
.model-label {
  font-size: 13px;
  font-weight: 700;
  color: #e6edf3;
  width: 24px;
  text-align: right;
}
.model-name {
  font-size: 11px;
  color: #8b949e;
  width: 72px;
}
.bar-container {
  flex: 1;
  height: 14px;
  background: #21262d;
  border-radius: 7px;
  overflow: hidden;
}
.bar-fill {
  height: 100%;
  border-radius: 7px;
  background: linear-gradient(90deg, #f97583, #e3b341 50%, #56d364);
  transition: width 0.3s;
}
.score-value {
  font-size: 12px;
  font-weight: 600;
  color: #e6edf3;
  width: 28px;
  text-align: right;
}

.dna-pattern {
  font-family: 'Noto Sans Mono', monospace;
  font-size: 13px;
  color: #8b949e;
  margin-top: 4px;
}
.dev-intro {
  font-size: 12px;
  color: #8b949e;
  font-style: italic;
  line-height: 1.5;
  margin-top: 4px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

/* === Zone C: Meta + Humor === */
.zone-c { display: flex; flex-direction: column; gap: 12px; padding-top: 4px; }

.evolution-timeline { display: flex; flex-direction: column; gap: 6px; }
.timeline-track {
  display: flex;
  align-items: center;
  gap: 0;
  margin-top: 6px;
}
.timeline-node {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-width: 72px;
}
.timeline-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: #58a6ff;
  border: 2px solid #0d1117;
  z-index: 1;
}
.timeline-dot.shift { background: #f0883e; }
.timeline-dot.current { background: #56d364; box-shadow: 0 0 8px #56d364; }
.timeline-type {
  font-size: 12px;
  font-weight: 700;
  color: #e6edf3;
  margin-top: 4px;
}
.timeline-meta {
  font-size: 10px;
  color: #8b949e;
}
.timeline-line {
  flex: 1;
  height: 2px;
  background: #30363d;
  margin: 0 -4px;
  align-self: flex-start;
  margin-top: 5px;
}

.roast-box {
  background: #1c2128;
  border: 1px solid #30363d;
  border-radius: 10px;
  padding: 12px 16px;
  flex: 1;
}
.roast-header {
  font-size: 12px;
  font-weight: 600;
  color: #f0883e;
  margin-bottom: 6px;
}
.roast-text {
  font-size: 13px;
  color: #e6edf3;
  line-height: 1.6;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
}

.achievements-row {
  font-size: 16px;
  letter-spacing: 4px;
  color: #ffd700;
  white-space: nowrap;
  overflow: hidden;
}
.achievements-row .locked { opacity: 0.3; }

/* === Footer === */
.footer {
  grid-column: 1 / -1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 4px;
  border-top: 1px solid #30363d;
  font-size: 11px;
  color: #8b949e;
}
.footer .brand {
  font-weight: 700;
  color: #58a6ff;
}
</style>
</head>
<body>
<div class="card">

  <!-- Zone A: Identity -->
  <div class="zone-a">
    <div class="terminal-box">
      <div class="title-bar">
        <span class="dot red"></span>
        <span class="dot yellow"></span>
        <span class="dot green"></span>
        <span class="title-text">~ buddy.sh</span>
      </div>
      <pre class="avatar">{{AVATAR_LINES}}</pre>
    </div>
    <div class="type-info">
      <div class="type-code">{{TYPE_CODE}}</div>
      <div class="type-name">{{TYPE_CN}} / {{BUDDY_NAME}}</div>
      <div class="similarity">Match: <strong>{{SIMILARITY}}%</strong></div>
      <div class="catchphrase">"{{CATCHPHRASE}}"</div>
    </div>
  </div>

  <!-- Zone B: Stats -->
  <div class="zone-b">
    <div class="section-title">{{DIMENSIONS_LABEL}}</div>
    <div class="score-bars">
      <div class="score-row">
        <span class="model-label">S</span>
        <span class="model-name">{{S_NAME}}</span>
        <div class="bar-container"><div class="bar-fill" style="width:{{S_AVG}}%"></div></div>
        <span class="score-value">{{S_AVG}}</span>
      </div>
      <div class="score-row">
        <span class="model-label">E</span>
        <span class="model-name">{{E_NAME}}</span>
        <div class="bar-container"><div class="bar-fill" style="width:{{E_AVG}}%"></div></div>
        <span class="score-value">{{E_AVG}}</span>
      </div>
      <div class="score-row">
        <span class="model-label">A</span>
        <span class="model-name">{{A_NAME}}</span>
        <div class="bar-container"><div class="bar-fill" style="width:{{A_AVG}}%"></div></div>
        <span class="score-value">{{A_AVG}}</span>
      </div>
      <div class="score-row">
        <span class="model-label">Ac</span>
        <span class="model-name">{{AC_NAME}}</span>
        <div class="bar-container"><div class="bar-fill" style="width:{{AC_AVG}}%"></div></div>
        <span class="score-value">{{AC_AVG}}</span>
      </div>
      <div class="score-row">
        <span class="model-label">So</span>
        <span class="model-name">{{SO_NAME}}</span>
        <div class="bar-container"><div class="bar-fill" style="width:{{SO_AVG}}%"></div></div>
        <span class="score-value">{{SO_AVG}}</span>
      </div>
    </div>
    <div class="dna-pattern">DNA: {{PATTERN}}</div>
    <div class="dev-intro">"{{DEV_INTRO}}"</div>
  </div>

  <!-- Zone C: Meta + Humor -->
  <div class="zone-c">
    <div class="evolution-timeline">
      <div class="section-title">{{EVOLUTION_LABEL}}</div>
      <div class="timeline-track">
        {{TIMELINE_NODES}}
      </div>
    </div>
    <div class="roast-box">
      <div class="roast-header">{{ROAST_HEADER}}</div>
      <div class="roast-text">{{ROAST_TEXT}}</div>
    </div>
    <div class="achievements-row">{{ACHIEVEMENT_BADGES}}</div>
  </div>

  <!-- Footer -->
  <div class="footer">
    <span class="brand">SBTI Buddy</span>
    <span>{{CONFIDENCE}} · {{MESSAGE_COUNT}} msgs</span>
    <span>{{DATE}}</span>
  </div>

</div>
</body>
</html>
```

---

## Placeholder Reference

| Placeholder | Source | Notes |
|-------------|--------|-------|
| `LANG` | profile.json `meta.lang` | HTML lang attribute (zh/en/ja/ko/...) |
| `AVATAR_LINES` | buddy-frames.json `base` array | 6 lines joined by `\n`. Copy verbatim into `<pre>` — backslashes render correctly in `<pre>` tags, do NOT escape them. |
| `TYPE_CODE` | profile.json `type.code` | Never translated |
| `TYPE_CN` | profile.json `type.cn` | Never translated |
| `BUDDY_NAME` | profile.json `buddyName` | Never translated |
| `SIMILARITY` | profile.json `type.similarity` | Integer 0-100 |
| `CATCHPHRASE` | type-profiles.md, select `{LANG}` version | Buddy catchphrase |
| `S_AVG` / `E_AVG` / ... | Average of 3 sub-dimension raw scores | `S_AVG = round((S1.raw + S2.raw + S3.raw) / 3)` |
| `S_NAME` / `E_NAME` / ... | Localized model names (see label table below) | |
| `DIMENSIONS_LABEL` | Localized "Dimensions" header | |
| `PATTERN` | profile.json `pattern` | e.g. `HHH-HMH-MHH-HHH-MHM` |
| `DEV_INTRO` | type-profiles.md, buddy intro | Select `{LANG}` version, max 2 lines |
| `EVOLUTION_LABEL` | Localized "Evolution" header | |
| `TIMELINE_NODES` | Generated from evolution.json (see below) | |
| `ROAST_HEADER` | Localized roast section header | |
| `ROAST_TEXT` | **Claude generates fresh each time** | See humor guidelines below |
| `ACHIEVEMENT_BADGES` | From evolution.json history | See achievement rendering below |
| `CONFIDENCE` | profile.json `meta.confidence` | |
| `MESSAGE_COUNT` | profile.json `meta.messageCount` | |
| `DATE` | Current date `YYYY-MM-DD` | |

---

## Score Bar Rendering

Each model score is the **average of its 3 sub-dimensions**:

```
S_AVG  = round((S1.raw + S2.raw + S3.raw) / 3)
E_AVG  = round((E1.raw + E2.raw + E3.raw) / 3)
A_AVG  = round((A1.raw + A2.raw + A3.raw) / 3)
AC_AVG = round((Ac1.raw + Ac2.raw + Ac3.raw) / 3)
SO_AVG = round((So1.raw + So2.raw + So3.raw) / 3)
```

Set `style="width:{{X_AVG}}%"` on the `.bar-fill` div.

---

## Timeline Node Rendering

Take the **last 3 entries** from `evolution.json history`. For each entry, generate:

```html
<div class="timeline-node">
  <div class="timeline-dot {{CLASS}}"></div>
  <div class="timeline-type">{{TYPE}}</div>
  <div class="timeline-meta">{{SIM}}% · {{MSGS}}msgs</div>
</div>
```

Between nodes, insert: `<div class="timeline-line"></div>`

**Node classes:**
- Last entry (current): `class="timeline-dot current"`
- Entry where type differs from previous: `class="timeline-dot shift"`
- Otherwise: `class="timeline-dot"`

If only 1 entry exists, show a single node with no lines.

---

## Achievement Badge Rendering

Scan `evolution.json history` for all `achievements_unlocked` arrays. Collect all unlocked achievement IDs.

For each of the 15 achievements (in order from companion-system.md §4.1), output:
- Unlocked: `<span>{{BADGE_EMOJI}}</span>` (the emoji from §4.1)
- Locked: `<span class="locked">{{BADGE_EMOJI}}</span>` (same emoji, dimmed via CSS opacity)

---

## Multilingual Labels

Generate all text labels in the user's detected language (`meta.lang`). Reference table for core languages:

| Key | zh | en | ja | ko |
|-----|----|----|----|----|
| `DIMENSIONS_LABEL` | 维度 | Dimensions | 次元 | 차원 |
| `EVOLUTION_LABEL` | 进化 | Evolution | 進化 | 진화 |
| `ROAST_HEADER` | 🎤 吐槽时间 | 🎤 Roast Zone | 🎤 ツッコミ | 🎤 로스트 |
| `S_NAME` | 自我认知 | Self-Image | 自己認識 | 자기인식 |
| `E_NAME` | AI 关系 | AI Relations | AI関係 | AI 관계 |
| `A_NAME` | 技术态度 | Tech Views | 技術態度 | 기술태도 |
| `AC_NAME` | 行动力 | Execution | 行動力 | 실행력 |
| `SO_NAME` | 社交 | Social | 社交 | 소셜 |

For other languages (es/fr/de/pt/ru), generate appropriate translations.

---

## Humor Generation Guidelines

The `ROAST_TEXT` is the card's centerpiece humor element. Claude generates it fresh each invocation. Max 2-3 sentences. Generated in `{LANG}`.

### Source Material

Combine up to 3 humor angles:

**1. Type-specific roast** (primary, always include):
- Use the same rules as `sbti roast` (see SKILL.md):
  - High S types: Confident backhanded compliments
  - Low S types: Self-deprecating shared humor
  - High Ac types: Speed burns ("You debug slower than you save")
  - Low Ac types: Lazy humor
  - High So types: Social burns about coding alone
  - Low So types: Introvert jokes about pair programming

**2. Stats commentary** (pick one if applicable):
- Low similarity (< 70%): "Even the algorithm isn't sure about you"
- All dimensions M: "You're the `undefined` of the programming world"
- Very high similarity (> 90%): "You ARE this type. Literally no deviation."
- Single model all H: "Your {MODEL} is maxed out — compensating for something?"
- Single model all L: "Your {MODEL} called. It wants to exist."

**3. Evolution commentary** (pick one if applicable):
- 3+ type shifts: "Your personality has more releases than your npm packages"
- 0 shifts (first analysis): "First analysis. The beginning of an identity crisis."
- Shifted from DEAD: "You escaped 404. Not everyone does."
- Same type 3+ times: "At least SOMETHING in your life is stable"

### Tone Rules

- Fun, warm, programmer-humor. Think tech Twitter / dev memes.
- Target coding patterns, NEVER personal traits.
- Keep it shareable — the person should WANT to post this.
- End with something positive or self-deprecating, never mean.

---

## Example (filled, CTRL type, zh)

For a user with:
- Type: CTRL, cn: 拿捏者, buddyName: Ctrl+S, similarity: 87%
- Pattern: HHH-HMH-MHH-HHH-MHM
- 2 evolution entries (DEAD → CTRL)
- 3 achievements unlocked
- Lang: zh

The `ROAST_TEXT` might be:

> 你写代码的姿态像个架构师，但 git log 出卖了你——80% 都是 "fix typo"。别担心，Ctrl+S 从不 judge（骗你的）。

The `TIMELINE_NODES` would render:

```html
<div class="timeline-node">
  <div class="timeline-dot"></div>
  <div class="timeline-type">DEAD</div>
  <div class="timeline-meta">72% · 30msgs</div>
</div>
<div class="timeline-line"></div>
<div class="timeline-node">
  <div class="timeline-dot current shift"></div>
  <div class="timeline-type">CTRL</div>
  <div class="timeline-meta">87% · 150msgs</div>
</div>
```

---

## Chrome Screenshot Command

Use `--force-device-scale-factor=2` to render at 2x resolution for a sharp, HD image (2400x1260 actual pixels).

```bash
google-chrome --headless --disable-gpu --no-sandbox \
  --force-device-scale-factor=2 \
  --screenshot=/tmp/sbti-share-card.png \
  --window-size=1200,630 \
  file:///tmp/sbti-share-card.html
```

If this fails (e.g., no display available), retry with:

```bash
xvfb-run --auto-servernum google-chrome --headless --disable-gpu --no-sandbox \
  --force-device-scale-factor=2 \
  --screenshot=/tmp/sbti-share-card.png \
  --window-size=1200,630 \
  file:///tmp/sbti-share-card.html
```

Verify the PNG was created: check file exists and size > 0. Expected dimensions: 2400x1260px.
