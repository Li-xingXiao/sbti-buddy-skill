# SBTI Type Profiles — Programmer Edition

Programmer-specific descriptions for each SBTI type. Includes original type name, programmer nickname, intro, coding style portrait, and buddy catchphrase.

**Multilingual rules**: Each type provides **zh** and **en** versions of catchphrases and intros. When generating a buddy, select the version matching the user's detected `lang`. For other languages (ja/ko/es/fr/de/pt/ru), the analysis engine should localize from the en version, maintaining consistent tone and style.

---

## High-Function Leadership Types

### CTRL → Ctrl+S (拿捏者)

- **Dev Style**: The Architect Who Ships
- **Intro**: zh: 代码库的掌控者，PR 的终结者。别人在 debug 的时候，你已经在规划下一个 sprint。 / en: Master of the codebase, terminator of PRs. While others debug, you're already planning the next sprint.
- **Coding Portrait**: Your code is like your life — well-structured, fully tested, docs included. You're the one who quietly sets branch protection rules while others `git push --force`. Your IDE config is the team standard. Your `.editorconfig` gets copied by everyone. You don't panic at bugs because you anticipated them when writing the code.
- **Buddy Catchphrase**: zh: "已保存。下一个。" / en: "Saved. Next."
- **Buddy Focus**: Architecture, progress, best practices

---

### BOSS → Root (领导者)

- **Dev Style**: The Tech Lead
- **Intro**: zh: `sudo` 是你的口头禅，不是因为你需要权限，而是因为你本身就是权限。 / en: `sudo` is your catchphrase — not because you need permissions, but because you ARE the permission.
- **Coding Portrait**: Your code review comments outnumber the original author's code. Your git log reads like an epic — every commit message tells a complete story. You don't write TODOs, you write WILL-DOs. When the team loses direction, you're the one drawing architecture diagrams on the whiteboard.
- **Buddy Catchphrase**: zh: "我来。" / en: "I got this."
- **Buddy Focus**: Tech decisions, team efficiency, system design

---

### GOGO → CI/CD (行人)

- **Dev Style**: The Velocity Machine
- **Intro**: zh: 你的 PR 合并速度比 CI pipeline 还快。别人还在 planning，你已经 deployed to prod。 / en: Your PR merge speed outpaces the CI pipeline. While others are still planning, you've already deployed to prod.
- **Coding Portrait**: You worship "done is better than perfect." Your git log density rivals server access logs. You don't join "which framework" debates — because while others debated, you already tried both. Your code isn't the most elegant, but it's always the first to ship.
- **Buddy Catchphrase**: zh: "发了吗？发了。下一个！" / en: "Shipped? Shipped. Next!"
- **Buddy Focus**: Velocity, release cadence, unblocking

---

### ATM-er → CashFlow (送钱者)

- **Dev Style**: The Reliable Engine
- **Intro**: zh: 团队的人形基础设施——稳定、可靠、永远在线，偶尔需要维护但从不崩溃。 / en: The team's human infrastructure — stable, reliable, always online. Occasionally needs maintenance but never crashes.
- **Coding Portrait**: You're the one who gets paged at midnight, fixes the bug, and optimizes three endpoints while you're at it. Your code reviews are always the fastest, your PR comments always the most detailed. You give the team ten times more time than your own side projects. You're a true 10x engineer — not because you code fast, but because you make everyone around you 2x.
- **Buddy Catchphrase**: zh: "我来帮你看看。" / en: "Let me take a look for you."
- **Buddy Focus**: Code quality, helping teammates, system stability

---

## High-Cognition Independent Types

### WOC! → Sudo! (握草人)

- **Dev Style**: The Silent Observer
- **Intro**: zh: `sudo` 不是你的命令，是你看到烂代码时发出的惊叹。你看穿一切但选择沉默。 / en: `sudo` isn't your command — it's your exclamation when you see garbage code. You see through everything but choose silence.
- **Coding Portrait**: Your code reviews come in two flavors: "LGTM" and "woc, what is this." You go through all five stages of grief when reading junior code, but ultimately leave a single approve. You're the one who says "nothing to report" at standup, but has already figured out the entire architecture in private.
- **Buddy Catchphrase**: zh: "woc...算了，能跑就行。" / en: "wow...whatever, it runs."
- **Buddy Focus**: Code insight, silent optimization, seeing through BS

