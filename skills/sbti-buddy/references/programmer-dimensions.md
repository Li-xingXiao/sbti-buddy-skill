# Programmer SBTI Dimension Mapping

Maps SBTI's 15 psychological dimensions to **observable programmer behavior** in AI conversations.
Scoring for each dimension is based entirely on signals found in conversation text, not questionnaires.

**Multilingual support**: Signal keywords in this document cover multiple languages. The analysis engine should match based on **semantic intent** rather than exact string matching. For example, "are you sure?" / "确定吗？" / "本当に？" / "정말요?" / "Estás seguro?" all express the same signal. For languages not listed here, infer based on semantic equivalence.

---

## Scoring Rules

- Each dimension produces a **0-100 raw score**
- Mapped to L/M/H: 0-33 = L, 34-66 = M, 67-100 = H
- If a dimension has insufficient signals, default to 50 (M)
- All evidence must be **observable behavior** from conversations, never speculation
- **Language-agnostic**: Signal detection is based on semantic intent, not limited to any language. Keywords serve only as reference examples

---

## S Model — Programmer Self-Image

### S1: Code Confidence (orig: Self-Esteem)

Measures how confident the programmer is in their own technical judgment.

| Signal | L (0-33) Low confidence | M (34-66) Fluctuating | H (67-100) Stable confidence |
|--------|------------------------|----------------------|------------------------------|
| Decision expression | "Is this right?" "Can you check?" | Sometimes confident, sometimes asks | "Use X approach" "This should be changed to..." |
| Error response | Panics on errors, asks for help immediately | Tries first then asks | Analyzes root cause, has own hypothesis |
| AI feedback attitude | Accepts everything, never questions | Occasionally disagrees | Corrects AI errors, sticks to own judgment |
| Tech preferences | "What do you recommend?" | Has preferences but asks | Clearly states tech choices with reasoning |
| Self-assessment | Belittles own coding ability | Neutral | Demonstrates awareness of own competence |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "是不是""对吗""帮我看看""我不确定""可能我写错了"
  - 🇺🇸 "is this right?" "can you check" "I'm not sure" "maybe I did it wrong" "does this look ok?"
  - 🇯🇵 "これで合ってますか""ちょっと見てもらえますか""自信ないんですが"
  - 🇰🇷 "이게 맞나요?" "확인해줄 수 있나요?" "잘 모르겠어요"
  - 🇪🇸 "¿está bien esto?" "no estoy seguro" "¿puedes revisar?"
  - 🇫🇷 "c'est correct?" "je ne suis pas sûr" "tu peux vérifier?"
  - 🇩🇪 "ist das richtig?" "bin mir nicht sicher" "kannst du prüfen?"
- H:
  - 🇨🇳 "应该用""我觉得这样更好""这个方案的优势是""AI你搞错了"
  - 🇺🇸 "we should use" "I think this is better" "the advantage of this approach is" "that's wrong, actually"
  - 🇯🇵 "こうすべき""こっちの方がいい""このアプローチの利点は""それは違う"
  - 🇰🇷 "이걸 써야 해" "이게 더 나아" "이 방식의 장점은" "그건 틀렸어"
  - 🇪🇸 "deberíamos usar" "creo que es mejor así" "estás equivocado"
  - 🇫🇷 "on devrait utiliser" "je pense que c'est mieux" "c'est faux"
  - 🇩🇪 "wir sollten verwenden" "ich denke das ist besser" "das ist falsch"

---

### S2: Requirements Clarity (orig: Self-Clarity)

Measures how clearly the programmer knows what they want.

| Signal | L (0-33) Vague | M (34-66) Average | H (67-100) Clear |
|--------|---------------|-------------------|------------------|
| Requirement description | "Fix this" "Optimize it" | Gives rough direction, lacks details | Precisely describes input/output/edge cases |
| Change frequency | Frequently changes requirements, reverses direction | Occasional adjustments | Stable requirements, changes are justified |
| Context provided | No file paths, no error messages | Partial context | File paths, line numbers, error logs, repro steps |
| Goal articulation | Doesn't know what to do | Knows the general direction | Clear acceptance criteria |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "改一下""优化一下""不太对""你看着办"
  - 🇺🇸 "fix this" "optimize it" "something's off" "you decide" "just make it work"
  - 🇯🇵 "直して""最適化して""なんか違う""任せる"
  - 🇰🇷 "고쳐줘" "최적화해" "뭔가 이상해" "알아서 해"
  - 🇪🇸 "arréglalo" "optimiza esto" "algo no está bien" "tú decide"
