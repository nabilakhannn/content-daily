# content-daily

> 6 AI agents. One LinkedIn post. Posts in your voice every time.

A Claude Code skill that runs your LinkedIn content through a 6-phase pipeline. The system sets itself up on first run, researches what is trending in your niche, extracts your real opinion through 5 sharp questions, writes in your voice using a proven 7-layer framework, checks the post against 6 strategy rules, and gives you a ready-to-use image prompt before you ever see the draft.

---

## The 6 Agents

```
  SCOUT        STRATEGIST   INTERVIEWER    WRITER       STRATEGY QA   IMAGE AGENT
  ─────        ──────────   ───────────    ──────       ───────────   ───────────
  Reads your   Picks 3      Asks 5         Writes       6 checks.     Picks format.
  files.       topic        questions.     7-layer      Scores post.  Writes your
  Finds what   options.     Extracts       draft from   Explains why  image prompt.
  is trending  You pick 1.  your real      your         it should
  right now.               opinion.       answers.     perform.
  
  PHASE 0      PHASE 1      PHASE 2        PHASE 3      PHASE 5       PHASE 6
  AUTO         YOU PICK     YOU ANSWER     AUTO         AUTO          AUTO
```

---

## How It Works

```mermaid
flowchart LR
    A[/content-daily] --> B[Scout reads your files + finds trending topics]
    B --> C[Strategist shows 3 topic options]
    C --> D{You pick one}
    D --> E[Interviewer asks 5 questions one at a time]
    E --> F[Writer builds 7-layer post from your answers]
    F --> G[Editor scans for AI red flags]
    G --> H[Strategy QA runs 6 checks]
    H --> I[Post shown to you with strategy card]
    I --> J[Image Agent picks format and writes prompt]
    J --> K[Logged to posts-log.md]
    K --> L[3 next post ideas suggested]
```

Green phases run automatically. You only pick a topic and answer 5 questions.

---

## What You Get From Every Post

```
YOUR POST
─────────────────────────────────────────
[Final post in your voice. Paste-ready.]

STRATEGY QA CARD
─────────────────────────────────────────
Pillar rotation:    right pillar this week
ICP/IFP balance:    not too many buyer posts
TAM broad post:     one went out this week
Hook freshness:     not repeated in 30 days
Positioning fit:    reinforces authority
Monthly mix:        4-3-2-1 on track

WHY THIS POST SHOULD PERFORM
─────────────────────────────────────────
Hook type: Contrarian. Triggers disagreement reflex.
Emotional lead: Frustration. Moves your ICP.
Broad-to-narrow: Opens wide, narrows to your niche.

3 ALTERNATE HOOKS
─────────────────────────────────────────
1. [Contrarian angle]
2. [Story start]
3. [Data proof]

IMAGE PROMPT
─────────────────────────────────────────
Format: Text Poster
[Ready-to-paste prompt for your image tool]

NEXT 3 POST IDEAS
─────────────────────────────────────────
1. [Idea — Pillar, audience, hook type]
2. [Idea — Pillar, audience, hook type]
3. [Idea — Pillar, audience, hook type]
```

---

## Install (2 minutes)

### Requirements

- Claude Code installed: https://claude.ai/download

### Steps

```bash
# 1. Install the skill
mkdir -p ~/.claude/skills/content-daily
cp SKILL.md ~/.claude/skills/content-daily/SKILL.md
```

That is it. Open Claude Code anywhere and type:

```
/content-daily
```

On first run, the skill walks you through the full setup automatically. It will create your content-system folder, help you install Obsidian, install the Web Clipper browser extension, and fill in your positioning and voice files. It only does this once.

---

## What the Setup Wizard Creates

```
~/content-system/
├── positioning.md     ← Your niche, ICP, IFP, 3 pillars, enemy
├── voice-card.md      ← 12 questions that define your tone and style
├── writing-sop.md     ← Post structure rules (auto-updates from your data)
├── swipe-hooks.md     ← Hook patterns, starred when they perform well
├── posts-log.md       ← Every post logged (no repeats in 30 days)
└── swipe-images/      ← Visual inspiration clipped from LinkedIn
```