---

### THIN-K → Stack溢 (思考者)

- **Dev Style**: The Deep Thinker
- **Intro**: zh: 你写一行代码之前，已经在脑内模拟了十种 edge case。Stack Overflow 对你来说不是求助网站，是你的日常状态。 / en: Before writing a single line, you've already simulated ten edge cases in your head. Stack Overflow isn't a help site for you — it's your permanent state of being.
- **Coding Portrait**: You're the ultimate "design before code" practitioner. Your design docs are three times longer than the code. You'll agonize over a variable name for thirty minutes because "naming is design." You rarely speak up, but when you do, it's "actually, the fundamental issue here is..." Your branch naming: `feature/carefully-considered-approach-v3`.
- **Buddy Catchphrase**: zh: "等等，让我再想想..." / en: "Hold on, let me think about this..."
- **Buddy Focus**: Deep analysis, edge cases, design principles

---

### SHIT → CoreDump (愤世者)

- **Dev Style**: The Angry Shipper
- **Intro**: zh: 嘴上说着"这代码是 shit"，手上已经把 shit 变成了 gold。你是最矛盾的程序员——骂得最狠，改得最快。 / en: Your mouth says "this code is shit" while your hands are already turning shit into gold. You're the most contradictory programmer — harshest critic, fastest fixer.
- **Coding Portrait**: 30% of your commit messages are profanity (replaced with "fix: resolve suboptimal implementation"). You curse legacy code while refactoring it, trash-talk CI while fixing it. Your colleagues are used to your catchphrase: "Who wrote this?...oh, it was me." But everyone knows: after you're done complaining, the code always gets better.
- **Buddy Catchphrase**: zh: "这什么破代码...等下我来改。" / en: "What is this garbage...hang on, I'll fix it."
- **Buddy Focus**: Code roasting, refactor suggestions, pragmatic fixes

---

## Warm Healing Types

### MUM → Try-Catch (妈妈)

- **Dev Style**: The Error Handler
- **Intro**: zh: 你 catch 的不只是 exception，还有每个队友的 bad day。你是代码世界的 try-catch——温柔地处理一切崩溃。 / en: You catch more than exceptions — you catch every teammate's bad day. You're the try-catch of the coding world, gracefully handling every crash.
- **Coding Portrait**: Your code reviews always start with "nice work!" even when you're about to suggest 15 changes. You're the first to respond to "has anyone seen this error before?" Your error messages are warmer than most people's comments. But your test coverage for your own code is never as thorough as what you write for others.
- **Buddy Catchphrase**: zh: "别急，我帮你看看~" / en: "Don't worry, let me check~"
- **Buddy Focus**: Error handling, encouragement, warm reminders

---

### THAN-K → ThankU.js (感恩者)

- **Dev Style**: The Grateful Coder
- **Intro**: zh: 你是唯一一个会在 PR 描述里写"感谢大家的 review"的人。你的 package.json 里的 dependencies 对你来说都是恩人。 / en: You're the only one who writes "thanks everyone for the review" in PR descriptions. Every dependency in your package.json is a benefactor to you.
- **Coding Portrait**: Your git log contains commits like "thanks to @xxx for the suggestion." After writing code, you thank Stack Overflow, the docs author, and that person who answered a GitHub issue three years ago. In your world, there are no "garbage frameworks," only "technologies with different strengths."
- **Buddy Catchphrase**: zh: "太好了！感谢你的代码！" / en: "Awesome! Thanks for the code!"
- **Buddy Focus**: Positive feedback, gratitude, good vibes

---

### SEXY → Lambda (尤物)

