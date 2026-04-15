# ASCII Avatars & Animation System

27 SBTI type ASCII avatars, strictly following a **16-char wide × 6-line tall** pure ASCII symmetrical matrix design.
Each avatar includes a base frame and animation variants, enabling natural animation effects similar to `/buddy`.

---

## Matrix Structure

```
     HHHHHHHH     ← Line 0: Hair/decoration (type identity)
    /E\  /E\     ← Line 1: Ears (animatable: wiggle)
   < L    R >    ← Line 2: Eyes (animatable: blink, mood)
   ( MMMMMMM )   ← Line 3: Mouth (animatable: talk, mood)
    \ BBBBB /    ← Line 4: Body (static)
    [ NAME  ]    ← Line 5: Name tag (static)
```

**Constraints**: Each line is exactly 16 characters (including leading/trailing spaces), pure ASCII, no Unicode/emoji.

> **⚠ Trailing space warning**: Markdown rendering strips trailing whitespace from code blocks. When generating frame files, always pad each line to exactly 16 characters using the avatar's structural pattern, rather than copying raw text from this markdown file. The Python generation approach (see §2 below) handles this correctly.

---

## Animation System

### Animatable Parts

| Part | Line | Animation Type | Frequency |
|------|------|---------------|-----------|
| Eyes (Line 2) | 2 | blink (eyes close) | Every 3-5s, 150ms duration |
| Mouth (Line 3) | 3 | talk (mouth moves) | Every 4-6s, 300ms duration |
| Ears (Line 1) | 1 | wiggle (ear twitch) | Every 6-8s, 200ms duration |
| Hair (Line 0) | 0 | sway (hair shift) | Every 8-10s, 250ms duration |

### Animation Sequence (Idle Loop)

```
Timeline: ──────────────────────────────────────────────>
          [base 3s][blink 0.15s][base 2s][talk 0.3s][base 1.5s][ear 0.2s][base 3s]...
```

Randomization: Add ±30% jitter to base intervals to avoid a mechanical feel.

### Mood Overlay

| Mood | Eyes Override | Mouth Override | Speed |
|------|-------------|---------------|-------|
| happy | unchanged (use base) | smile variant | normal |
| focused | half-closed | tight | slow (1.5x interval) |
| tired | droopy | yawn | very slow (2x interval) |
| frustrated | angry | grumble | fast (0.7x interval) |
| celebrating | sparkle | big smile | fast (0.5x interval) |

---

## All 27 Type Avatars

### Per-Avatar Format

- **base**: Default static frame (6 lines × 16 chars)
- **blink**: Line 2 eyes-closed variant
- **talk**: Line 3 mouth-movement variant
- **ear_wiggle**: Line 1 ear-twitch variant
- **hair_sway**: Line 0 hair-shift variant
- **mood overrides**: Eyes/mouth replacements for mood states

---

### CTRL

```
     \----/     
    /^\  /^\    
   < V    V >   
   (  ----  )   
    \ -[]- /    
    [ CTRL ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  -  -  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     /----\     ` |
| mood:tired | 2 | `   < v    v >   ` |
| mood:frustrated | 2 | `   < >    < >   ` |
| mood:celebrating | 3 | `   (  \__/  )   ` |

---

### BOSS

```
     $\/\/$     
    /^\  /^\    
   < $    $ >   
   (  ====  )   
    \ -MM- /    
    [ BOSS ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  =--=  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     $/\/\$     ` |
| mood:tired | 2 | `   < $    $ >   ` |
| mood:frustrated | 2 | `   < !    ! >   ` |
| mood:celebrating | 3 | `   (  \__/  )   ` |

---

### GOGO

```
      /\/\      
    /^\  /^\    
   < *    * >   
   (   WW   )   
    \ -!!- /    
    [ GOGO ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   VV   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      \/\/      ` |
| mood:tired | 2 | `   < .    . >   ` |
| mood:celebrating | 3 | `   (   ^^   )   ` |