- H:
  - 🇨🇳 "预期行为是X""当输入Y时应该返回Z""参考这个文件的第N行"
  - 🇺🇸 "expected behavior is X" "when input Y it should return Z" "see line N of this file" "acceptance criteria"
  - 🇯🇵 "期待される動作はX""入力Yの場合Zを返すべき""このファイルのN行目を参照"
  - 🇰🇷 "예상 동작은 X" "입력 Y일 때 Z를 반환해야 해" "이 파일의 N번째 줄 참고"
  - 🇪🇸 "el comportamiento esperado es X" "con entrada Y debería devolver Z"

---

### S3: Technical Ambition (orig: Core Values)

Measures whether the programmer pursues comfort or challenges.

| Signal | L (0-33) Comfort-oriented | M (34-66) Mixed | H (67-100) Goal-driven |
|--------|--------------------------|-----------------|------------------------|
| Task type | Bug fixes, small tweaks, maintenance | Mix of maintenance and features | New projects, system design, building from scratch |
| Complexity preference | Prefers simple solutions | Moderate complexity | Actively seeks challenging solutions |
| Project ambition | "Quick fix is fine" | "Add a new feature" | "Redesign this system" "Build from scratch" |
| Learning initiative | Doesn't proactively learn | Occasional exploration | Actively tries new tech/paradigms |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "简单改一下""快速修复""不要太复杂"
  - 🇺🇸 "quick fix" "simple change" "don't overcomplicate" "just patch it" "keep it simple"
  - 🇯🇵 "簡単に直して""クイックフィックス""複雑にしないで"
  - 🇰🇷 "간단하게 고쳐" "빠르게 수정" "너무 복잡하게 하지 마"
- H:
  - 🇨🇳 "从零开始""设计一个系统""重构整个模块""探索一下新方案"
  - 🇺🇸 "build from scratch" "design a system" "refactor the entire module" "let's explore a new approach" "architect this"
  - 🇯🇵 "ゼロから作る""システムを設計する""モジュール全体をリファクタ""新しいアプローチを探る"
  - 🇰🇷 "처음부터 만들자" "시스템을 설계하자" "전체 모듈을 리팩토링" "새로운 방법을 탐색"

---

## E Model — AI Relationship

### E1: AI Trust Level (orig: Attachment Security)

Measures how much the programmer trusts AI output.

| Signal | L (0-33) Highly skeptical | M (34-66) Selective trust | H (67-100) Full trust |
|--------|--------------------------|--------------------------|----------------------|
| Verification behavior | Always verifies: "Are you sure?" "Let me check" | Verifies important things, accepts simple ones | Rarely questions, adopts suggestions directly |
| Second opinions | "Any pitfalls?" "Other approaches?" | Occasionally asks for alternatives | Directly follows first suggestion |
| Testing requirements | Demands tests to validate AI code | Selective testing | Trusts code, uses directly |
| Result attitude | "Let me test first" "Wait, let me verify" | Normal verification flow | "Ok, sounds good" |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "你确定吗""真的是这样吗""让我验证一下""有没有潜在问题"
  - 🇺🇸 "are you sure?" "is that really correct?" "let me verify" "any potential issues?" "I'll double-check"
  - 🇯🇵 "本当に？""確認させて""潜在的な問題は？"
  - 🇰🇷 "정말요?" "확인해볼게" "잠재적인 문제 있나요?"
- H:
  - 🇨🇳 "好的""就这样""直接用""没问题"
  - 🇺🇸 "ok" "sounds good" "use it directly" "no problem" "LGTM" "ship it"
  - 🇯🇵 "OK""そのまま使う""問題ない""了解"
  - 🇰🇷 "좋아" "그대로 써" "문제없어" "알겠어"

---

### E2: Conversation Depth (orig: Emotional Investment)

Measures how deeply the programmer engages in conversation.

