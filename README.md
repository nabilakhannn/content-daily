# Content Daily

> 5 AI agents. One LinkedIn post. Zero AI slop.

A Claude Code system that runs your LinkedIn content through a rigid 5-phase pipeline. No more generic ChatGPT posts. The system researches what's trending, extracts YOUR opinion through 5 sharp questions, then writes in your voice using a 7-layer framework. Auto-scans for AI red flags before showing you the draft.

**Two modes available:**
- **Single skill mode** (`content-daily`) — All 5 phases run in one context. Cheap. Fast. Good for daily posts.
- **Multi-agent mode** (`content-daily-agents`) — 5 separate Claude Code subagents handle each phase. Higher quality. 3-5x more tokens. Use for big launches and high-stakes posts.

Install one or both. Pick which to run per post.

---

## The 5 Agents

```
  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
  │             │    │             │    │             │    │             │    │             │
  │   ▄█████▄   │    │    ▄███▄    │    │   ▄█▀ ▀█▄   │    │   ▄█████▄   │    │    ▄███▄    │
  │   █ ▄ ▄ █   │    │   █ ◉ ◉ █   │    │   █ ◉ ◉ █   │    │   █ ▀ ▀ █   │    │   █ ✕ ✕ █   │
  │   █  ▼  █   │    │   █  ▼  █   │    │   █  ◯  █   │    │   █  ▽  █   │    │   █  ━  █   │
  │   ▀█████▀   │    │    ▀█▄█▀    │    │    ▀█▄█▀    │    │   ▀█████▀   │    │    ▀█▄█▀    │
  │   ▌█ █ █▐   │    │   ▌▒ ▒ ▒▐   │    │   ▌█▒█▒█▐   │    │   ▌█ █ █▐   │    │   ▌█▓█▓█▐   │
  │   ▀█▀ ▀█▀   │    │   ▀█▀ ▀█▀   │    │   ▀█▀ ▀█▀   │    │   ▀█▀ ▀█▀   │    │   ▀█▀ ▀█▀   │
  │             │    │             │    │             │    │             │    │             │
  │   SCOUT     │    │  STRATEGIST │    │ INTERVIEWER │    │   WRITER    │    │   EDITOR    │
  │             │    │             │    │             │    │             │    │             │
  │  Research   │    │ Pick topic  │    │  5 Q's POV  │    │  7 layers   │    │ Red-flag    │
  │  trending   │    │  + hook     │    │  extract    │    │  draft      │    │ scan        │
  │  topics     │    │  angle      │    │  opinion    │    │             │    │ + alts      │
  └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
        │                   │                   │                   │                   │
        ▼                   ▼                   ▼                   ▼                   ▼
     PHASE 0            PHASE 1            PHASE 2            PHASE 3            PHASE 3d
```

---

## How It Works

```mermaid
flowchart LR
    A[You: today's LinkedIn post] --> B[SCOUT 🔍]
    B --> |Trends + Positioning + Swipe + Log| C[STRATEGIST 🎯]
    C --> |3 topic options| D{You pick}
    D --> E[INTERVIEWER 🎤]
    E --> |5 POV questions| F[WRITER ✍️]
    F --> |7-layer draft| G[EDITOR 🛡️]
    G --> |Red-flag scan| H{Pass?}
    H --> |No| F
    H --> |Yes| I[Final post + 3 alt hooks + image prompt]
    I --> J[Logged to posts-log.md]
```

---

## What You Get

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
YOUR POST
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Final post copy in YOUR voice — paste-ready]

━━━━━━━━━━━━━━━━━━
STRUCTURE NOTES
━━━━━━━━━━━━━━━━━━
Archetype: Contrarian Truth
Hook type: Shock/Contradiction
Target: ICP
Pillar: Authority
Length: 920 words

━━━━━━━━━━━━━━━━━━
ALTERNATE HOOKS
━━━━━━━━━━━━━━━━━━
1. [Different pattern]
2. [Different pattern]
3. [Different pattern]

━━━━━━━━━━━━━━━━━━
POSTING CHECKLIST
━━━━━━━━━━━━━━━━━━
- [ ] Post live (never schedule)
- [ ] Stay first 30 min
- [ ] Reply to every comment
- [ ] Comment on 3 ICP posts
- [ ] DM substantive commenters
```

---

## What Makes It Different

| Generic AI tool | Content Daily |
|-----------------|---------------|
| Writes from a prompt | Researches trends + your positioning + your hook history first |
| Sounds like ChatGPT | Reads your voice card + writes in YOUR style |
| Generic hooks | 21+ hook templates, never repeats one from last 30 days |
| Slop-prone | Mandatory red-flag scan before output (em dashes, stock phrases, triplets, sycophantic openers) |
| One-shot | Logs every post for performance tracking |
| No memory | Auto-checks posts-log to avoid repeating topics + hooks |

---

## Install (3 minutes)

### Requirements
- Claude Code installed → https://claude.com/claude-code
- 30 minutes to fill out 2 templates (positioning + voice card)

### Steps — Single Skill Mode (recommended for most users)

```bash
# 1. Create your content system folder
mkdir -p ~/content-system

