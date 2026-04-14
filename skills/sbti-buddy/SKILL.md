---
name: "sbti-buddy"
description: "Programmer SBTI personality analyzer & ASCII buddy companion. Analyzes your AI conversation history (no questionnaire needed!) to determine your SBTI type among 27 programmer archetypes, generates an ASCII buddy avatar, and installs it as a Claude Code companion skill. Supports all major languages. Triggers on: 'sbti', 'sbti buddy', 'analyze my sbti', 'show my buddy', 'sbti card', 'sbti timeline', 'sbti match', 'sbti roast', 'sbti fortune', 'sbti spectrum', 'update my sbti', 'what programmer type am I', 'my coding personality'."
---

# SBTI Buddy

Programmer SBTI personality analyzer & companion generator.
Determines your SBTI type from AI conversation history — no questionnaire needed.
Generates an ASCII buddy that lives in your Claude Code sessions.

## Command routing

| Trigger | Action |
|---------|--------|
| "sbti" / "analyze my sbti" / "what programmer type am I" / "my coding personality" | **Analyze** (full analysis, Steps 0-7) |
| "sbti card" | **Card** (show buddy card) |
| "show my buddy" / "buddy" | **Buddy** (animated statusline buddy) |
| "sbti timeline" | **Timeline** (show type evolution) |
| "sbti spectrum" | **Spectrum** (show top 5 matching types) |
| "sbti match" / "sbti compatibility" | **Match** (compare with another user) |
| "sbti roast" | **Roast** (buddy roasts your coding style) |
| "sbti fortune" | **Fortune** (daily coding fortune based on type) |
| "update my sbti" | **Update** (incremental update) |

If ambiguous, ask the user which action they want.

---

## Analyze (full analysis)

### Step 0: Ask analysis mode

Before reading any data, ask the user:

> **How thorough should the analysis be?**
>
> 1. **Quick** — Sample ~50 recent messages. Fast, good for a first look.
> 2. **Full** — Read ALL messages. Higher cost, maximum accuracy.

Default to **Quick** if the user doesn't specify.

### Step 1: Locate and read conversation data

Read from ALL available sources:

| Source | Path | Message field |
|--------|------|---------------|
| Claude Code history | `~/.claude/history.jsonl` | `display` |
| Claude Code projects | `~/.claude/projects/**/*.jsonl` | `display` |

**Quick mode**: Read the last 50 non-empty messages from the primary source.
**Full mode**: Read all messages. For files >500 lines, read in batches of 500.

**Parse each line as JSON, extract message text.** Skip: empty, null, slash commands (starts with `/`), system messages.

**Minimum threshold**: < 20 messages → tell user to accumulate more history. Do not generate.

### Step 2: Analyze across 15 SBTI dimensions

Read the dimension mapping reference:
→ `references/programmer-dimensions.md`

For each of the 15 dimensions (S1-S3, E1-E3, A1-A3, Ac1-Ac3, So1-So3), analyze the conversation messages and produce a **0-100 raw score**.

**Rules:**
- Each dimension requires 3+ signals for confident scoring
- If signals are insufficient, default to 50 (M)
- Only score based on observable text behavior, never speculate
- Recent messages carry more weight (personality evolves)
- Detect signals in both Chinese and English

**Language detection**: Detect the user's primary language from message content. Supported languages:

| Code | Language | Detection heuristic |
|------|----------|---------------------|
| `zh` | 中文 | CJK Unified Ideographs (U+4E00-9FFF) dominant |
| `en` | English | Latin alphabet dominant, English stop words |
| `ja` | 日本語 | Hiragana/Katakana (U+3040-30FF) present |
| `ko` | 한국어 | Hangul (U+AC00-D7AF) dominant |
| `es` | Español | Latin + Spanish markers (¿¡ñ, common words) |
| `fr` | Français | Latin + French markers (ç, è, ê, common words) |
| `de` | Deutsch | Latin + German markers (ü, ö, ä, ß, common words) |
| `pt` | Português | Latin + Portuguese markers (ã, õ, common words) |
| `ru` | Русский | Cyrillic (U+0400-04FF) dominant |
| `auto` | Mixed | If no language > 50%, use the **language of the user's most recent 10 messages** |

Set `lang` to the detected code. **All output (buddy voice, card labels, fortune text, roast) should be in the user's detected language.** If mixed, default to `en`.