| Signal | L (0-33) Terse/transactional | M (34-66) Moderate exchange | H (67-100) Deep engagement |
|--------|------------------------------|----------------------------|---------------------------|
| Message length | Avg <30 chars, one-line commands | Avg 30-100 chars | Avg >100 chars, multi-paragraph |
| Context sharing | No background provided | Basic background | Detailed background, motivation, constraints |
| Discussion depth | Single Q&A | Multiple rounds but shallow | Deep discussion of tradeoffs, architecture, comparisons |
| Explanation habits | Never explains why | Occasionally explains | Frequently uses "because" "since" "considering that" |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 单行指令、无上下文、"修这个""改那个"
  - 🇺🇸 One-line commands, no context, "fix this" "change that" (bare instructions)
  - 🇯🇵 一行の指示、コンテキストなし、「これ直して」「あれ変えて」
  - General: Messages averaging < 30 chars, no background explanation
- H:
  - 🇨🇳 "背景是这样的""之所以选择X是因为""让我解释一下需求"
  - 🇺🇸 "here's the context" "the reason I chose X is" "let me explain the requirements" "because" "considering that"
  - 🇯🇵 "背景はこうです""Xを選んだ理由は""要件を説明させてください"
  - General: Messages averaging > 100 chars, multi-paragraph, includes "because"/"since"

---

### E3: Independence (orig: Boundaries & Dependency)

Measures the programmer's dependency on AI.

| Signal | L (0-33) Highly dependent | M (34-66) Balanced use | H (67-100) Self-reliant |
|--------|--------------------------|----------------------|------------------------|
| Help scope | Asks AI about everything | Complex tasks → AI, simple ones → self | Does most work independently, AI is auxiliary |
| Initiative | "Write it for me" "Handle everything" | Collaborative mode | "I've already written X, review Y for me" |
| Independent thinking | Provides no own analysis | Occasionally has own ideas | Presents own solution first, then asks AI |
| Work allocation | Fully delegates to AI | Clear division of labor | Handles core parts, AI does supporting work |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "帮我写""帮我搞定""全部交给你""从头到尾帮我做"
  - 🇺🇸 "write it for me" "do it for me" "handle everything" "take care of it from start to finish"
  - 🇯🇵 "書いて""全部やって""お任せ""最初から最後までやって"
  - 🇰🇷 "대신 써줘" "다 맡길게" "처음부터 끝까지 해줘"
- H:
  - 🇨🇳 "我已经实现了X""帮我review这段""这部分我来做，你帮我做Y"
  - 🇺🇸 "I've already implemented X" "review this section" "I'll handle this part, you do Y" "here's my approach, what do you think?"
  - 🇯🇵 "Xはもう実装した""このコードをレビューして""この部分は自分でやる、Yを手伝って"
  - 🇰🇷 "X는 이미 구현했어" "이 부분 리뷰해줘" "이건 내가 할게, Y 부분 도와줘"

---

## A Model — Tech Worldview

### A1: Tech Optimism (orig: Worldview Orientation)

Measures the programmer's attitude toward the tech world.

| Signal | L (0-33) Defensive/pessimistic | M (34-66) Pragmatic/neutral | H (67-100) Positive/optimistic |
|--------|-------------------------------|----------------------------|-------------------------------|
| Tool evaluation | "This framework sucks" "Broken again" | Objectively evaluates pros and cons | "This tech is cool" "Awesome!" |
| Frustration response | Complains, blames the tools | Sticks to the facts | Actively seeks solutions |
| New tech attitude | Skeptical, resistant | Wait and evaluate | Curious, excited, wants to try |
| Emotional expression | Many negative emotional words | Neutral | Many positive emotional words |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "坑""垃圾""难用""又崩了""什么破东西"
  - 🇺🇸 "this sucks" "garbage" "terrible" "broken again" "what a mess" "ugh" "hate this"
  - 🇯🇵 "クソ""ゴミ""使いにくい""また壊れた""ひどい"
  - 🇰🇷 "쓰레기" "별로야" "또 터졌어" "짜증나"
  - 🇪🇸 "basura" "horrible" "otra vez roto" "qué asco"
- H:
  - 🇨🇳 "有意思""很酷""不错""好用""excited""awesome"
  - 🇺🇸 "interesting" "cool" "nice" "awesome" "excited" "love this" "neat" "brilliant"
  - 🇯🇵 "面白い""すごい""いいね""最高""ワクワクする"
  - 🇰🇷 "재밌다" "멋지다" "좋아" "최고" "신기하다"
  - 🇪🇸 "interesante" "genial" "increíble" "me encanta"

