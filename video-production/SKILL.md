---
name: video-production
description: >-
  Use when the user gives a topic, inspiration, raw footage, or says
  做个视频/做封面/改片/剪口播/做宣传片 and wants a finished video made (topic → script → edit →
  export → covers), not uploaded or published.
---
# Video production

## When
Making or revising a video: synthesized no-narration explainer/promo (合成片), 口播精剪 of user footage, or covers. Not for upload/publish (→ multipublish-video), 图文 (→ multipublish-tuwen), 公众号 (→ 公众号 assistant).

## Source of truth (read on the user's Mac first; newer confirmed rules win)
- `~/git_pro/xingxiang/SKILL.md` + `references/{visual-language,render-routes,music-timing,render-delivery,provenance}.md` — 星象: the user's own base method (no-narration, picture-tells-story, render routes)
- `~/.claude/skills/video-studio/SKILL.md` — refined method built on 星象 (anti-PPT, BGM, QA, covers)
- `~/git_pro/VideoPilot/.agents/skills/videopilot/SKILL.md` and `references/{preferences,lessons,production,talking-head-editing,toolkit,video-skills}.md`
- `~/git_pro/VideoPilot/videos/INDEX.md` + retro.md of 1–2 recent similar videos
- Past Claude chats (read-only): `~/Library/Application Support/ChatHistoryVault/backup/records/*-claude/<id>/dialogue.jsonl`
Precedence: preferences.md (dated) > video-studio > xingxiang defaults. E.g. xingxiang's "default 30 s / 9:16 for vertical" is superseded by 16:9 + unlimited length.

## Fixed rules (confirmed, don't re-ask)
1. Titles: list 3–5, mark ★, start with ★ immediately; revise on feedback. Style: 口语问句 + 情绪钩子 ("…是干嘛的？如何使用？", "一口气看懂…", reverse-intuition questions). If user says "标题由你决定/不设限", decide yourself and don't copy a previous video's title pattern. 诺奖: suffix「｜诺奖专题」, gold badge, #诺奖专题.
2. Picture 16:9 1920×1080 30fps; length = whatever explains it fully.
3. Sound: 合成片 = no narration/TTS/voice clone/lyrics; pure instrumental BGM; voices in source material not mixed in. 口播 = keep original voice.
4. Effort fits the task (按合适强度，不用最高档, 2026-10-22; replaces "always max effort").
5. Ask only questions that truly block; state assumptions and make a cheap sample. Don't turn each step into an approval gate.
6. Privacy: never read keys/tokens; demo data instead of heavy blur; label 演示数据/示意画面/本机实机画面.
7. Never touch Clash Verge proxy/network; read-only diagnosis only.
8. Reply briefly whenever the user messages mid-task, then continue.
9. Small doc/preference commits: don't push on your own.

## Topic selection
- User's niches: AI / 大模型 / 编程, 硬核黑科技解读, 原理科普 (chips, crypto, diffusion, physics/biology/诺奖), 软件讲解 (tools on their Mac), 游戏宣传/评析 (their own game, 王国保卫战).
- When asked "什么适合做视频": combine current hot news with these niches; prefer 硬核解读 with a counter-intuitive one-line thesis. Then 核实 → 收集素材 → 制作.
- Read the project knowledge base before pitching; the user rejected suggestions that ignored past preferences.
- Promo for own game: use the finished heroes/enemies as primary assets; bilingual 中英 short on-screen text OK when asked.

## #1 principle: 不要做成 PPT
Symptoms → redo: equal-length shots; fixed title+bullets layout; only fades/pop-ins; motion faked by constant pans/irrelevant particles; any frame looks like a slide.
Do: one core message → build one visual world/metaphor; each shot = one idea shown as motion, deformation, contrast, reveal, causality or spatial relation; make one frame work, then animate it; unified palette/type/material/motion language; shot length follows content & music; text secondary; ≥1 climax per chapter on a downbeat; motivated transitions. Structure: 动画钩子 → 标题揭示 → 因果正文 → 回扣点题. Intentional stillness is fine for reading.