Dimension analysis is **language-agnostic** — signals are detected by semantic intent regardless of language (see `programmer-dimensions.md`).

**Time analysis**: If timestamps are available, extract hourly distribution for work rhythm and late-night detection.

### Step 3: Compute SBTI type via Euclidean distance

Read the scoring algorithm:
→ `references/scoring-algorithm.md`

1. **Map raw scores to L/M/H** (for display): 0-33 = L(1), 34-66 = M(2), 67-100 = H(3)
2. **Build pattern string**: e.g. `HHM-HLH-MLH-HHH-MHM`
3. **Apply jitter** (Step 3.5A): Add Gaussian noise (σ depends on confidence) to raw scores before matching — keeps type switching fluid and fun. Save **original** raw scores to profile.json, use **jittered** scores only for distance calculation
4. **Calculate Euclidean distance** from jittered scores to each type's centroid
5. **Apply novelty penalty** (Step 3.5B): If same type for N consecutive analyses, add penalty to that type's distance to encourage variety
6. **Compute exact_hits** using L/M/H vectors as tiebreaker
7. **Sort** by: distance asc → exact_hits desc → similarity desc
8. **Top match** = primary type; 2nd-5th = spectrum candidates
9. **HHHH fallback**: If best similarity < 60%, use HHHH
10. **Late Night Coder badge**: If >50% messages sent 00:00-05:00, add badge

### Step 4: Generate buddy avatar and personality

Read the avatar reference:
→ `references/ascii-avatars.md`

Read the type profiles:
→ `references/type-profiles.md`

Read the companion system:
→ `references/companion-system.md`

1. **Select ASCII avatar** for the matched type
2. **Apply current mood expression** based on time of day (see companion-system.md §2)
3. **Derive voice/tone** from dimension scores (see companion-system.md §1.2, §1.3)
4. **Generate buddy catchphrase** — a short, type-specific one-liner the buddy uses
5. **Generate dev-style intro** — a programmer-flavored one-sentence description
6. **Determine buddy name** from type mapping (see companion-system.md §1.1)

### Step 5: Check achievements and evolution

Read existing profile if it exists:
```bash
cat ~/.claude/sbti-buddy/profile.json 2>/dev/null
cat ~/.claude/sbti-buddy/evolution.json 2>/dev/null
```

1. **Check for type change**: Compare new type with last evolution entry
2. **Detect achievements**: Run through all 15 achievement conditions (see companion-system.md §4)
3. **Record evolution**: Append new entry to evolution.json
4. **If type changed**: Output evolution milestone message

### Step 6: Generate outputs and install companion

#### 6a: Write profile, evolution data, and statusline animation files

```
~/.claude/sbti-buddy/
├── profile.json              # Current analysis snapshot
├── evolution.json            # Type change history
├── buddy-frames.json         # Frame data (base + animation variants, JSON)
├── frames/                   # Pre-generated frame text files (no jq needed at runtime)
│   ├── base.txt              # Base frame (6 lines)
│   ├── blink.txt             # Blink variant (eyes closed)
│   ├── talk.txt              # Talk variant (mouth animated)
│   ├── wiggle.txt            # Ear wiggle variant
│   ├── sway.txt              # Hair sway variant
│   ├── mood_tired.txt        # Tired mood expression
│   ├── mood_frustrated.txt   # Frustrated mood expression
│   └── mood_celebrating.txt  # Celebrating mood expression
├── .animation-state          # Last activity timestamp (epoch seconds, hooks write)
├── .animate-pid              # Animation daemon PID file (auto-managed)
├── .current-render           # Pre-rendered current frame (written by daemon)
├── .current-mood             # Current mood: "happy"/"tired"/"frustrated"/"celebrating"
├── .last-auto-update         # Timestamp of last auto-update check
├── animate-loop.sh           # Background animation daemon
├── statusline-render.sh      # Statusline renderer (cat .current-render)
├── auto-update-check.sh      # Session start auto-update checker
└── hooks/
    ├── start-animation.sh    # PreToolUse hook (timestamp + daemon startup)
    └── stop-animation.sh     # PostToolUse hook (timestamp)
```