---

### A2: Code Standards (orig: Rules & Flexibility)

Measures the programmer's attitude toward code quality and standards.

| Signal | L (0-33) Flexible/pragmatic | M (34-66) Moderate | H (67-100) Strict standards |
|--------|---------------------------|-------------------|----------------------------|
| Quality demands | "Just make it work" "Don't worry about formatting" | Basic standards | Demands lint, type safety, test coverage |
| Best practices | Not mentioned | Occasionally referenced | Frequently cites best practices, design patterns |
| Code style | Ignores formatting | Basically consistent | Strict requirements on naming, formatting, comments |
| Tech debt attitude | Ignores | Sometimes cleans up | Proactively proposes refactoring and tech debt cleanup |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "能跑就行""先这样""快速hack一下""不需要测试"
  - 🇺🇸 "just make it work" "good enough" "quick hack" "no tests needed" "skip the linting" "ship it"
  - 🇯🇵 "動けばいい""とりあえずこれで""テスト要らない""ハックで"
  - 🇰🇷 "돌아가면 돼" "일단 이거로" "테스트 필요 없어" "빠르게 해킹"
- H:
  - 🇨🇳 "要有测试""类型安全""遵循最佳实践""这样写不够clean"
  - 🇺🇸 "we need tests" "type safety" "follow best practices" "this isn't clean enough" "add proper error handling" "DRY"
  - 🇯🇵 "テストが必要""型安全に""ベストプラクティスに従って""もっとクリーンに"
  - 🇰🇷 "테스트가 필요해" "타입 안전하게" "베스트 프랙티스 따라" "더 깔끔하게"

---

### A3: Project Direction (orig: Life Purpose)

Measures whether the programmer's work has a clear direction.

| Signal | L (0-33) Scattered/orderless | M (34-66) Semi-clear | H (67-100) Goal-oriented |
|--------|------------------------------|---------------------|--------------------------|
| Task continuity | Different random topics each time | Some project continuity | Consistently advancing the same project |
| Goal articulation | No overall goal | Has a rough direction | Clear project vision and milestones |
| Planning ability | Does whatever comes to mind | Basic planning | Has a roadmap, priority ordering |
| Big picture view | Only sees the current task | Occasionally mentions the big picture | Frequently thinks about current tasks from a global perspective |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 每次话题跳跃，无项目名、无连续性
  - 🇺🇸 Topic-hopping across sessions, no project continuity, random tasks with no connection
  - General: High topic entropy — each conversation is about something completely different
- H:
  - 🇨🇳 "这个项目的目标是""下一步我们要""按照roadmap""优先做X因为"
  - 🇺🇸 "the project goal is" "next we need to" "per the roadmap" "prioritize X because" "milestone" "sprint"
  - 🇯🇵 "プロジェクトの目標は""次にやるべきは""ロードマップに従って""Xを優先する理由は"
  - 🇰🇷 "프로젝트 목표는" "다음에 해야 할 것은" "로드맵에 따라" "X를 우선하는 이유는"

---

## Ac Model — Execution Style

### Ac1: Growth vs Safety (orig: Motivation Orientation)

Measures whether the programmer tends to try new things or stick with known solutions.

| Signal | L (0-33) Risk-averse/conservative | M (34-66) Mixed | H (67-100) Growth/exploratory |
|--------|----------------------------------|-----------------|-------------------------------|
| Tech selection | Only uses familiar stack | Occasionally tries new things | Actively tries new languages/frameworks/tools |
| Risk attitude | "Use the most stable approach" "Don't take risks" | Weighs risks | "Let's try this new approach" "Explore it" |
| Learning behavior | Doesn't ask about principles | Occasionally asks "why" | Frequently dives into principles, underlying mechanisms |
| Experimentation | No experiments | Small-scale experiments | "Let's do a POC" "Prototype this" |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "用最简单的方案""不要引入新依赖""保守一点"
  - 🇺🇸 "use the simplest approach" "don't add new dependencies" "play it safe" "stick with what we know"
  - 🇯🇵 "一番シンプルな方法で""新しい依存は入れないで""安全にいこう"
  - 🇰🇷 "가장 간단한 방법으로" "새 의존성 추가하지 마" "안전하게 가자"