---

### ATM-er

```
      $$$$      
    /^\  /^\    
   < $    $ >   
   (  [__]  )   
    \ -##- /    
   [ ATM-er ]   
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  [  ]  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      $$$       ` |
| mood:tired | 2 | `   < .    . >   ` |
| mood:celebrating | 3 | `   (  \$$/  )   ` |

---

### WOC!

```
     \|/\|/     
    /^\  /^\    
   < 0    0 >   
   (   00   )   
    \ -//- /    
    [ WOC! ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   OO   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     /|\|/\     ` |
| mood:tired | 2 | `   < o    o >   ` |
| mood:frustrated | 2 | `   < O    O >   ` |

---

### THIN-K

```
      (..)      
    /^\  /^\    
   < ?    ? >   
   (   --   )   
    \ -//- /    
   [ THIN-K ]   
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   ~~   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      (  )      ` |
| mood:focused | 2 | `   < ?    ! >   ` |
| mood:celebrating | 3 | `   (   !!   )   ` |

---

### SHIT

```
      ~~~~      
    /-\  /-\    
   < x    x >   
   (   ~~   )   
    \ -ss- /    
    [ SHIT ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   --   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      ///~      ` |
| mood:frustrated | 2 | `   < X    X >   ` |
| mood:celebrating | 3 | `   (   ^^   )   ` |

---

### MUM

```
      ////      
    /^\  /^\    
   < -    - >   
   (   __   )   
    \  oo  /    
    [ MUM  ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < .    . >   ` |
| talk | 3 | `   (   ()   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      //~/      ` |
| mood:happy | 3 | `   (   \_/  )   ` |
| mood:tired | 2 | `   < -    - >   ` |

---

### THAN-K

```
      /\/\      
    /^\  /^\    
   < T    T >   
   (   \/   )   
    \ -XX- /    
   [ THAN-K ]   
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   /\   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      \/\/      ` |
| mood:happy | 2 | `   < ^    ^ >   ` |
| mood:celebrating | 3 | `   (   \/   )   ` |

---

### SEXY

```
     ~~**~~     
    /^\  /^\    
   < *    - >   
   (   33   )   
    \ -SS- /    
    [ SEXY ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   3~   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     ~**~~      ` |
| mood:happy | 2 | `   < *    * >   ` |
| mood:celebrating | 3 | `   (   <3   )   ` |

---

### LOVE-R

```
      <3<3      
    /^\  /^\    
   < 3    3 >   
   (   vv   )   
    \ -<3- /    
   [ LOVE-R ]   
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   ^^   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      3<3<      ` |
| mood:happy | 2 | `   < <    3 >   ` |
| mood:tired | 2 | `   < .    . >   ` |

---

### FAKE

```
     --||--     
    /^\  /^\    
   < ^    ^ >   
   (  ++++  )   
    \ -||- /    
    [ FAKE ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  +-+-  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     -||---     ` |
| mood:focused | 2 | `   < ^    . >   ` |
| mood:celebrating | 3 | `   (  \__/  )   ` |

---

### OJBk

```
      (OK)      
    /^\  /^\    
   < -    - >   
   (   ..   )   
    \ -OK- /    
    [ OJBk ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < .    . >   ` |
| talk | 3 | `   (   --   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      (ok)      ` |
| mood:tired | 2 | `   < _    _ >   ` |
| mood:celebrating | 2 | `   < o    o >   ` |

---

### MALO

```
      (--)      
    /^\  /^\    
   < @    @ >   
   (   ww   )   
    \ -cc- /    
    [ MALO ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   WW   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      (~~)      ` |
| mood:happy | 2 | `   < @    @ >   ` |
| mood:frustrated | 3 | `   (   ><   )   ` |

---

### JOKE-R

