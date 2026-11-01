---
name: multipublish-video
description: >-
  Use when the user wants a finished video uploaded, drafted, scheduled, or
  published to Bilibili / Xiaohongshu / Douyin / YouTube (视频号 only if named) via
  Ego Lite on their Mac. Not for making or editing videos.
---
# Multipublish video

## When
A finished video (usually `~/Movies/剪映导出/<完整标题>/`) needs upload/draft/schedule/publish. Not for editing, covers, scripts (→ video-production), 图文 (→ multipublish-tuwen), 公众号 (→ 公众号 assistant).

## Source of truth (read on the user's Mac first)
- `~/git_pro/VideoPilot/.agents/skills/videopilot/references/publishing.md` (per-platform notes, newest wins)
- `.../references/preferences.md` (交付与归档 section)
- `~/.codex/skills/video-publisher/SKILL.md` + references (config, intake-workflow, content-package, cover-workflow)
- `~/.codex/skills/ego-browser/SKILL.md`
- Per-video `videos/<…>/publication.md` for resumed jobs

## Defaults (confirmed, don't re-ask)
1. Browser: **Ego only** (replaces old Chrome default).
2. Platforms unspecified → **B站, 小红书, 抖音, YouTube**. 视频号 only when named this time; 露脸/口播 videos normally not to 视频号. X is not a video target.
3. **One upload at a time globally** (old background uploads count). Wait for real 上传完成/receipt, not just 100%.
4. Covers: check export folder AND `~/Pictures/视频封面/`; match by title + real size. Prefer the 剪映-exported SRT; upload where supported and verify.
5. Originality: default 原创/自制 (user's standing confirmation), unless the user says otherwise for this video. AI/自主创作声明 default「无需声明」. Don't mention AI cover in 简介.
6. **B站 every time**: 更多设置 → 高级设置 → tick 杜比音效 + Hi-Res无损音质, read back checked state. Script READY doesn't cover this.
7. Default stop = verified draft before final button. Publish/schedule only on explicit request for this video × platforms.
8. Scheduling = platform **native** scheduler only. Never Codex/WorkBuddy cron, heartbeat, reminders, or "start upload at time T". If 08:11 isn't selectable, use 08:10 same day without asking. Ambiguous relative dates across midnight → confirm exact date/time/zone. Target time passed → ask for new time.
9. Location prompts → 不允许 (only location).
10. 小红书 title weighted length ≤ 20 (ASCII 0.5); 诺奖 suffix may drop, keep #诺奖专题 tag.
11. Never touch Clash Verge proxy/network to speed uploads; report and let the user decide.

## Steps
1. `node scripts/config.mjs status` in video-publisher; finish onboarding if required.
2. Confirm exact video, platforms, title/tags, covers, draft vs publish vs native schedule (inherit what's already clear).
3. Write content package JSON outside the skill folder.
4. Run `scripts/run-safe-platforms.sh <package.json> [suffix] [platform...]`; hand-drive with Ego only for missing steps (B站 音质, scheduling, final publish).
5. Final branch (when authorized): submit once; on timeout read dialog/list before retrying.
6. Report per platform honestly: uploaded / draft READY / scheduled (date+time+zone) / under review / public, with receipt evidence.
7. Resumed batches: find the original draft (title/duration/cover/ID), continue it, never re-upload; verify each video × platform for no duplicates/misses.
8. Close finished task tabs; keep tabs still uploading or needing review; never close user's other tabs.

## Platform gotchas (re-read page; UI changes)
- **B站**: upload button may not open picker → `setInputFiles` on `input[name=buploader][accept*=".mp4"]`. 分区 single dropdown (e.g. 知识). 4:3 and 16:9 share one image input; confirm selected canvas before upload. Scheduler minutes in 5-min steps. "内容无需标注" + "内容为自制" may coexist; that's normal. Evidence: 稿件投递成功 + 稿件处理 status.
- **小红书**: cover via 设置封面 → 裁剪 → 3:4. 定时 input accepts `YYYY-MM-DD HH:MM`; 定时发布 button inside shadow DOM (use snapshot ref / scroll). Evidence: 发布成功 + 笔记管理.
- **抖音**: horizontal cover 4:3, vertical 3:4. Schedule `input[placeholder="日期和时间"]`, window 2 h–14 days. "检测人数过多" = busy, not penalty. Evidence: 发布成功 + 内容管理.
- **YouTube**: 安排时间 collapsed under 公开范围; time via `tp-yt-paper-input`. Scheduling before upload/processing finishes may only save a draft; verify final 预定 receipt + same-ID record. Verify thumbnail via `i9.ytimg.com/vi_webp/<id>/mqdefault`. Don't re-encode to speed upload.
- **视频号** (only when named): new space often needs user QR login. Fields inside wujie shadow DOM. Short title ≤ 16 chars; a comma was rejected once (use space). Cover editable only after upload completes. 视频标注 → 无需标注.
- **Ego**: a task space can expire after long waits; don't retry/self-claim. When the user says continue, `claimTaskSpace(<spaceId>)` the original space.

## Hard stops
- No silent extra platforms (especially 视频号).
- No "published/scheduled" claims without UI receipt and same-ID list status.
- No replacing/transcoding/cropping user files silently.
- No re-upload to fake a source swap on published content.
- No automation timers as publish clock; no proxy changes; no credential reads.
