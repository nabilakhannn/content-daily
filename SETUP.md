# Content Daily Skill — Setup Guide

3 minutes. One-time. Then trigger with "today's LinkedIn post" forever.

## What You're Installing

A 5-phase LinkedIn content pipeline that runs inside Claude Code:
1. Researches what's trending in your niche
2. Picks topic options based on your positioning
3. Asks 5 POV questions to extract YOUR opinion (not generic AI)
4. Writes the post in your voice using the 7-layer framework
5. Logs it for performance tracking

## Requirements

- Claude Code installed (https://claude.com/claude-code)
- 5 minutes to fill out 2 templates (positioning + voice card)

## Step 1 — Create the content system folder

Open Terminal:

```bash
mkdir -p ~/content-system
```

## Step 2 — Drop the 5 templates inside

Copy these files from this share folder into `~/content-system/`:
- `positioning.md`
- `voice-card.md`
- `swipe-hooks.md`
- `posts-log.md`
- `writing-sop.md`

Or run from this folder:

```bash
cp templates/* ~/content-system/
```

## Step 3 — Install the skill

```bash
mkdir -p ~/.claude/skills/content-daily
cp SKILL.md ~/.claude/skills/content-daily/SKILL.md
```

## Step 4 — Fill out the 2 templates that matter

Open these and fill them in (15 min total):

### `~/content-system/positioning.md`
Your niche, ICP (who pays you), IFP (who follows you but cant pay yet), 3 content pillars, your unfair advantage, your enemy.

### `~/content-system/voice-card.md`
12 questions about how you write, talk, and think. Skill uses this to mimic your voice instead of sounding like ChatGPT.

The other 3 (`swipe-hooks.md`, `posts-log.md`, `writing-sop.md`) work as-is. Don't edit unless you want to.

## Step 5 — Test it

Open Claude Code in any folder. Type:

```
today's LinkedIn post
```

Skill should fire. If it doesn't, restart Claude Code (close + reopen).

## Troubleshooting

**Skill doesn't fire?**
- Confirm the SKILL.md sits at `~/.claude/skills/content-daily/SKILL.md`
- Restart Claude Code
- Try: `/content-daily` directly

**It says "positioning.md not found"?**
- Confirm folder spelled `content-system` (not `content_system` or `Content-System`)
- Confirm you copied templates to `~/content-system/` not somewhere else
- Run: `ls ~/content-system/` — should show 5 files

**Posts feel generic?**
- Voice card is the engine. Spend 30 min filling it out properly. Bad voice card = generic post.

## What This Won't Do

- Schedule posts to LinkedIn (post manually, this is content gen only)
- Generate images (use a separate tool like Midjourney/Higgsfield)
- Replace your judgment (always read + edit before posting)

## Cost

Free. Runs inside your existing Claude Code subscription. No external APIs.