# 2. Drop the 5 templates in
cp templates/* ~/content-system/

# 3. Install the skill
mkdir -p ~/.claude/skills/content-daily
cp SKILL.md ~/.claude/skills/content-daily/SKILL.md
```

Trigger: `today's LinkedIn post`

### Steps — Multi-Agent Mode (optional, for high-stakes posts)

After single skill install, also run:

```bash
# 1. Install the orchestrator skill
mkdir -p ~/.claude/skills/content-daily-agents
cp skills/content-daily-agents.md ~/.claude/skills/content-daily-agents/SKILL.md

# 2. Install the 5 subagents
mkdir -p ~/.claude/agents
cp agents/*.md ~/.claude/agents/
```

Trigger: `run agent pipeline` or `today's LinkedIn post (agent mode)`

Both modes share the same `~/content-system/` folder. Voice card, positioning, swipe file, and posts log work for both.

### Fill out the 2 templates that matter

```
~/content-system/
├── positioning.md   ← FILL THIS (5 min — niche, ICP, pillars, enemy)
├── voice-card.md    ← FILL THIS (30 min — 12 questions about your style)
├── swipe-hooks.md   ← works as-is
├── posts-log.md     ← empty, fills as you post
└── writing-sop.md   ← works as-is
```

### Test it

Open Claude Code anywhere. Type:

```
today's LinkedIn post
```

Skill fires. Walks you through the 5 phases. Drops final post + alt hooks + checklist.

---

## File Structure

```
content-daily/
├── SKILL.md                    ← Single-skill 5-phase pipeline (single-skill mode)
├── SETUP.md                    ← Detailed install guide
├── README.md                   ← This file
├── templates/                  ← User config (copy to ~/content-system/)
│   ├── positioning.md          ← Your niche, ICP, IFP, 3 pillars, enemy
│   ├── voice-card.md           ← 12 questions that define your voice
│   ├── swipe-hooks.md          ← 7 archetypes + 21 templates + anti-patterns
│   ├── posts-log.md            ← Append-only memory of every post
│   └── writing-sop.md          ← 7-layer framework + red-flag scanner
├── skills/                     ← Multi-agent mode orchestrator
│   └── content-daily-agents.md ← Skill that fires the 5 subagents
└── agents/                     ← Multi-agent mode subagents (copy to ~/.claude/agents/)
    ├── scout.md                ← Phase 0 research agent
    ├── strategist.md           ← Phase 1 topic picker
    ├── interviewer.md          ← Phase 2 POV extractor
    ├── writer.md               ← Phase 3 drafter
    └── editor.md               ← Phase 3d 12-point red-flag scanner
```

## Two Modes Compared

| Feature | Single Skill | Multi-Agent |
|---------|--------------|-------------|
| Install command | 1 file copy | 7 file copies |
| Token cost per post | 1x | 3-5x |
| Speed | Faster (single context) | Slower (sequential agents) |
| Quality | High | Higher (strict separation) |
| Context isolation | All 5 phases share context | Each agent has own context |
| Pushback strength | Medium | Stronger (interviewer dedicated) |
| Red-flag scan | Same scan, single pass | Dedicated editor agent, can rewrite-and-rescan up to 3 times |
| Best for | Daily posts | Launches, lead magnets, high-stakes posts, batch generation |
| Trigger | `today's LinkedIn post` | `run agent pipeline` |

---

## The 7 Layers (every post follows this)

```
LAYER 1  ▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░  Hook        (1-2 lines, max 12 words/line)
LAYER 2  ░░▓▓▓▓▓▓▓▓░░░░░░░░░░  Context     (under 80 words, ONE moment)
LAYER 3  ░░░░▓▓▓▓▓▓▓▓▓▓▓▓░░░░  Emotion     (150-200 words, sensory)
LAYER 4  ░░░░░░░░▓▓▓▓▓▓▓▓▓▓░░  Value       (150-200 words, your POV)
LAYER 5  ░░░░░░░░░░░░▓▓▓▓░░░░  Rehook      (~50 words at 60% mark)
LAYER 6  ░░░░░░░░░░░░░░░░▓▓▓▓  CTA         (20-40 words, open question)
LAYER 7  ░▓░▓░▓░▓░▓░▓░▓░▓░▓░  Format      (whitespace + flow)
```

---

## The Red-Flag Scan (banned in every post)

```
✗  Em dashes (—)
✗  "It's not about X, it's about Y."
✗  Triplet endings: "Same X. Same Y. Same Z."
✗  Stock corporate words: revolutionary, game-changing, skyrocket, leverage, dive deep
✗  Sycophantic openers: "Great question," "Love this"
✗  Lists always exactly 3 items (vary the count)
✗  Zero contractions (humans use don't/can't/won't)
✗  Zero hedging ("kinda", "I think", "honestly")
```

If any present → skill rewrites + rescans before showing you anything.

---

## Cost

Free. Runs inside your Claude Code subscription. No external APIs, no per-post charges.

---

## Troubleshooting

**Skill doesn't fire?**
- Confirm `~/.claude/skills/content-daily/SKILL.md` exists
- Restart Claude Code
- Try `/content-daily` directly

**Posts feel generic?**
- Voice card is the engine. Spend 30 min filling it properly.
- Add a real sample post you wrote (Q5 of voice-card.md)
- Add an anti-sample (Q6) — what NOT to sound like

**"positioning.md not found"?**
- Run: `ls ~/content-system/` — should show 5 files
- Folder must be `content-system` (lowercase, hyphen)

---

## What This Won't Do

- Schedule posts to LinkedIn (post manually — this is generation only)
- Generate images (use Midjourney/Higgsfield/etc separately)
- Replace your judgment (always read + edit before posting)

---

## License

MIT — fork, modify, ship. Just keep your voice card private (it's your moat).