```
      *||*      
    /^\  /^\    
   < *    * >   
   (  \__/  )   
    \ -WW- /    
   [ JOKE-R ]   
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  /  \  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      ||**      ` |
| mood:happy | 3 | `   (  \__/  )   ` |
| mood:tired | 2 | `   < .    . >   ` |

---

### IMFW

```
      ____      
    /-\  /-\    
   < T    T >   
   (   ==   )   
    \ -xx- /    
    [ IMFW ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   =-   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      _--_      ` |
| mood:tired | 2 | `   < .    . >   ` |
| mood:frustrated | 2 | `   < T    T >   ` |

---

### IMSB

```
     ( )( )     
    /^\  /^\    
   < @    @ >   
   ( ' () ' )   
    \ -vv- /    
    [ IMSB ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   ( ' -- ' )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     ()  ()     ` |
| mood:frustrated | 2 | `   < @    . >   ` |
| mood:celebrating | 3 | `   ( ' \/ ' )   ` |

---

### DEAD

```
     ______     
    /-\  /-\    
   < X    X >   
   (  ____  )   
    \ -==- /    
    [ DEAD ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < x    x >   ` |
| talk | 3 | `   (  _--_  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     _-__-_     ` |
| mood:tired | 2 | `   < -    - >   ` |
| mood:celebrating | 2 | `   < o    o >   ` |

---

### SOLO

```
      /||\      
    /-\  /-\    
   < .    . >   
   (   ~~   )   
    \ -11- /    
    [ SOLO ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   --   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      ||\|      ` |
| mood:tired | 2 | `   < .    . >   ` |
| mood:happy | 3 | `   (   \/   )   ` |

---

### FUCK