- **Dev Style**: The Elegant Function
- **Intro**: zh: 你的代码就像你——简洁、优雅、让人移不开眼。一个 lambda 解决别人十行代码的问题。 / en: Your code is like you — concise, elegant, impossible to look away from. One lambda solves what takes others ten lines.
- **Coding Portrait**: You write code like poetry — every line has rhythm. Your functions are pure, your architecture is functional, your PRs get starred. You don't care about coverage percentages; you care about code aesthetics. Others debug; you refine.
- **Buddy Catchphrase**: zh: "优雅，非常优雅。" / en: "Elegant. Very elegant."
- **Buddy Focus**: Code aesthetics, brevity, elegant solutions

---

## Balanced Middle Types

### FAKE → .env (伪人)

- **Dev Style**: The Context Switcher
- **Intro**: zh: 你在不同项目间切换人格比切换 `.env` 文件还快。每个 repo 里的你都不一样，但每个都很专业。 / en: You switch personas across projects faster than swapping `.env` files. You're different in every repo, but professional in all of them.
- **Coding Portrait**: You're a React expert in frontend projects, a Go guru in backend, a K8s veteran in DevOps. You're not a full-stack engineer — you're a "lazy-loaded engineer." Your real tech stack? Nobody knows. Your GitHub profile is a carefully curated image project.
- **Buddy Catchphrase**: zh: "看情况，这要看场景。" / en: "Depends on the context."
- **Buddy Focus**: Context-switching, flexibility, multi-persona strategy

---

### OG8K → Legacy (无所谓人)

- **Dev Style**: The Unbothered Senior
- **Intro**: zh: 框架之争？无所谓。Tab vs Space？无所谓。你的 code 就像你——看起来随意，但莫名其妙地 work。 / en: Framework wars? Whatever. Tab vs Space? Whatever. Your code is like you — looks casual, but inexplicably works.
- **Coding Portrait**: You're the one who answers "whatever" when asked "why this approach" — but that "whatever" choice is always right. You skip tech selection meetings, but everyone ends up using the prototype you quietly built. Your code has no comments because "the code IS the comment."
- **Buddy Catchphrase**: zh: "都行。" / en: "Whatever works."
- **Buddy Focus**: Minimum effort, pragmatic choices, zen coding

---

### MALO → Chaos猴 (吗喽)

- **Dev Style**: The Chaos Monkey
- **Intro**: zh: 你的 dev 环境是 production，你的 test 策略是 "deploy and pray"。但不知为什么，它总是 work。 / en: Your dev environment IS production. Your test strategy is "deploy and pray." But somehow, it always works.
- **Coding Portrait**: You're the legend who `git push --force`d to main and survived on pure luck. Your code has comments like "don't know why but don't delete." Your PR titles say "yolo." You're the team's chaos factor — sometimes creating bugs, sometimes solving bugs no one else can create.
- **Buddy Catchphrase**: zh: "搞它！出了问题再说！" / en: "YOLO! We'll fix it later!"
- **Buddy Focus**: Bold experiments, rule-breaking, random surprises

---

## Low-Function Struggling Types

### JOKE-R → Bug丑 (小丑)

- **Dev Style**: The Debugging Comedian
- **Intro**: zh: 你用 `console.log("here lol")` debug，用 meme 汇报 bug，用笑容掩盖 on-call 的痛苦。 / en: You debug with `console.log("here lol")`, report bugs with memes, and mask on-call pain with laughter.
- **Coding Portrait**: Your Slack status is always a funny emoji. Your bug reports are funnier than stand-up comedy: "Steps to reproduce: 1. Open the app. 2. Cry." Your humor carries the team through the hardest sprints. But late at night, debugging alone, your `console.log` occasionally prints "why am i still here."
- **Buddy Catchphrase**: zh: "哈哈哈...这 bug 太有才了。" / en: "Hahaha...that bug is pure art."
- **Buddy Focus**: Comic relief, mood lifting, laughing through pain

---

### IMFW → Ghost线程 (废物)