## Workflow — 合成片
1. Read materials (originals), prefs, lessons, similar retros. Verify facts (official docs/repos/local state) → sources.md with fact boundaries; charts keep true data relationships.
2. Project dir `<title>/{assets/raw,assets/clean,assets/music,project,qa,outputs,renders,work}`; brief.md, storyboard.md (per shot: time/bars, single message, start→action→end composition, on-screen text + read window, transition, music cue, asset source).
3. Music structure first (BPM/bar grid, sections), then lock shots to phrases; reading time is the floor.
4. Sample: 1 still + 5–8 s clip with real text, BGM, one transition, on the FINAL renderer. Offer 2–3 still directions only if aesthetics are truly ambiguous.
5. Render route (pick, don't mix for show):
   - existing project/user-named tool first (Remotion, HyperFrames, Blender, own renderer);
   - DOM/SVG text/UI/charts → HyperFrames (Node 22+, FFmpeg; paused GSAP timeline calling `frame(t)`);
   - React project or Remotion named → `useCurrentFrame()` (check license: company >3 staff needs paid license);
   - Canvas/particles/textures → minimal renderer: headless Chromium, `renderFrame(t)`, pipe frames to FFmpeg;
   - 3D → Three.js (heavy materials: Blender); mechanism diagrams → Manim (`--fps 30`);
   - plain clip edits → FFmpeg directly.
   Deterministic: state = f(t), fixed seeds, no CSS anim/rAF/live clock/network; frame-addressed capture, never screen recording. Generative image/video = asset layer only; text, timing, compositing stay in code.
6. Low-res full preview → review narrative/text/music/seams → fix → 1080p → QA.

## BGM
- Original synth (fixed seed) or clearly licensed lyric-free track (log title/author/license/range).
- Must flow naturally (user: 「音乐是不是太跳脱的，没有自然连贯」): continuous motif and harmony, sections evolve, no jumpy switching.
- References: software 讲解 = bright pop chords + plucked arps + light drums, 100 BPM (approved); AI/励志 = D major 120 BPM cinematic electro-pop; 科普 = D minor 120 BPM. Choose per topic each time.
- Master 2-pass loudnorm −16 LUFS / −2 dBTP / 48 kHz; re-measure after AAC. Interlude −4~5 dB, not >7.
- If you cannot listen, say 「未试听」 and point the user to key timestamps.

## Workflow — 口播精剪
- Keep originals; local Buzz/Whisper word-level transcript.
- Keep spoken opening title; repeated takes → keep LATER complete take; physically remove false starts from audio-video; recheck all similar spots.
- Editable 剪映 project (source_timerange refs, editable subtitles); never overwrite user's native draft.
- Subtitles: 剪映收藏「快乐体」, 黑色填充 + 白色描边; verify in native UI.
- Cover set in 剪映 timeline 封面 slot; don't insert cover at video head. Export MP4 + same-version SRT natively.

## Software 讲解 assets
Use real screenshots from the user's Mac (`screencapture -x -o -l <windowID>`); browse only, cancel dialogs, restore app state; don't operate in the window hosting the session; tray icons → redraw as 示意画面.

## Covers
- 16:9 1920×1080, 4:3 1440×1080, 3:4 1080×1440, each composed separately. Big title + question subtitle; readable at thumbnail size.
- Check export folder and `~/Pictures/视频封面/` first; 口播 covers fresh per video unless reuse named.
- Archive to `~/Pictures/视频封面/<标题>-16-9.png` / `-4-3.png` / `-3-4.png`; verify size+hash; never silent overwrite.

## Optional reference style: 比特新语 (ONLY when the user explicitly says to 借鉴/参考 比特新语)
Not a default. Never apply these unless the user names 比特新语 for that video; otherwise keep the user's own style above. Full teardown: `/workspace/学习/比特心语/拆解.md` (covers in `covers/`).
- Account: B站「比特新语」(UID 3494362707135250), ~86万粉 in ~1 month from 2026-10-01, broke out on 诺奖周 (tracked fast). Partition 软件应用 + AI 活动话题; states made with Opus; likely subtitles + BGM, no narration.
- One idea per video, ~2:10–2:45 (max ~3:20); a long list video becomes a series of single-item shorts, long cut kept as 合集.
- Emotional translation: map the knowledge point to a human feeling; title and closing line land on it. Title pattern 「《片名》｜金句」 or one counter-intuitive sentence; avoid 「16个/盘点」 list words.
- Covers: near-black background, single glowing gold subject, huge 2- or 4-char serif title, two lines of 金句 with key words in gold, small top series tag; some covers are a single film-subtitle-like line for suspense. If borrowing, adapt to the user's own visual identity rather than cloning the dark-gold look.
- Hook text on frame 1 (no black fade-in); a turn every 10–15 s; subtitles act as narration: short lines cut to BGM bars.
- Chase public events (诺奖, astronomy events, science trends) within 24–48 h.
- 简介: 3–5 short prose lines + AI-made note + current activity topic. Track favorite rate (his hits ~5–7%).
- Caveats: his timing/platform-support window is not repeatable; emotion must serve verified facts in hard science.

## Export / delivery
- `~/Movies/剪映导出/<完整标题>/`; files and 剪映 project named with full title (dup → 「（口播版）」). 合成片: final + covers at folder root, NO `00_最终交付/` (that's only for 口播). Clean wrong old versions after verification.
- Deliver MP4, covers, editable project, music + asset sources, short report.
- Repo archive `videos/<date>_<short>/` (README, brief, storyboard, sources, qa-report, retro); update INDEX/preferences/lessons in place. No auto commit/push/publish.
- 简介 text is drafted for the publisher; one-off credits only when asked that time.
- 简介 compliance (B站 removed one for 违规推广, 2026-11-02): no URLs, no contact info, no 「详见置顶评论/评论区」 guidance, no filenames that look like domains (e.g. `sources.md` — `.md` is a TLD). Say 「资料来源见片尾」 instead.

## QA checklist (read logs, not exit codes)
ffprobe spec/duration (±1 frame); `ffmpeg -xerror` decode; ebur128 on final AAC; black/freeze/silence detect (freeze = clue); ±0.4 s frames at each handoff; reading time ≥ max(2 s, chars/4+0.5); bt709 yuv420p tv-range; first frame composed. Tech pass ≠ visual success; list 未验证项.

## Handoff to publish
Report path, ★ title + alternatives, 简介/tags draft, style one-liner, 未验证项, user to-dos. Hand to the video-publishing assistant (multipublish-video) with exact MP4, SRT, three cover paths. Do not upload.

## Hard stops
No uploading/publishing; no config/proxy changes; no credential reads; no overwriting user files or native drafts; no claiming "no issues" from checks alone.