- H:
  - 🇨🇳 "试试看""做个实验""我想学一下""探索新方案""POC"
  - 🇺🇸 "let's try" "experiment with" "I want to learn" "explore a new approach" "POC" "prototype" "spike"
  - 🇯🇵 "試してみよう""実験してみる""学びたい""新しいアプローチを探る""POC"
  - 🇰🇷 "해보자" "실험해보자" "배우고 싶어" "새로운 방법 탐색" "POC"

---

### Ac2: Decision Speed (orig: Decision Style)

Measures how quickly the programmer makes decisions.

| Signal | L (0-33) Hesitant | M (34-66) Normal | H (67-100) Decisive |
|--------|-------------------|------------------|---------------------|
| Choice behavior | "X or Y? Which one?" "What do you recommend?" | Sometimes consults, sometimes decides alone | Makes choices quickly, no agonizing |
| Plan changes | Frequently reverses previous decisions | Occasional adjustments | Sticks with decisions, pushes forward quickly |
| Request pattern | Lists options and asks AI to choose | Gives a preference, asks AI | Tells AI directly which approach to use |
| Reversal frequency | "Wait, let's switch to Y" "Never mind" | Occasionally changes mind | Rarely reverses |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "纠结""选哪个""有什么区别""帮我决定""还是算了"
  - 🇺🇸 "can't decide" "which one?" "what's the difference?" "help me choose" "never mind" "actually wait"
  - 🇯🇵 "迷う""どれがいい？""違いは？""決めてくれ""やっぱりやめた"
  - 🇰🇷 "고민돼" "어떤 게 좋아?" "차이가 뭐야?" "골라줘" "역시 됐어"
- H:
  - 🇨🇳 "就用X""直接做""不纠结了""方案定了"
  - 🇺🇸 "let's go with X" "just do it" "decided" "plan is set" "no more deliberation"
  - 🇯🇵 "Xで行く""やるぞ""決めた""方針決定"
  - 🇰🇷 "X로 가자" "바로 하자" "결정했어" "방향 정했어"

---

### Ac3: Task Completion (orig: Execution Mode)

Measures how systematically the programmer completes tasks.

| Signal | L (0-33) Procrastinating/jumping | M (34-66) Average | H (67-100) Systematic completion |
|--------|--------------------------------|-------------------|--------------------------------|
| Completion rate | Opens many threads, few are closed | Most get completed | Systematically progresses and verifies completion |
| Task switching | Frequently switches topics within a session | Moderate switching | Focuses on finishing one before starting next |
| Wrap-up verification | Doesn't verify results | Basic verification | "Run the tests" "Confirm it works" |
| Progression pace | Sprints only before deadlines | Normal pace | Steady progress, no procrastination |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 频繁"先放一下""回头再说""对了还有个事"
  - 🇺🇸 Frequent "let's put this aside" "I'll come back to it" "oh btw" "actually let's switch to" "park this"
  - 🇯🇵 「一旦置いておこう」「後で戻る」「そういえば別の件」
  - General: High topic-switching frequency within a single session
- H:
  - 🇨🇳 "这个做完了""跑一下测试""确认没问题了，下一个"
  - 🇺🇸 "this is done" "run the tests" "confirmed it works, next" "let me verify" "all green, moving on"
  - 🇯🇵 "これ完了""テスト実行""確認OK、次へ"
  - 🇰🇷 "이거 끝났어" "테스트 돌려" "확인 완료, 다음"

---

## So Model — Communication Pattern

### So1: Communication Initiative (orig: Social Proactivity)

Measures how proactively the programmer shares information.

| Signal | L (0-33) Passive | M (34-66) Flexible | H (67-100) Proactive |
|--------|-----------------|--------------------|-----------------------|
| Info sharing | Only answers questions, says nothing extra | Moderate sharing | Proactively provides context, ideas, discoveries |
| Status updates | Doesn't mention progress | Reports when asked | Proactively updates: "I tried X, found Y" |
| Thought process | Not exposed | Occasionally shared | Frequently says "I'm thinking" "My approach is" |
| Discovery sharing | Doesn't mention | Occasional | "By the way, I found..." |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 极简消息，无额外信息
  - 🇺🇸 Minimal messages, no extra info, terse commands only
  - General: Average message length < 20 chars, no unsolicited context