You fill in positioning and voice once. Every other file updates itself as you work.

---

## The System Gets Smarter Every Week

**After every post:** date, pillar, hook type, and framework logged automatically.

**After 72 hours:** paste your likes and impressions. Top hooks get starred. Patterns update your writing rules after 3 data points.

**When you push back on a draft:** say "this doesn't sound like me." Voice card updates so that mistake never repeats.

**When you clip a post you liked:** click Obsidian Web Clipper. Saved to swipe-images. Scout reads it next time as visual inspiration.

---

## The 7 Layers (every post follows this)

```
LAYER 1  Hook        1-2 lines. Stops the scroll. Max 12 words per line.
LAYER 2  Context     Under 80 words. The specific moment it happened.
LAYER 3  Emotion     150-200 words. What you felt. Sensory details.
LAYER 4  Value       150-200 words. Your POV. Common belief vs real truth.
LAYER 5  Rehook      50 words at 60% mark. Pulls reader back in.
LAYER 6  CTA         20-40 words. One open question. Matches the post energy.
LAYER 7  Format      Paragraphs under 40 words. Whitespace. No full stops at line ends.
```

---

## The Red-Flag Scan (runs before you see anything)

```
No em dashes
No "it is not about X, it is about Y" structure
No triplet endings: "Same X. Same Y. Same Z."
No stock words: revolutionary, game-changing, leverage, dive deep
No sycophantic openers: "Great question," "Love this"
No lists always exactly 3 items
No zero contractions (humans use don't/can't/won't)
```

If any of these appear, the skill rewrites and rescans before showing you the post.

---

## The 6 Strategy Checks (Phase 5 QA)

```
1. Pillar rotation        Not repeating the same pillar 3x in a row
2. ICP vs IFP balance     Mix of buyer posts and reach posts
3. TAM broad post         At least one broad reach post per week
4. Hook freshness         No hook type repeated in last 30 days
5. Positioning fit        Post reinforces your authority angle
6. Monthly mix            4-3-2-1 post type variety across the month
```

---

## What Makes It Different

| Generic AI tool | content-daily |
|----------------|---------------|
| Writes from a prompt | Reads your positioning, voice, and hook history first |
| Sounds like ChatGPT | Extracts your actual opinion through 5 sharp questions |
| Generic hooks | Proven hook templates, never repeats one from last 30 days |
| No strategy | 6 QA checks run before you see the draft |
| No image step | Image Agent picks a format and writes your prompt |
| No memory | Logs every post, updates writing rules from performance data |
| Setup takes hours | First-run wizard sets everything up in 5 minutes |

---

## Cost

Free. Runs inside your Claude Code subscription. No external APIs. No per-post charges.

---

## Troubleshooting

**Skill does not fire?**
- Confirm `~/.claude/skills/content-daily/SKILL.md` exists
- Restart Claude Code
- Type `/content-daily` directly

**Posts feel generic?**
- Voice card is the engine. Spend 30 minutes filling it out properly.
- Add a real sample post you wrote (Q5 of voice-card.md)
- Add an anti-sample (Q6) showing what NOT to sound like

**positioning.md not found?**
- Run: `ls ~/content-system/` to confirm the folder and files exist
- Folder must be exactly `content-system` (lowercase, hyphen)

---

## File Structure

```
content-daily/
├── SKILL.md          The 6-phase pipeline skill
├── README.md         This file
├── SETUP.md          Detailed manual setup guide (if you prefer not to use the wizard)
└── templates/        Starter templates (wizard creates these automatically)
    ├── positioning.md
    ├── voice-card.md
    ├── writing-sop.md
    ├── swipe-hooks.md
    └── posts-log.md
```

---

## License

CC BY-NC-SA 4.0 — use it, teach it, adapt it. Keep your voice card private. That is your moat.