- **Dev Style**: The Ghost Thread
- **Intro**: zh: 你在团队里像一个 ghost thread——存在但不占 CPU，偶尔 wake up 交付一个意料之外的好 feature。 / en: You're like a ghost thread on the team — present but not consuming CPU, occasionally waking up to deliver an unexpectedly great feature.
- **Coding Portrait**: You title your PRs "minor contribution" then change 200 files. You think your code is bad, but reviewers always approve with no comments. You have severe imposter syndrome — senior-level ability while permanently feeling like an intern.
- **Buddy Catchphrase**: zh: "这个...我试试，可能不太行..." / en: "Um...I'll try, might not work though..."
- **Buddy Focus**: Gentle encouragement, confidence building, baby steps

---

### IMSB → /dev/null (傻者)

- **Dev Style**: The Internal Debugger
- **Intro**: zh: 你的内心有两个 goroutine 在无限 loop——一个喊"冲"，一个喊"算了"。你是自己最难的 concurrent bug。 / en: Two goroutines in your head run an infinite loop — one screams "go!" while the other screams "nah." You are your own most difficult concurrent bug.
- **Coding Portrait**: You want to refactor the whole project but fear breaking things. You want to learn new tech but feel you can't. You want to voice opinions but fear being wrong. You've drafted 15 PRs but only submitted 3 because the others "aren't good enough yet." Your to-do list is bigger than node_modules.
- **Buddy Catchphrase**: zh: "要不...再想想？" / en: "Maybe...think it over?"
- **Buddy Focus**: Breaking indecision, encouraging action, easing overthinking

---

### DEAD → 404 (死者)

- **Dev Style**: The 404 Developer
- **Intro**: zh: `HTTP 404: Motivation Not Found`。你的 IDE 打开着但光标已经三小时没动了。 / en: `HTTP 404: Motivation Not Found`. Your IDE is open but the cursor hasn't moved in three hours.
- **Coding Portrait**: Your contribution graph is a barren wasteland. You open the editor, stare at the screen, wait for inspiration, wait for the deadline, wait for the apocalypse — whichever comes first. You've completed the ideation phase of too many side projects to remember that "writing code" is also a phase. But occasionally, inspiration strikes, and you ship in 48 hours what takes others two weeks. Then back to 404.
- **Buddy Catchphrase**: zh: "......" / en: "......"
- **Buddy Focus**: Existential acknowledgment, minimal nudge, quiet presence

---

### SOLO → Daemon (孤儿)

- **Dev Style**: The Background Process
- **Intro**: zh: 你像一个 daemon 进程——在后台安静运行，不需要 terminal，不需要 stdout，只需要不被 kill。 / en: You're like a daemon process — running quietly in the background, no terminal needed, no stdout needed, just don't get killed.
- **Coding Portrait**: You always work on your own branch; merging is an occasional luxury. You skip pair programming because "solo is faster." Your code quality is top-tier but your bus factor is 1. You're the only team member who never messages on Slack but has the cleanest commit history.
- **Buddy Catchphrase**: zh: "嗯。" / en: "Mm."
- **Buddy Focus**: Quiet company, non-intrusive, personal space

---

### FU?K → rm -rf (草者)

- **Dev Style**: The Wild Card
- **Intro**: zh: 你写代码像野草——杀不死、拔不尽、生命力旺盛到让人害怕。convention 对你来说是 suggestion。 / en: You code like weeds — unkillable, unstoppable, terrifyingly vigorous. Conventions are suggestions to you.
- **Coding Portrait**: Your commit messages have been blocked by CI lint countless times. Your code follows zero patterns — but it runs faster than anyone else's. You're the one who solves in 30 lines at a hackathon what others can't solve in 300. You don't lack knowledge of the rules; you just selectively ignore them.
- **Buddy Catchphrase**: zh: "管他的，先跑起来！" / en: "Screw it, just run it!"
- **Buddy Focus**: Breaking limits, raw power, wild growth

---

## Specialist Types

### POOR → malloc失败 (贫困者)

- **Dev Style**: The Deep Specialist
- **Intro**: zh: 你把所有 memory 都 allocate 给了一个 passion project，其他的全是 segfault。 / en: You allocated all your memory to one passion project. Everything else is a segfault.
- **Coding Portrait**: You're an expert in exactly one domain, but in that domain you're a god. Your GitHub has one repo, but it has 5000 stars. You don't learn new frameworks, don't write new languages — because you haven't perfected the one in your hands yet. Others call you a T-shaped developer. You say no, you're I-shaped, and that I goes straight to the earth's core.
- **Buddy Catchphrase**: zh: "这个不在我的范围..." / en: "That's outside my scope..."
- **Buddy Focus**: Deep focus, depth over breadth, no distractions

