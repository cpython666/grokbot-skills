---
name: multipublish-tuwen
description: >-
  Use when the user wants to publish 图文 (images + caption) now or on a
  platform-native schedule to Bilibili / X / Xiaohongshu / Douyin image posts
  via Ego Lite on their Mac. Not for 公众号 (WeChat Official Account) and not for
  video.
---
# Multipublish 图文

## When
User hands images + text (or a ready caption) and wants realtime or scheduled social 图文 posts. Not for long video uploads, not for writing 科技日报, not for 公众号 articles/drafts (that workstream belongs to the 公众号/日报 assistant; the user scans to publish), not for inventing Codex/WorkBuddy cron as a publish timer.

## Source of truth (read these first on the user's Mac)
- `~/git_pro/WechatPilot/.agents/skills/wechatpilot/SKILL.md`
- `.../references/preferences.md`
- `.../references/multiplatform.md`
- `.../references/workflow.md`
- Per-platform: `.../references/{bilibili,x,xiaohongshu,douyin}-platform.md`
- Browser: `~/.codex/skills/ego-browser/SKILL.md` (or Ego Lite app ego-skills copy)

Do **not** merge or follow `video-publisher` / VideoPilot video upload skills for this path.

## Defaults
1. Browser: **Ego Lite only** for publish UI (not Chrome as default).
2. Platforms when user does not specify: B站多图动态 → X → 小红书. Include 抖音图文+配乐 only if authorized for sync **and** the user did not say「抖音不发」.
3. Accounts (verify live UI): X ≈ 星梦 `@stardreamfly`; B站/小红书/抖音 ≈ SI斗罗.
4. 公众号 is out of scope: if asked, say it is handled by the 公众号 assistant and stop.
5. Timing: realtime if they say 实时/现在发; otherwise use each platform’s **native** scheduler. Stagger themes 1–2h with random minutes; Douyin needs ~2h minimum — bump later if needed. Never use Codex/WorkBuddy/heartbeat as the publish clock.

## Steps
1. Confirm this time's platforms + realtime vs native schedule in one short check (skip if already crystal clear).
2. Privacy/redact pass on images and caption before any upload.
3. Build or update a `publish-package.json` (or project equivalent) for this drop: assets, caption, platforms, excluded, schedule.
4. Load ego-browser skill; one Ego task space per platform; upload via measured file-chooser APIs from the platform refs.
5. Publish or native-schedule; capture evidence (URL / success UI / schedule time).
6. Append `~/git_pro/WechatPilot/templates/publication.md`-style log entry.
7. Close spare Ego tabs.

## Hard stops
- No video READY/upload flows from VideoPilot.
- No 公众号 drafting or publishing.
- No silent Douyin when user excluded it.
- No fabricating engagement or “posted” without UI evidence.