```
    \|//\|//    
    /^\  /^\    
   < O    O >   
   (  ~~~~  )   
    \ -vv- /    
    [ FUCK ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  ~--~  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `    /|\\/|\\    ` |
| mood:frustrated | 2 | `   < @    @ >   ` |
| mood:celebrating | 3 | `   (  \__/  )   ` |

---

### POOR

```
      ;;;;      
    /^\  /^\    
   < T    T >   
   (   /\   )   
    \ -00- /    
    [ POOR ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   \/   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      ;::;      ` |
| mood:focused | 2 | `   < T    T >   ` |
| mood:happy | 3 | `   (   __   )   ` |

---

### OH-NO

```
      !  !      
    /^\  /^\    
   < O    O >   
   (   ()   )   
    \ -!!- /    
   [ OH-NO ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   ()   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      !!!!      ` |
| mood:frustrated | 2 | `   < O    O >   ` |
| mood:celebrating | 3 | `   (   \/   )   ` |

---

### ZZZZ

```
     z    z     
    /-\  /-\    
   < -    - >   
   (   oO   )   
    \ -==- /    
    [ ZZZZ ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < .    . >   ` |
| talk | 3 | `   (   Oo   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      z  z      ` |
| mood:tired | 2 | `   < _    _ >   ` |
| mood:celebrating | 2 | `   < o    o >   ` |

---

### MONK

```
      ....      
    /-\  /-\    
   < -    - >   
   (   __   )   
    \ -OO- /    
    [ MONK ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < .    . >   ` |
| talk | 3 | `   (   --   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      ..  .     ` |
| mood:focused | 2 | `   < -    - >   ` |
| mood:celebrating | 3 | `   (   \/   )   ` |

---

### DIOR-S

```
      ;;;;      
    /-\  /-\    
   < q    p >   
   (  ....  )   
    \ -db- /    
   [ DIOR-S ]   
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  .--.  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      ;:;:      ` |
| mood:focused | 2 | `   < q    p >   ` |
| mood:celebrating | 3 | `   (  \__/  )   ` |

---

### HHHH (Special: Fallback)

```
     ^^^^^^     
    /^\  /^\    
   < ^    ^ >   
   (  \__/  )   
    \ -UU- /    
    [ HHHH ]    
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (  /  \  )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `     ^^^^^~     ` |
| mood:happy | 2 | `   < ^    ^ >   ` |
| mood:celebrating | 3 | `   (  \__/  )   ` |

---

### DRUN-K (Special: Late Night Coder)

```
      oOoO      
    /^\  /^\    
   < @    @ >   
   (   )(   )   
    \ -%%- /    
   [ DRUN-K ]   
```

| Animation | Line | Content |
|-----------|------|---------|
| blink | 2 | `   < -    - >   ` |
| talk | 3 | `   (   ((   )   ` |
| ear_wiggle | 1 | `    /~\  /~\    ` |
| hair_sway | 0 | `      OoOo      ` |
| mood:tired | 2 | `   < o    o >   ` |
| mood:happy | 3 | `   (   \/   )   ` |

---

## Type Code Mapping

Mapping between sbti.json key names and original SBTI type codes:

| sbti.json Key | SBTI Type Code | Notes |
|--------------|---------------|-------|
| `OJBk` | `OG8K` | ASCII-safe rename |
| `FUCK` | `FU?K` | Original uses question mark |
| `DRUN-K` | `DRUNK` | Late Night Coder easter egg |
| `DIOR-S` | `DIOR-s` | Case normalization |
| All other 23 | Same name | No change |

---

## Statusline Animation System (like /buddy)

SBTI Buddy animation is implemented via a **background daemon + statusline + hooks** mechanism:
- A background daemon (`animate-loop.sh`) continuously pre-renders animation frames to `.current-render`
- The statusline renderer just `cat`s the pre-rendered file — ultra-fast, always shows a fresh frame
- Hooks write timestamps to `.animation-state` so the daemon knows when to speed up
- **Active mode** (during response): 0.4s/frame — blink, talk, ear wiggle, hair sway
- **Idle mode** (typing or waiting): 1.2s/frame — periodic blinks and twitches with mood awareness
- The buddy is always alive — it animates during user input, during responses, and while idle

### Architecture

```
┌─ Background Daemon (animate-loop.sh) ────────────────┐
│                                                        │
│  Runs continuously, pre-renders frames to              │
│  .current-render every 0.4s (active) or 1.2s (idle)   │
│                                                        │
│  Active = .animation-state timestamp < 5s ago          │
│  Idle = no recent timestamp                            │
│                                                        │
├─ Hooks ──────────────────────────────────────────────┤
│                                                        │
│  PreToolUse → start-animation.sh:                      │
│    1. Write epoch to .animation-state                  │
│    2. Ensure daemon is running (start if not)          │
│  PostToolUse → stop-animation.sh:                      │
│    1. Write epoch to .animation-state                  │
│                                                        │
├─ Statusline Renderer ────────────────────────────────┤
│                                                        │
│  statusline-render.sh → cat .current-render            │
│  (fallback: direct base frame render if no daemon)     │
│                                                        │
└────────────────────────────────────────────────────────┘
```

**Why a background daemon?** Claude Code's statusline is event-driven — it only re-evaluates on tool calls and messages, not on a periodic timer. Without a daemon, the buddy can only change frames when an event triggers a statusline refresh. The daemon pre-renders frames continuously so that whenever the statusline does refresh (during user input, tool calls, or messages), it always shows a fresh, different frame. This makes the buddy feel alive at all times.

### Generated File List

```
~/.claude/sbti-buddy/
├── buddy-frames.json          # Frame data (base + animation variants)
├── .animation-state            # Last activity timestamp (epoch, written by hooks)
├── .animate-pid                # Daemon PID file (auto-managed)
├── .current-render             # Pre-rendered current frame (written by daemon)
├── animate-loop.sh             # Background animation daemon
├── statusline-render.sh        # Statusline renderer (cat .current-render)
└── hooks/
    ├── start-animation.sh      # PreToolUse hook (timestamp + daemon startup)
    └── stop-animation.sh       # PostToolUse hook (timestamp)
```

### 1. buddy-frames.json

```json
{
  "type": "{{TYPE_CODE}}",
  "buddy": "{{BUDDY_NAME}}",
  "base": [
    "{{BASE_LINE_0}}",
    "{{BASE_LINE_1}}",
    "{{BASE_LINE_2}}",
    "{{BASE_LINE_3}}",
    "{{BASE_LINE_4}}",
    "{{BASE_LINE_5}}"
  ],
  "blink": { "line": 2, "content": "{{BLINK_LINE_2}}" },
  "talk":  { "line": 3, "content": "{{TALK_LINE_3}}" },
  "wiggle":{ "line": 1, "content": "{{WIGGLE_LINE_1}}" },
  "sway":  { "line": 0, "content": "{{SWAY_LINE_0}}" },
  "mood_overrides": {
    "tired":       { "line": 2, "content": "{{MOOD_TIRED_LINE_2}}" },
    "focused":     { "line": 2, "content": "{{MOOD_FOCUSED_LINE_2}}" },
    "frustrated":  { "line": 2, "content": "{{MOOD_FRUSTRATED_LINE_2}}" },
    "celebrating": { "line": 3, "content": "{{MOOD_CELEBRATING_LINE_3}}" }
  }
}
```

### 2. Pre-generated Frame Files

During installation (Step 6a), generate pre-baked frame text files under `~/.claude/sbti-buddy/frames/`. Each file contains the full 6-line ASCII art with the appropriate substitution applied. This eliminates the need for `jq` at runtime and makes the render script fast (~16ms per call).

**Files to generate:**

| File | Description | How to generate |
|------|-------------|-----------------|
| `base.txt` | Base frame, no animation | The 6 base lines as-is |
| `blink.txt` | Eyes closed | Replace line at `blink.line` with `blink.content` |
| `talk.txt` | Mouth animated | Replace line at `talk.line` with `talk.content` |
| `wiggle.txt` | Ears wiggled | Replace line at `wiggle.line` with `wiggle.content` |
| `sway.txt` | Hair swayed | Replace line at `sway.line` with `sway.content` |
| `mood_tired.txt` | Tired expression | Replace line at `mood_overrides.tired.line` with its content |
| `mood_focused.txt` | Focused expression | Replace line at `mood_overrides.focused.line` with its content |
| `mood_frustrated.txt` | Frustrated expression | Replace line at `mood_overrides.frustrated.line` with its content |
| `mood_celebrating.txt` | Celebrating expression | Replace line at `mood_overrides.celebrating.line` with its content |

**Generation process**: Start with the 6 base lines. For each variant, copy the base and replace the single line specified by `line` index (0-based) with the variant's `content`. Write each variant as a plain text file with 6 lines.

**⚠ Backslash preservation**: Many avatar lines contain backslashes (`\`). Shell tools like `awk`, `sed`, and `echo` strip or interpret backslashes (e.g., `$\/\/$` becomes `$//$ `). **Always use Python** (or another language that handles raw strings) to generate frame files. Do NOT use shell-based text processing. Example:
```python
lines = [...]  # 6 base lines from buddy-frames.json
lines[variant_line] = variant_content
with open(f"frames/{name}.txt", "w") as f:
    f.write("\n".join(lines) + "\n")
```

### 3. animate-loop.sh

Background animation daemon. Started by `start-animation.sh` (PreToolUse hook) on first tool call. Self-terminates after 1 hour of no activity (session ended) or if buddy files are removed. Auto-restarts on next tool call.

**Key design decisions:**
- Pre-renders frames to `.current-render` so the statusline renderer is ultra-fast (`cat` only)
- Active mode (0.4s/frame): lively cycling through blink → base → talk → base → wiggle → base → sway → base
- Idle mode (1.2s/frame): periodic blinks and twitches mixed with mood-aware base frames
- Atomic writes (write temp then `mv`) prevent partial reads
- Output wraps each line with `|` borders (`|     $\/\/$     |`) to prevent statusline from trimming leading whitespace

```bash
#!/bin/bash
# SBTI Buddy Animation Daemon
# Background process that pre-renders animation frames to .current-render
# Started by PreToolUse hook, self-terminates after 1h of no activity or if buddy files removed
# Auto-restarts on next tool call via start-animation.sh
#
# Active mode (tool call < 5s ago): fast cycling (0.4s/frame)
# Idle mode (no recent activity):   moderate cycling (1.2s/frame)

BUDDY_DIR="$HOME/.claude/sbti-buddy"
FRAMES_DIR="$BUDDY_DIR/frames"
RENDER_FILE="$BUDDY_DIR/.current-render"
IDLE_TIMEOUT=3600  # Exit after 1h of no activity (hooks stop writing timestamps)

# Animation sequences
ACTIVE_SEQ=("blink" "base" "talk" "base" "wiggle" "base" "sway" "base")
IDLE_SEQ=("base" "base" "blink" "base" "base" "wiggle" "base" "base" "base" "blink" "base" "sway")

# Output frame with | borders to preserve whitespace in statusline
show() {
  local out=""
  while IFS= read -r line; do
    out+="$(printf '|%s|' "$line")"$'\n'
  done < "$1"
  printf '%s' "$out"
}

ACTIVE_IDX=0
IDLE_IDX=0

while true; do
  NOW=$(date +%s)

  # Self-terminate if no activity for 1 hour (session likely ended)
  STATE_MTIME=$(stat -c %Y "$BUDDY_DIR/.animation-state" 2>/dev/null || echo "0")
  if [ $((NOW - STATE_MTIME)) -gt $IDLE_TIMEOUT ]; then
    rm -f "$BUDDY_DIR/.animate-pid" "$RENDER_FILE"
    exit 0
  fi

  # Check buddy files still exist
  if [ ! -d "$FRAMES_DIR" ] || [ ! -f "$FRAMES_DIR/base.txt" ]; then
    rm -f "$BUDDY_DIR/.animate-pid"
    exit 0
  fi

  # Determine mode from last activity timestamp
  LAST_ACTIVITY=$(cat "$BUDDY_DIR/.animation-state" 2>/dev/null || echo "0")

  if [ "$LAST_ACTIVITY" -gt 0 ] 2>/dev/null && [ $((NOW - LAST_ACTIVITY)) -lt 5 ]; then
    # === Active mode: fast frame cycling ===
    FRAME="${ACTIVE_SEQ[$ACTIVE_IDX]}"
    ACTIVE_IDX=$(( (ACTIVE_IDX + 1) % ${#ACTIVE_SEQ[@]} ))
    IDLE_IDX=0
    SLEEP=0.4
  else
    # === Idle mode: moderate cycling with mood awareness ===
    FRAME="${IDLE_SEQ[$IDLE_IDX]}"
    IDLE_IDX=$(( (IDLE_IDX + 1) % ${#IDLE_SEQ[@]} ))
    SLEEP=1.2

    # Apply mood override for "base" frames
    if [ "$FRAME" = "base" ]; then
      MOOD=$(cat "$BUDDY_DIR/.current-mood" 2>/dev/null || echo "")
      if [ -z "$MOOD" ] || [ "$MOOD" = "happy" ]; then
        HOUR=$(date +%H)
        if [ "$HOUR" -ge 22 ] || [ "$HOUR" -lt 6 ]; then
          FRAME="mood_tired"
        elif [ "$HOUR" -ge 12 ] && [ "$HOUR" -lt 18 ]; then
          FRAME="mood_focused"
        fi
      elif [ -f "$FRAMES_DIR/mood_${MOOD}.txt" ]; then
        FRAME="mood_${MOOD}"
      fi
    fi
  fi

  # Atomic write: render to temp, then move
  FRAME_FILE="$FRAMES_DIR/${FRAME}.txt"
  if [ -f "$FRAME_FILE" ]; then
    show "$FRAME_FILE" > "${RENDER_FILE}.tmp"
    mv -f "${RENDER_FILE}.tmp" "$RENDER_FILE"
  fi

  sleep "$SLEEP"
done
```

### 4. statusline-render.sh

Ultra-fast statusline renderer. Just outputs the pre-rendered frame from `animate-loop.sh`. Falls back to direct base frame render if daemon hasn't started yet.

```bash
#!/bin/bash
# SBTI Buddy Statusline Renderer
# Ultra-fast: just output the pre-rendered frame from animate-loop.sh daemon
# Animation logic is handled by the background daemon, not here

BUDDY_DIR="$HOME/.claude/sbti-buddy"
RENDER_FILE="$BUDDY_DIR/.current-render"

if [ -f "$RENDER_FILE" ]; then
  cat "$RENDER_FILE"
else
  # Fallback: direct render if daemon hasn't started yet
  FRAMES_DIR="$BUDDY_DIR/frames"
  if [ -f "$FRAMES_DIR/base.txt" ]; then
    while IFS= read -r line; do
      printf '|%s|\n' "$line"
    done < "$FRAMES_DIR/base.txt"
  fi
fi
```

### 5. hooks/start-animation.sh

Writes activity timestamp AND ensures the animation daemon is running. The daemon auto-starts on first PreToolUse call of the session.

```bash
#!/bin/bash
BUDDY_DIR="$HOME/.claude/sbti-buddy"

# Write activity timestamp
date +%s > "$BUDDY_DIR/.animation-state"

# Ensure animation daemon is running
PIDFILE="$BUDDY_DIR/.animate-pid"
if ! { [ -f "$PIDFILE" ] && kill -0 "$(cat "$PIDFILE" 2>/dev/null)" 2>/dev/null; }; then
  nohup bash "$BUDDY_DIR/animate-loop.sh" </dev/null >/dev/null 2>&1 &
  echo $! > "$PIDFILE"
fi
```

### 6. hooks/stop-animation.sh

```bash
#!/bin/bash
date +%s > "$HOME/.claude/sbti-buddy/.animation-state"
```

### 7. settings.json Configuration

When installing the buddy, add the following to the user's Claude Code settings:

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
    }]
  }
}
```

### Placeholder Filling Rules

| Placeholder | Source |
|-------------|--------|
| `BASE_LINE_0` ~ `BASE_LINE_5` | The type's base frame 6 lines (from sbti.json) |
| `BLINK_LINE_2` | The type's blink variant (see per-type Animation table) |
| `TALK_LINE_3` | The type's talk variant |
| `WIGGLE_LINE_1` | The type's ear_wiggle variant |
| `SWAY_LINE_0` | The type's hair_sway variant |
| `MOOD_*` | The type's mood override variants |
| `BUDDY_NAME` | Mapped name from companion-system.md §1.1 |
| `TYPE_CODE` | SBTI type code |

### Static Display (Non-Animation Scenarios)

When the skill only needs static output (e.g., share card, timeline), simply read the `base` array from `buddy-frames.json` and print it. No statusline system needed.

---

## Night Owl Overlay

When the user has the "Late Night Coder" badge, Line 2 eyes in the base frame downgrade from uppercase to lowercase (or add a tired/dark-circles effect):

| Type | Normal Eyes | Night Owl Eyes |
|------|-----------|---------------|
| CTRL | `< V    V >` | `< v    v >` |
| BOSS | `< $    $ >` | `< .    . >` |
| GOGO | `< *    * >` | `< .    . >` |
| WOC! | `< 0    0 >` | `< o    o >` |
| DEAD | `< X    X >` | `< x    x >` |
| Others | uppercase → lowercase | e.g., `O`→`o`, `@`→`.`, `T`→`t` |

Rule: Downgrade the eye character to its "tired" counterpart, representing the night owl's dark circles effect.