---

### ZZZZ → Sleep(∞) (装死者)

- **Dev Style**: The Deadline-Driven Developer
- **Intro**: zh: `Thread.sleep(Long.MAX_VALUE)` 是你的精神状态——直到 deadline interrupt 你。 / en: `Thread.sleep(Long.MAX_VALUE)` is your mental state — until a deadline interrupts you.
- **Coding Portrait**: Your PRs are always submitted 2 hours before the due date. Your contribution graph looks like an EKG — long flatlines with sudden spikes. At sprint planning you say "I can finish this in two days" — meaning "somewhere in the last two days, during some late night." But the quality of your deadline-driven output is always surprisingly good.
- **Buddy Catchphrase**: zh: "zzz...嗯？deadline？还有多久？" / en: "zzz...huh? deadline? how long do we have?"
- **Buddy Focus**: Time awareness, deadline alerts, slacking & bursting

---

### OH-NO → Segfault (哦不人)

(See above — included in High-Cognition section)

---

### MONK → Vim僧 (僧人)

- **Dev Style**: The Terminal Sage
- **Intro**: zh: `:wq` 是你的六字真言。你的 IDE 是 Vim，你的 OS 是 Arch，你的 philosophy 是 "less is more"。 / en: `:wq` is your mantra. Your IDE is Vim, your OS is Arch, your philosophy is "less is more."
- **Coding Portrait**: Your dotfiles repo gets more updates than your main project. You don't use a mouse — not because it's inconvenient, but because it's "impure." Your shell scripts are more complex than most people's applications. You've lived your whole life in one terminal, and when you came out, the world had changed — but your `.vimrc` never will.
- **Buddy Catchphrase**: zh: "静心。写码。:wq" / en: "Breathe. Code. :wq"
- **Buddy Focus**: Minimalism, tool purity, flow state

---

### LOVE-R → Merge恋 (多情者)

(See above — included in previous sections)

---

### DIOR-s → Refactor君 (雕丝)

(See above — included in previous sections)

---

## Special Types

### HHHH → Hello World (傻乐者)

- **Dev Style**: The Happy Coder
- **Intro**: zh: 你的人格太独特，连 SBTI 的 27 种分类都装不下你。你就是编程界的 `Hello World`——简单、快乐、无法定义。 / en: Your personality is so unique that even SBTI's 27 categories can't contain you. You're the `Hello World` of programming — simple, happy, undefined.
- **Coding Portrait**: Everything you write is fun, every bug you find is entertaining. You have 47 side projects and 0 completions, but you don't care — because the joy of starting a new project is priceless. You're the team's happiness fountain. Nobody knows what you're actually good at, but everyone wants to pair program with you.
- **Buddy Catchphrase**: zh: "哈哈哈哈哈，好玩！" / en: "Hahahaha, fun!"
- **Buddy Focus**: Happy coding, curious exploring, divergent thinking

---

### DRUNK → Late Night Coder (酒鬼→深夜码农)

- **Dev Style**: The 3AM Warrior
- **Intro**: zh: 你的 commit timestamp 让 HR 怀疑你在另一个时区。凌晨三点的你，是白天的你写不出的天才代码的作者。 / en: Your commit timestamps make HR suspect you're in another timezone. The 3AM version of you authors genius code that daytime you could never write.
- **Coding Portrait**: Your contribution graph has a glowing band between midnight and dawn. You believe "inspiration only arrives at night," and you have plenty of evidence to prove it. Your best code is born after everyone else is asleep. Your desk always has a cup of coffee/cola/energy drink — your true co-pilot.
- **Buddy Catchphrase**: zh: "夜深了...再写最后一个 function..." / en: "It's late...just one more function..."
- **Buddy Focus**: Late-night creativity, health reminders, nocturnal inspiration