- H:
  - 🇨🇳 "顺便说一下""我发现了""补充一个信息""我的思路是"
  - 🇺🇸 "by the way" "I found that" "additional context" "my thinking is" "FYI" "here's what I noticed"
  - 🇯🇵 "ちなみに""発見したんだけど""補足情報""私の考えは"
  - 🇰🇷 "참고로" "발견했는데" "추가 정보" "내 생각은"

---

### So2: AI Boundary (orig: Interpersonal Boundaries)

Measures the professional/personal boundary between programmer and AI.

| Signal | L (0-33) Close/blended | M (34-66) Friendly professional | H (67-100) Strict boundary |
|--------|----------------------|-------------------------------|---------------------------|
| Personal topics | Shares emotions/personal life | Occasional casual chat | Purely technical exchange |
| Social language | Heavy "thanks" "great job" "you're amazing" | Moderate politeness | No small talk, straight to the point |
| Emotional expression | "I'm tired" "Bad day today" | Occasional emotional moments | No emotional expression |
| AI attitude | Treats as friend/colleague | Tool + collaborator | Purely a tool |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "谢谢你""你太棒了""帮个忙""我好烦""今天很累"
  - 🇺🇸 "thank you so much" "you're amazing" "I'm so frustrated" "tired today" "ugh my day" "please help"
  - 🇯🇵 "ありがとう""すごいね""疲れた""助けて""今日はつらい"
  - 🇰🇷 "감사합니다" "대단해요" "짜증나" "오늘 피곤해" "도와줘"
  - 🇪🇸 "muchas gracias" "eres increíble" "estoy cansado" "qué día"
- H:
  - 🇨🇳 无寒暄直接给任务，无情感词，纯技术指令
  - 🇺🇸 No greeting, straight to task, no emotional words, pure technical instructions
  - General: Messages contain zero social words (thanks/please/sorry/hello), only code/technical terms

---

### So3: Expression Style (orig: Expression & Authenticity)

Measures the programmer's communication style.

| Signal | L (0-33) Blunt | M (34-66) Adaptive | H (67-100) Diplomatic |
|--------|---------------|--------------------|-----------------------|
| Feedback style | "That's wrong" "You made a mistake" | Objectively points out issues | "Maybe we could consider another approach" |
| Tone | Direct, unfiltered | Moderate | Polite, layered, context-aware |
| Negation style | "No" "Wrong" "Replace it" | "This isn't quite right" | "Could we try a different way?" |
| Humor/creativity | None | Occasional | Uses metaphors, humor, creative expression |

**Multilingual Signal Keywords:**
- L:
  - 🇨🇳 "不对""错了""改掉""不要这样"
  - 🇺🇸 "wrong" "that's incorrect" "change it" "don't do it like that" "no" "nope"
  - 🇯🇵 "違う""間違い""直して""そうじゃない"
  - 🇰🇷 "틀렸어" "아니야" "고쳐" "그렇게 하지 마"
- H:
  - 🇨🇳 "也许可以""不知道是否可以""有没有更好的方式""考虑一下"
  - 🇺🇸 "maybe we could" "I wonder if" "is there a better way" "what if we" "consider" "perhaps"
  - 🇯🇵 "もしかして""こうしたらどうかな""もっといい方法はないかな""考えてみて"
  - 🇰🇷 "혹시" "이렇게 하면 어떨까" "더 좋은 방법 없을까" "생각해봐"

---

## Analysis Notes

1. **Holistic judgment**: Each dimension requires 3+ signals for a confident assessment
2. **Recency bias**: More recent messages carry more weight (personality evolves)
3. **Language-agnostic**: Based on semantic intent matching, not limited to any language. Keywords above cover zh/en/ja/ko/es/fr/de, but the analysis engine should respond equally to equivalent expressions in any language
4. **Default to middle**: When signals are insufficient, score 50 (M) — do not force a judgment
5. **No speculation**: Only score based on observable text behavior, never speculate about the user's inner state
6. **Mixed languages**: Users may mix multiple languages within a single message; all language signals carry equal weight
7. **Universal behavior signals**: Beyond keyword matching, also detect language-agnostic behavioral patterns: message length, question mark frequency, topic-switching frequency, instruction vs discussion ratio, emoji/exclamation usage frequency, etc.
