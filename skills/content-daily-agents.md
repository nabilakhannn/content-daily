---
name: content-daily-agents
description: Multi-agent LinkedIn content pipeline. Orchestrates 5 subagents (scout → strategist → interviewer → writer → editor) sequentially. Invoke for "today's LinkedIn post (agent mode)", "run agent pipeline", "generate post with agents", "agent mode content". Higher quality than single-skill mode but uses 3-5x more tokens. Use for important posts, batch generation, or when single-skill output feels generic.
---

# Content Daily — Multi-Agent Orchestrator

This skill orchestrates 5 specialized subagents to produce a LinkedIn post. Each agent has a single job. Output of one feeds the next.

## When To Use This vs Single Skill

| Use single skill (`content-daily`) when | Use agents (`content-daily-agents`) when |
|------|------|
| Quick daily post | Important post (launch, lead magnet, big take) |
| Token cost matters | Quality matters more than cost |
| Single context fits whole flow | Want strict separation between research/voice/scan |
| Post is for warm audience | Post needs to convert cold audience |

## The 5-Agent Pipeline

```
SCOUT (Phase 0)
  ↓ research brief
STRATEGIST (Phase 1)
  ↓ 3 topic options → user picks
INTERVIEWER (Phase 2)
  ↓ 5 POV questions → POV brief
WRITER (Phase 3a-c)
  ↓ 7-layer draft + 3 alt hooks
EDITOR (Phase 3d)
  ↓ 12-point red-flag scan → GREENLIT or REWRITE
USER (final review)
```

## Orchestration Steps

### Step 0 — Pre-flight check

Read these files. If any missing, abort with clear error:
- `~/content-system/positioning.md`
- `~/content-system/voice-card.md`
- `~/content-system/swipe-hooks.md`
- `~/content-system/posts-log.md` (create empty if missing)
- `~/content-system/writing-sop.md`

If positioning.md or voice-card.md is the unfilled template, abort with:
```
ABORT: positioning.md or voice-card.md not filled out.
Fill them at ~/content-system/ before running the agent pipeline.
```

### Step 1 — Dispatch Scout

Use the Task tool with `subagent_type: scout`. Pass:
- User's request (single or batch)
- Today's date

Wait for scout to return RESEARCH BRIEF.

### Step 2 — Dispatch Strategist

Use the Task tool with `subagent_type: strategist`. Pass:
- Scout's research brief
- Today's day of week (for pillar rotation)

Strategist returns 3 topic options. Show options to user. Wait for user pick.

### Step 3 — Dispatch Interviewer

Use the Task tool with `subagent_type: interviewer`. Pass:
- Selected topic from user
- Pillar from strategist

Interviewer asks 5 questions one at a time. Pushes back on weak answers. Returns POV BRIEF.

**Note:** Interviewer interactions are user-facing. Run synchronously (foreground), not in background.

### Step 4 — Dispatch Writer

Use the Task tool with `subagent_type: writer`. Pass:
- POV brief from interviewer
- Topic + pillar + hook angle from strategist

Writer returns full 7-layer draft + 3 alt hooks + image prompt.

### Step 5 — Dispatch Editor

Use the Task tool with `subagent_type: editor`. Pass:
- Writer's draft
- All 3 alt hooks

Editor scans 12 points. Returns GREENLIT or REWRITE APPLIED.

If editor returns `EDITOR ABORT`, restart from Step 3 (Interviewer) — POV is too weak.

### Step 6 — Present to user

Format final output:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
YOUR POST (Agent Pipeline)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Final post copy from editor]

━━━━━━━━━━━━━━━━━━
PIPELINE TRACE
━━━━━━━━━━━━━━━━━━
Scout: [N candidate angles]
Strategist: User picked option [1/2/3]
Interviewer: 5/5 POV answers extracted
Writer: [archetype] / [hook type] / [word count]
Editor: 12/12 scan PASS [or X rewrites applied]

━━━━━━━━━━━━━━━━━━
ALTERNATE HOOKS
━━━━━━━━━━━━━━━━━━
1. [Alt 1]
2. [Alt 2]
3. [Alt 3]

━━━━━━━━━━━━━━━━━━
IMAGE PROMPT
━━━━━━━━━━━━━━━━━━
[Brief or "skip"]

━━━━━━━━━━━━━━━━━━
POSTING CHECKLIST
━━━━━━━━━━━━━━━━━━
- [ ] Post live (never schedule)
- [ ] Stay first 30 min
- [ ] Reply to every comment
- [ ] Comment on 3 ICP posts
- [ ] DM substantive commenters
```

### Step 7 — Log to posts-log.md

Append entry to `~/content-system/posts-log.md`:

```
## [Today's date] — [Pillar] | [Framework] | [Hook Type] | AGENT MODE
**Hook:** [first 1-2 lines]
**Link:** [fill after posting]
**Pillar:** [Broad TAM / Niche ICP / Authority]
**Framework:** [archetype]
**Hook type:** [pattern used]
**Performance (72h):** [fill in]
**Pipeline:** scout → strategist → interviewer → writer → editor
**Editor scans applied:** [count]
**Notes:** Generated via content-daily-agents.
```

## Hard Rules

1. Always run pre-flight check first. Missing files = abort.
2. Each agent must complete before next starts. No parallel.
3. If user takes >10 min between phases, save state by writing intermediate brief to `~/content-system/.draft-state.md` so user can resume.
4. NEVER bypass editor. Even on user request.
5. If editor fails 3 rewrites, restart from interviewer (don't just patch).
6. Log every run to posts-log.md, even if user doesn't end up posting.

## Cost Note (be honest with user)

This pipeline uses 5 separate agent contexts. Token cost is roughly 3-5x higher than single-skill mode. For daily posts, single skill is enough. Use agents for high-stakes posts only.
