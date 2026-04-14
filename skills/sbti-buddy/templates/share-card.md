# SBTI Buddy Share Card Template

Avatar uses a 16-char wide × 6-line tall matrix. Card width is 44 characters to accommodate the full avatar.

## Template

```
╭──────────────────────────────────────────╮
│  ✦ SBTI BUDDY CARD                      │
│  ══════════════════                      │
│                                          │
│  {{AVATAR_LINE_0}}    {{TYPE_CODE}}      │
│  {{AVATAR_LINE_1}}    ({{TYPE_CN}})      │
│  {{AVATAR_LINE_2}}                       │
│  {{AVATAR_LINE_3}}    Match: {{SIM}}%    │
│  {{AVATAR_LINE_4}}    Style: {{STYLE}}   │
│  {{AVATAR_LINE_5}}    DNA: {{PATTERN}}   │
│                                          │
│  "{{DEV_INTRO}}"                         │
│                                          │
│  ─── Dimensions ─────────────────────    │
│  S  {{S1_BAR}} {{S2_BAR}} {{S3_BAR}}    │
│  E  {{E1_BAR}} {{E2_BAR}} {{E3_BAR}}    │
│  A  {{A1_BAR}} {{A2_BAR}} {{A3_BAR}}    │
│  Ac {{AC1_BAR}} {{AC2_BAR}} {{AC3_BAR}}  │
│  So {{SO1_BAR}} {{SO2_BAR}} {{SO3_BAR}}  │
│                                          │
│  {{ACHIEVEMENTS_LINE}}                   │
│                                          │
│  Confidence: {{CONFIDENCE}}              │
│  Generated:  {{DATE}}                    │
╰──────────────────────────────────────────╯
```

## Placeholder Reference

| Placeholder | Source / How to fill |
|-------------|---------------------|
| `AVATAR_LINE_0` ~ `AVATAR_LINE_5` | 6-line ASCII avatar from `ascii-avatars.md`, 16 chars each |
| `TYPE_CODE` | 4-6 letter SBTI code, e.g. `CTRL` |
| `TYPE_CN` | Chinese label or dev nickname |
| `SIM` | Similarity percentage, integer 0-100 |
| `STYLE` | Dev style phrase from `type-profiles.md` (max 20 ch) |
| `PATTERN` | DNA bar visualization (10 ch, see DNA rules) |
| `DEV_INTRO` | One-line programmer quote (truncate to 36 ch) |
| `S1-3, E1-3, ...` | Per-dimension 2-char bars (see DNA rules) |
| `ACHIEVEMENTS_LINE` | Badge chars joined by space (max 38 ch) |
| `CONFIDENCE` | Early Sketch / Clear Portrait / Deep Portrait |
| `DATE` | `YYYY-MM-DD` format |

## DNA Bar Rendering

Each sub-dimension score maps to a 2-character block:

| Level | Score range | Bar |
|-------|-----------|------|
| H | >= 67 | `██` |
| M | 34 - 66 | `▓░` |
| L | < 34 | `░░` |

Build `PATTERN` by concatenating the 5 dimension bars (S, E, A, Ac, So)
using each dimension's **average** sub-score. Example: `██▓░░░██▓░`

## Avatar Rendering

Place the 6-line ASCII avatar on the left side of the card, with type info
on the right. Each avatar line is exactly 16 characters. The card layout
uses the avatar area (columns 4-19) and the info area (columns 24-40).

## Achievements Line

Render earned badges as single characters separated by spaces.
Unlocked: `★`, Locked: `☆`. Truncate to fit 38 chars.
Example: `★ ★ ★ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆ ☆`

## Example (filled)

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