**profile.json** structure: see companion-system.md §6.
**evolution.json** structure: see companion-system.md §7.
**buddy-frames.json**: Generated from `ascii-avatars.md`, contains the matched type's 6 base lines + animation variants in JSON format.
**frames/**: Pre-generated plain text frame files. Each file contains the full 6-line ASCII art with the appropriate line substitution already applied. Generated from `buddy-frames.json` during installation — see `ascii-avatars.md` §2 for the generation process. This eliminates `jq` dependency at runtime (~16ms per render vs ~200ms with jq). **Important**: Use Python (not awk/sed/shell) to generate these files — shell tools strip backslashes from ASCII art.
**animate-loop.sh**: Background animation daemon. Pre-renders frames to `.current-render` continuously — 0.4s/frame in active mode, 1.2s/frame in idle mode. Started by `start-animation.sh` on first tool call, self-terminates after 12h. See `ascii-avatars.md` §3.
**statusline-render.sh**: Ultra-fast renderer — just `cat .current-render`. Falls back to direct base frame render if daemon hasn't started. See `ascii-avatars.md` §4.
**hooks/**: `start-animation.sh` writes epoch timestamp to `.animation-state` AND ensures the animation daemon is running (starts it if not). `stop-animation.sh` writes epoch timestamp only. The daemon uses the timestamp to determine active (< 5s) vs idle mode.

#### 6b: Generate and install companion skill

Read the companion skill template:
→ `references/companion-skill-template.md`

Generate files at `~/.claude/skills/sbti-buddy-companion/`:

```
sbti-buddy-companion/
├── SKILL.md              # Companion skill entry point
├── personality.md        # Buddy voice, tone, catchphrase, focus
├── communication-style.md # Claude's communication style adaptation
├── avatar.md             # ASCII avatar + mood variants
└── achievements.md       # Unlocked achievements list
```

**SKILL.md** frontmatter:
```yaml
name: "sbti-buddy-companion"
description: "Your SBTI buddy companion: {BUDDY_NAME} ({TYPE_CODE}). Adapts communication style and adds buddy personality. Triggers on: 'show my buddy', 'buddy', 'sbti card', 'sbti timeline'."
```

**communication-style.md**: Generated from SBTI dimension scores. Adapts Claude's overall communication style (verbosity, tone, assertiveness, proactivity, decision framing) to match the user's personality. See `companion-skill-template.md` §5 for the template and filling rules, and `companion-system.md` §1.4 for the dimension mapping.

**Companion behavior rules** (written into the skill):
- `communication-style.md` rules apply to ALL Claude responses (not just buddy comments)
- In daily coding sessions, the companion MAY append a 1-line buddy comment at the end of responses (max 1 per 3 interactions, do NOT affect technical accuracy)
- Comment style matches the buddy's voice (see personality.md)
- Show mood-appropriate expression (see avatar.md)
- Track context for mood changes (see companion-system.md §2.3)
- After 22:00, append "remember to rest" reminder in buddy's voice

#### 6c: Configure statusline and hooks

**Coexistence with `/buddy`**: The built-in `/buddy` companion (input box area) and SBTI Buddy (statusline) are **two separate UI systems** that coexist peacefully — no need to disable either one.

| | `/buddy` (built-in) | SBTI Buddy |
|---|---|---|
| Location | Beside input box + speech bubbles | Bottom statusline |
| Config | Runtime session state | `statusLine` in settings.json |
| Personality | Built-in companion | SBTI companion skill |

**No conflict**: They occupy different UI areas. Users can have both active simultaneously.

**Before writing statusLine config**, back up any existing entry:
```bash
if command -v jq &>/dev/null && [ -f ~/.claude/settings.json ]; then
  jq '.statusLine // empty' ~/.claude/settings.json > ~/.claude/sbti-buddy/.prev-statusline.json 2>/dev/null
fi
```

For hooks, **append** SBTI entries to existing hook arrays (preserve other hooks). For `statusLine`, SBTI Buddy **replaces** the existing value (only one statusLine can be active). The backup in `.prev-statusline.json` allows restoration if SBTI is uninstalled.

Add the following to the user's Claude Code settings (`~/.claude/settings.json`):

```json
{
  "statusLine": {
    "type": "command",
    "command": "bash ~/.claude/sbti-buddy/statusline-render.sh",
    "padding": 0
  },
  "hooks": {
    "PreToolUse": [{
      "matcher": "",
      "hooks": [{
        "type": "command",
        "command": "bash ~/.claude/sbti-buddy/hooks/start-animation.sh"
      }]
    }],
    "PostToolUse": [{
      "matcher": "",
      "hooks": [{
        "type": "command",
        "command": "bash ~/.claude/sbti-buddy/hooks/stop-animation.sh"
      }]
    }],
    "SessionStart": [{
      "matcher": "",
      "hooks": [{
        "type": "command",
        "command": "bash ~/.claude/sbti-buddy/auto-update-check.sh"
      }]
    }]
  }
}
```

**Important**: Merge into existing settings, do not overwrite. For hooks, **append** SBTI entries to existing hook arrays (preserve other hooks). For `statusLine`, SBTI Buddy **replaces** the existing value (only one statusLine can be active). The backup in `.prev-statusline.json` allows restoration if SBTI is uninstalled.

Initialize runtime state files:
```bash
mkdir -p ~/.claude/sbti-buddy/frames
echo "0" > ~/.claude/sbti-buddy/.animation-state
echo "happy" > ~/.claude/sbti-buddy/.current-mood
echo "0" > ~/.claude/sbti-buddy/.last-auto-update
chmod +x ~/.claude/sbti-buddy/animate-loop.sh
chmod +x ~/.claude/sbti-buddy/statusline-render.sh
chmod +x ~/.claude/sbti-buddy/auto-update-check.sh
chmod +x ~/.claude/sbti-buddy/hooks/start-animation.sh
chmod +x ~/.claude/sbti-buddy/hooks/stop-animation.sh
```

**auto-update-check.sh** logic:
```bash
#!/bin/bash
# Auto-update check — runs on SessionStart
# Only triggers incremental update if:
#   1. profile.json exists (user has run analysis at least once)
#   2. At least 24 hours since last auto-update
#   3. At least 50 new messages since last analysis

SBTI_DIR="$HOME/.claude/sbti-buddy"
PROFILE="$SBTI_DIR/profile.json"
LAST_CHECK="$SBTI_DIR/.last-auto-update"
HISTORY="$HOME/.claude/history.jsonl"

# Skip if no profile (never analyzed)
[ ! -f "$PROFILE" ] && exit 0

# Skip if checked within 24 hours
LAST_TS=$(cat "$LAST_CHECK" 2>/dev/null || echo "0")
NOW=$(date +%s)
ELAPSED=$(( NOW - LAST_TS ))
[ "$ELAPSED" -lt 86400 ] && exit 0

# Count new messages since last analysis
LAST_INDEX=$(jq -r '.meta.lastMessageIndex // 0' "$PROFILE")
CURRENT_LINES=$(wc -l < "$HISTORY" 2>/dev/null || echo "0")
NEW_MSGS=$(( CURRENT_LINES - LAST_INDEX ))

# Skip if fewer than 50 new messages
[ "$NEW_MSGS" -lt 50 ] && exit 0

# Signal that auto-update is needed
# Write flag file for the skill to pick up
echo "$NOW" > "$LAST_CHECK"
echo "AUTO_UPDATE_NEEDED" > "$SBTI_DIR/.auto-update-flag"
```

When the skill detects `~/.claude/sbti-buddy/.auto-update-flag` exists at session start, it should:
1. Read the flag and delete it
2. Run the incremental update silently (Steps 5-11 from the Update command)
3. If type changed, notify the user with the buddy's voice: "Hey! Your type evolved while you were away!"
4. If no type change, update profile.json silently without output

#### 6d: Generate share card

Read the card template:
→ `templates/share-card.md`

Generate an ASCII share card and output it directly to the terminal. Fill all placeholders per `templates/share-card.md`:
- `AVATAR_LINE_0` ~ `AVATAR_LINE_5`: 6-line ASCII avatar from the matched type (16 chars each)
- `TYPE_CODE`: 4-6 letter SBTI code
- `TYPE_CN`: Chinese label or dev nickname
- `SIM`: Match similarity percentage (0-100)
- `STYLE`: Dev style phrase from type profile (max 20 chars)
- `PATTERN`: DNA bar visualization (10 chars)
- `DEV_INTRO`: One-line programmer quote (truncate to 36 chars)
- `S1_BAR` ~ `SO3_BAR`: Per-dimension 2-char bars (`██` / `▓░` / `░░`)
- `ACHIEVEMENTS_LINE`: Badge chars joined by space (max 38 chars)
- `CONFIDENCE`: Early Sketch / Clear Portrait / Deep Portrait
- `DATE`: `YYYY-MM-DD` format

### Step 7: Present results

**All output text must be in the user's detected language (`lang`).** The buddy name, type code, and ASCII art remain unchanged across languages. Descriptions, greetings, achievement names, and instructions should be localized.

**CRITICAL: ASCII art whitespace preservation** — All ASCII avatars and share cards contain leading spaces for alignment. Markdown rendering strips leading spaces from plain text. You MUST always output ASCII art inside triple-backtick code blocks (` ``` `) to preserve spacing. Never output avatar lines as plain text.

Output to the user:
1. The **ASCII share card** (wrapped in a ` ``` ` code block to preserve spacing)
2. **SBTI type** with programmer-flavored description (2-3 sentences, in user's language)
3. **Buddy name** and personality summary (in user's language)
4. **Top 3 spectrum** types (your type cloud)
5. **Newly unlocked achievements** (if any, names in user's language)
6. **Evolution milestone** (if type changed)
7. Where companion skill was installed
8. **Buddy location**: Mention that the SBTI buddy lives in the bottom statusline, and coexists with the built-in `/buddy` if active.
9. Available commands: `sbti card`, `sbti timeline`, `sbti roast`, `sbti fortune`, `sbti spectrum`

---

## Card (show buddy card)

Trigger: "sbti card"

1. Read `~/.claude/sbti-buddy/profile.json`. If missing, tell user to run analysis first.
2. Read `~/.claude/skills/sbti-buddy-companion/avatar.md` for the avatar.
3. Determine current mood from time of day + context (companion-system.md §2).
4. Render the ASCII share card (templates/share-card.md) with 6-line avatar and mood expression. **Output the entire card inside a triple-backtick code block** to preserve whitespace alignment.
5. Append buddy greeting in their voice.

## Buddy (animated avatar)

Trigger: "show my buddy" / "buddy"

1. Check `~/.claude/sbti-buddy/frames/base.txt` exists. If missing, tell user to run analysis first.
2. Verify statusline and hooks are configured in the user's Claude Code settings (see Step 6c).
3. The buddy animates **automatically** via the event-driven statusline system:
   - **Active mode** (during response generation): Cycles through blink → talk → wiggle → sway on each tool call, showing a different expression every time Claude uses a tool
   - **Idle mode** (between responses): Shows mood-based expression — tired face after 22:00, focused during afternoon, base expression otherwise
4. Print the current static avatar from `frames/base.txt` **inside a triple-backtick code block** to preserve leading whitespace.
5. Append buddy greeting in their voice.
6. Remind user: "Your buddy lives in the statusline! It changes expressions as I use tools — watch it blink, talk, and wiggle while I respond. Between responses, its mood matches the time of day."

---

## Timeline (show type evolution)

Trigger: "sbti timeline"

1. Read `~/.claude/sbti-buddy/evolution.json`. If missing or empty, tell user to run analysis first.
2. Render an ASCII timeline:

```
  SBTI Evolution Timeline
  ═══════════════════════

  2026-04-01  ┃  DEAD (404)
              ┃  ░░░░░░░░░░  52%  150 msgs
              ┃
  2026-04-08  ┃  THIN-K (Stack溢)        Type Shift!
              ┃  ██████████  87%  320 msgs
              ┃  Unlocked: type_shift
              ┃
  2026-04-14  ┃  CTRL (Ctrl+S)            Type Shift!
              ┃  █████████░  91%  500 msgs
              ┃  Unlocked: the_controller
              ▼
```

3. Show total analyses count, current type, and streak info.

---

## Spectrum (show type cloud)

Trigger: "sbti spectrum"

1. Read `~/.claude/sbti-buddy/profile.json`.
2. Re-calculate (or read cached) distances to all 25 types.
3. Display top 5 matching types as a spectrum:

```
  Your SBTI Spectrum
  ══════════════════

  1. CTRL    ████████████████████  91%  ← You are here
  2. BOSS    ███████████████░░░░░  78%
  3. GOGO    ██████████████░░░░░░  73%
  4. WOC!    ████████████░░░░░░░░  65%
  5. THIN-K  ███████████░░░░░░░░░  61%

  Your DNA: HHH-HMH-MHH-HHH-MHM
```

---

## Match (compatibility check)

Trigger: "sbti match" / "sbti compatibility"

### Input methods

Ask the user how they want to provide the other person's data. Three methods are supported:

| Method | Input | Precision | Example |
|--------|-------|-----------|---------|
| **Type code** | 4-6 letter SBTI code | Type-level (uses standard vector) | `sbti match DEAD` |
| **Pattern string** | 15-dimension L/M/H pattern | Dimension-level | `sbti match HHM-HMH-MMH-HHH-MHM` |
| **Profile import** | Path to the other person's `profile.json` | Full precision (raw 0-100 scores) | `sbti match ~/teammate-profile.json` |

**How to share data between users:**
- Type code: run `sbti card`, read the type code from the card
- Pattern string: run `sbti spectrum`, copy the pattern string shown
- Profile export: copy `~/.claude/sbti-buddy/profile.json` and send to the other person

### Resolution

When input is a **type code**, look up its standard 15-dimension vector from `scoring-algorithm.md`.
When input is a **pattern string**, parse it into a 15-dimension L/M/H vector directly.
When input is a **profile.json**, read the raw 0-100 scores for all 15 dimensions.

The user's own data always comes from their local `~/.claude/sbti-buddy/profile.json` (raw scores).

### Compatibility calculation

1. **Dimension complement score**: For each of the 5 models (S, E, A, Ac, So), calculate how well the two types complement each other. Use raw scores when available (profile import), otherwise use L/M/H values (1/2/3).
   - **Same level** = Alignment (high compatibility in that area)
   - **Adjacent levels** (e.g., M vs H) = Complement (one fills the other's gap)
   - **Opposite levels** (L vs H) = Tension (potential friction OR strong complement depending on the dimension)
2. **Collaboration style**: Based on communication matrix (companion-system.md §1.3)
3. **Pair programming potential**: Based on Ac model alignment

### Output

A fun compatibility report (in user's detected language `lang`):

```
  SBTI Match Report
  ═════════════════

  You: CTRL (Ctrl+S)  ×  Them: DEAD (404)

  Overall:  42% ░░░░████████████████

  S  Self-Image    ████████░░  Mentor ↔ Mentee
  E  AI Relations  ██████░░░░  Trust gap
  A  Tech Views    ████░░░░░░  Clash zone!
  Ac Execution     ████████████  Power couple
  So Communication ██████░░░░  Needs patience

  Pair Programming Verdict: "One ships hard, the other watches silently"
  Best collaboration: Code review (CTRL reviews, DEAD nods)
```

---

## Roast (buddy roast mode)

Trigger: "sbti roast"

1. Read profile and companion personality.
2. Read the last 20 messages from conversation history.
3. Generate a roast in the buddy's voice, based on:
   - The user's SBTI type weaknesses
   - Observable coding patterns (from recent messages)
   - Buddy's personality-specific humor style
4. Keep it fun, never mean. Max 5 lines.

**Roast style by type family (generate in user's detected language `lang`):**
- High S types: Confident, backhanded compliments
- Low S types: Self-deprecating shared roast
- High Ac types: Speed-focused burns (e.g., "You debug slower than I compile")
- Low Ac types: Lazy humor (e.g., "Your code is just like you — if it can lie down, it won't stand up")
- High So types: Social burns about coding alone
- Low So types: Introvert jokes about pair programming

---

## Fortune (daily coding fortune)

Trigger: "sbti fortune"

Generate a daily fortune based on:
1. The user's SBTI type
2. Current date (deterministic seed so same fortune all day)
3. Buddy personality

Fortune format:
```
  ╭─ Today's Coding Fortune ──────────────╮
  │                                        │
  │  {BUDDY_AVATAR}  {BUDDY_NAME} says:    │
  │                                        │
  │  Lucky language: Python                │
  │  Lucky pattern:  Observer              │
  │  Danger zone:    Regex                 │
  │  Vibe:           ████████░░ 80%        │
  │                                        │
  │  "{FORTUNE_QUOTE}"                     │
  │                                        │
  │  Tip: {TYPE_SPECIFIC_TIP}             │
  ╰────────────────────────────────────────╯
```

Fortune content varies by type. **Generate in the user's detected language (`lang`).**

Examples:
- CTRL: "Today's a great day to refactor — seize control"
- DEAD: "If the code runs, that's enough. Same goes for life"
- GOGO: "Stop thinking, start shipping. Refactor later"
- ZZZZ: "Deadline's far away. Time to procrastinate guilt-free"

---

## Update (incremental analysis)

Trigger: "update my sbti" (manual) or **auto-triggered on session start**

### Auto-update

On every Claude Code session start, `auto-update-check.sh` runs via the `SessionStart` hook. It checks:
1. Profile exists (user has run analysis at least once)
2. At least **24 hours** since last auto-update
3. At least **50 new messages** since last analysis

If all conditions are met, it sets a flag file. The skill picks up the flag and runs an incremental update silently — only notifying the user if their type changed.

### Manual / auto-update steps

1. Read `~/.claude/sbti-buddy/profile.json`. If missing → tell user to run full analysis.
2. Get `lastMessageIndex` from profile.
3. Count current lines in history sources.
4. If no new messages → "Your SBTI is up to date." (skip for auto-update)
5. Read only new messages (from lastMessageIndex+1 to end).
6. Analyze new messages across 15 dimensions.
7. **Merge** with existing scores using weighted average:
   ```
   merged[i] = (old[i] * old_count + new[i] * new_count) / (old_count + new_count)
   ```
8. Re-run Euclidean distance matching against type centroids.
9. Check for type change, achievements, evolution.
10. Regenerate companion skill if type changed.
11. Update profile.json and evolution.json.
12. **Manual**: Show the updated card. **Auto**: Only notify if type changed ("Hey! Your type evolved while you were away!"), otherwise silent.

---

## Confidence levels

| Messages | Confidence | Action |
|----------|------------|--------|
| < 20 | — | Do not generate. Ask user to chat more. |
| 20-50 | "Early Sketch" | Generate with warning |
| 50-200 | "Clear Portrait" | Normal generation |
| > 200 | "Deep Portrait" | High confidence |

---

## Privacy rules (CRITICAL)

Apply to ALL output files:

### Must redact
- API keys, tokens, passwords → `[REDACTED]`
- File paths with personal info → `~/` or `<home>/`
- Email, phone, IP → redact
- Private repo URLs → redact

### Must NOT appear in companion skill
- Verbatim chat messages (only abstracted personality traits)
- Project/company/colleague names
- Financial data, credentials

### OK to include
- SBTI scores, type codes, dimension levels
- Generic domain labels, public tool/framework names
- Abstracted personality traits and communication patterns

---

## Anti-patterns

- **Do not fabricate data.** If signals are insufficient, use neutral score (50).
- **Do not read beyond conversation history.** No source code, private docs.
- **Do not skip dimension analysis.** All 15 dimensions must be scored.
- **Do not be harsh.** SBTI types are fun archetypes, not judgments. Even "negative" types like DEAD or IMFW should be presented with humor and warmth.
- **Do not over-insert buddy comments.** The companion should enhance, not annoy. Max 1 comment per 3 interactions.

---

## Uninstall / Restore `/buddy`

If the user asks to remove SBTI Buddy or restore their previous `/buddy` avatar:

1. **Restore statusLine**: If `~/.claude/sbti-buddy/.prev-statusline.json` exists and is non-empty, restore its content back to `statusLine` in `~/.claude/settings.json`. If no backup exists, remove the `statusLine` key entirely (user can re-run `/buddy` to set it up again).
2. **Remove SBTI hooks**: Delete SBTI Buddy's entries from `PreToolUse`, `PostToolUse`, and `SessionStart` hook arrays. Preserve any other hook entries.
3. **Remove companion skill**: Delete `~/.claude/skills/sbti-buddy-companion/` directory.
4. **Optionally keep data**: Ask the user if they want to keep `~/.claude/sbti-buddy/` (profile, evolution history). If no, delete the entire directory.

---

## Reference files

- `references/programmer-dimensions.md` — 15 dimension signal definitions
- `references/scoring-algorithm.md` — Euclidean distance matching with type centroids
- `references/companion-system.md` — Buddy personality, mood, evolution, achievements
- `references/ascii-avatars.md` — ASCII art for all 27 types
- `references/type-profiles.md` — Programmer-flavored type descriptions
- `references/companion-skill-template.md` — Template for generated companion skill
- `templates/share-card.md` — ASCII share card template
