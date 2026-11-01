---
name: multipublish-video
description: >-
  Use when the user wants an exported VideoPilot video uploaded, drafted,
  scheduled, or published to Bilibili / Xiaohongshu / Douyin / YouTube (Channels
  only if named) via Ego Lite on their Mac.
---
# Multipublish video

## When
User has a finished video (usually in `~/Movies/剪映导出/<完整标题>/`) and wants it uploaded, drafted, scheduled, or published. Not for editing, making covers, writing 科技日报, or 图文 posts (use multipublish-tuwen).

## Source of truth (read on the user's Mac first)
- `~/git_pro/VideoPilot/.agents/skills/videopilot/SKILL.md`
- `.../references/publishing.md`
- `.../references/preferences.md`
- `~/.codex/skills/video-publisher/SKILL.md` and its references (production entry, config check, content package, READY semantics)
- `~/.codex/skills/ego-browser/SKILL.md`

## Defaults
1. Browser: **Ego Lite only**.
2. Platforms when not specified: **B站, 小红书, 抖音, YouTube**. 视频号 only if named this time. X is not a default video target.
3. **One upload at a time globally**; wait for real upload completion before the next.
4. Before upload, check both the export folder and `~/Pictures/视频封面/`; reuse matching 16:9 / 4:3 / 3:4 covers. Upload the matching SRT when the platform supports it.
5. **B站**: expand 更多设置 and verify 杜比音效 + Hi-Res无损音质 every time; script READY does not cover these.
6. Default stop: verified draft before the final publish button. Only press publish / schedule when the user explicitly asks for this video on these platforms.
7. Scheduling uses each platform's **native** scheduler only. Never Codex/WorkBuddy cron, heartbeat, or polling as the publish clock.
8. Location permission prompts: choose 不允许.
9. Originality checkbox only if config says all videos are original or the user confirms for this video.
10. Xiaohongshu title weighted length ≤ 20 (ASCII = 0.5).

## Steps
1. Run video-publisher config status; if onboarding required, finish config first.
2. Confirm exact video path, platforms, title/tags, cover choice, draft vs publish vs native schedule (skip what's already clear this task).
3. Write the content package JSON outside the skill folder.
4. Run the maintained production entry (`scripts/run-safe-platforms.sh`) rather than hand-driving creator pages, unless it lacks a needed step; then follow the platform notes in VideoPilot publishing.md with Ego.
5. Report each platform with an honest status: uploaded, draft READY, scheduled, under review, or public. Keep evidence.
6. Verify per video × platform for duplicates on resumed batches; close finished Ego tabs, keep ones still uploading or needing review.

## Hard stops
- No silent extra platforms (especially 视频号).
- No claiming published without UI receipt.
- No replacing/transcoding user files silently.
- No re-upload to fake a source swap on already-published content.
