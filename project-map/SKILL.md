---
name: project-map
description: >-
  处理用户任何代码项目任务（改网站/工具页、合并推送、查某项目在哪）前读：用户全部项目的分布、远程仓库与 Mac 本地 ~/git_pro
  仓库对照，以及改代码/合并/推送的流程。
---
# 项目总览与本地仓库对照

用户（GitHub cpython666，另有 w-x-x-w、StarDreamTech 组织）的所有项目分布、对应的本地仓库路径和工作方式。项目管家 bot 处理任何项目任务前先读这里。

## 怎么接项目任务
1. 先在下方对照表里定位项目：本地目录（用户 Mac 上 `~/git_pro/<目录>`）、远程仓库、默认分支。表里没有的，用 GitHub 工具（list_my_repositories，sort=pushed）查，并把新项目补进本技能。
2. 改代码交给 Cursor 云端代理（CloudAgent launch，repo 填 https://github.com/<远程仓库>），把需求、截图、验收标准写清楚，让它自己调查和实现，开 PR。
3. 用户说“合并/推送”时：云端代理开完 PR 后，确认 CI 和预览正常，再让云端代理把 PR 合并进默认分支（注意有的仓库默认分支是 master）。合并即推送上线（例如 cpython666.github.io 由 GitHub Pages 自动部署到 https://cpython666.github.io/，StarDreamTech.github.io 同理部署到 https://stardreamtech.github.io/）。
4. 不在用户 Mac 上克隆或改代码；只在需要核对本地状态时，经用户授权在 Mac 上只读查看 `~/git_pro`（如 `git -C ~/git_pro/<目录> status`）。本地有未推送改动或在非默认分支上时，先告诉用户，不要覆盖。
5. 合并后提醒用户本地仓库可 `git pull` 同步。

## 重点项目速查
- 个人网站「星梦启航」：cpython666/cpython666.github.io（master），本地 ~/git_pro/cpython666.github.io，线上 https://cpython666.github.io/ ，工具页在 /tools/<工具名>/（如 /tools/markdown-image/）。
- 组织主页「星梦科技」：StarDreamTech/StarDreamTech.github.io（main），线上 https://stardreamtech.github.io/ 。Mac 本地尚未克隆。
- 星笺 Starclip（Rust 剪贴板）：StarDreamTech/starclip（cpython666/starclip 为 fork）；Homebrew 源 StarDreamTech/homebrew-tap，安装 `brew install --cask stardreamtech/tap/starclip`。
- 星镜 Starshot（截图工具）：StarDreamTech/starshot（cpython666/starshot 为 fork）。
- 星匣 StarVault（AI 对话档案）：StarDreamTech/starvault（cpython666/starvault 为 fork）。
- 星哨 StarWatch：StarDreamTech/StarWatch（筹备中；cpython666/StarWatch 为 fork）。
- 星搭子 starbuddy（2026-11-11 起公开，第 0 期，本地未发现）：StarDreamTech/starbuddy。组织禁用私有 fork，cpython666 下没有副本。
- 星相 StarPersona（公开，2026-11-11 新建，只有 README）：StarDreamTech/StarPersona，指纹浏览器 / 多账号环境管理器，第一期用现成内核（Camoufox 或魔改 Chromium）只做外层管理器，Windows + macOS。
- 星盘 StarDash（公开，2026-11-11 新建，只有 README）：StarDreamTech/StarDash，对标 CalmBar（chao-eng/CalmBar）的跨平台菜单栏/托盘状态面板，计划 Tauri，动态 SVG 图标 + 多主题。
- Grok Bot 共享技能库：cpython666/grokbot-skills（每晚同步到 Mac）。
- 内容仓库：WechatPilot（公众号）、VideoPilot（视频）、xingxiang（星象视频技能）。
- 运维：ai-server-ops（私有）；电脑助手 my-computer-assistant（每台电脑一个分支）。
- 其他 StarDreamTech 组织仓库：StarScout、sd-spider-utils、sd_ctx、starscout-skill。

## 本地仓库对照表（2026-11-01 盘点，按最近推送排序）
| 本地目录 (~/git_pro/) | 当前分支 | 远程仓库 | 最近推送 | 说明 |
|---|---|---|---|---|
| grokbot-skills | main | cpython666/grokbot-skills | 2026-11-01 | 小星的 Grok Bot 共享技能库 |
| hyperliquid_trader_stats_pro | main | cpython666/hyperliquid_trader_stats_pro | 2026-11-01 |  |
| starclip | claude/project-thread-r6wahm | cpython666/starclip | 2026-11-01 | 星笺 Starclip · Rust 驱动的本地优先剪贴板管理器，让每一次复制都 |
| cpython666.github.io | master | cpython666/cpython666.github.io | 2026-10-30 | 星梦启航 |
| homebrew-tap | main | cpython666/homebrew-tap | 2026-10-29 | 星笺 Starclip 的 Homebrew 安装源（Apple Silicon |
| starshot | codex/screenshot-interactions-20261029 | cpython666/starshot | 2026-10-29 | 星镜 Starshot：本地优先的桌面截图、标注、贴图与图片美化工具 |
| chat-history-vault | main | cpython666/chat-history-vault | 2026-10-28 | Incremental Codex and Claude chat archiv |
| HandwritingGenerator | main | cpython666/HandwritingGenerator | 2026-10-25 | HandwritingGenerator，一个使用PyQt6制作的手写文本图片生 |
| sd-spider-utils | main | StarDreamTech/sd-spider-utils | 2026-10-16 | 爬虫工具库，解析，文本标准化等，爬虫常用的方法和工具函数。 |
| my-computer-assistant | computer/macbook-pro-4 | cpython666/my-computer-assistant | 2026-10-15 | 我的电脑助手：电脑操作说明与经用户授权的脚本；不同电脑使用独立分支。 |
| kr6-ai-heroes | main | cpython666/kr6-ai-heroes | 2026-10-14 | Kingdom Rush 6: Genesis 非官方双角色 Mod：小克炮塔与 |
| WechatPilot | main | cpython666/WechatPilot | 2026-10-13 | 公众号创作仓库：选题、文风、栏目模板、发布经验与文章归档 |
| ai-server-ops | claude/project-thread-5ejqwz | cpython666/ai-server-ops | 2026-10-13 | AI 辅助服务器运维工作区：SSH 连接、项目运行状态查看与部署脚本管理。 |
| VideoPilot | main | cpython666/VideoPilot | 2026-10-11 | 我的视频创作仓库：要求、审美、全流程经验与工具，一句话生成视频 |
| IPProxyPoolMax | main | cpython666/IPProxyPoolMax | 2026-10-08 |  |
| xingxiang | main | cpython666/xingxiang | 2026-10-08 | 星象：以艺术画面、BGM与精炼文字制作无旁白视频的 Agent Skill。 |
| warden-of-wonders-skill | main | cpython666/warden-of-wonders-skill | 2026-08-25 |  |
| BossPilot | main | cpython666/BossPilot | 2026-08-11 |  |
| BiliScout | main | cpython666/BiliScout | 2026-08-05 |  |
| GrowthPilot | main | cpython666/GrowthPilot | 2026-08-05 |  |
| IPProxyPoolPro | main | cpython666/IPProxyPoolPro | 2026-07-22 |  |
| hyperliquid-trader-stats | main | cpython666/hyperliquid_trader_stats | 2026-07-22 |  |
| cpython666 | main | cpython666/cpython666 | 2026-07-09 |  |
| Spider-Project | main | cpython666/Spider-Project | 2026-07-06 | 爬虫实操项目合集代码及分析 |
| learn_test | main | cpython666/learn_test | 2026-07-02 |  |
| ScribeFlow | main | cpython666/ScribeFlow | 2026-01-24 | 全平台视频文案自动化采集与 AI 处理工具 |
| BloggerVault | main | cpython666/BloggerVault | 2026-01-20 | 📥 BloggerVault (博主文章归档计划) |
| SubtitleExtractor | main | cpython666/SubtitleExtractor | 2026-01-18 | 字幕提取器3.0-终极版本，预计语音识别与ocr识别两种都支持。 |
| SubExtractor-OCR | main | cpython666/SubExtractor-OCR | 2026-01-15 | SubExtractor-OCR 是一款基于 OCR（Optical Chara |
| ContentArchiver | main | cpython666/ContentArchiver | 2025-12-14 | 自动化采集与备份网络内容，包括 Youtube / B站 视频字幕、公众号文章以 |
| NewsSpider | main | cpython666/NewsSpider | 2025-12-03 |  |
| drawio_pro | main | cpython666/drawio_pro | 2025-10-30 | drawio流程图存储 |
| StarDream | main | cpython666/StarDream | 2025-10-19 | 星梦启航 |
| chain-scout | main | cpython666/chain-scout | 2025-08-27 | Web3-Monitor-Go 是一个使用 Go 语言构建的 Web3 领域信息 |
| walktheblock.github.io | walktheblock | WalkTheBlock/walktheblock.github.io | 2025-08-16 | 区块漫步 |
| StarDreamWeb3 | main | cpython666/StarDreamWeb3 | 2025-06-21 |  |
| HyperX | main | cpython666/HyperX | 2025-06-15 | HyperLiquid账户持仓分析 |
| stardream-logos | main | cpython666/stardream-logos | 2025-05-02 | logo图片 |
| AutoDex | main | cpython666/AutoDex | 2025-04-11 |  |
| StarDream-frontend | main | cpython666/StarDream-frontend | 2025-03-17 | 星梦启航-前端-Vue+Vuetify |
| Web3Monitor | main | cpython666/Web3Monitor | 2025-03-15 | 区块链新闻监控网站 |
| StarDreamSpider | main | cpython666/StarDreamSpider | 2025-03-09 | 星梦爬虫，这个名字真是，碉堡了。学习爬虫的一些小demo项目辣，嘿嘿嘿。 |
| stardream_api_spider_service | main | cpython666/stardream_api_spider_service | 2025-03-09 | DrissionPage+FastAPI，将爬虫服务封装为一个服务，请求之后返回 |
| sd_ctx | main | StarDreamTech/sd_ctx | 2025-03-08 | 浏览器插件 |
| chrome-extensions-samples | main | cpython666/chrome-extensions-samples | 2025-03-03 | Chrome Extensions Samples |
| CodeCapsule | main | cpython666/CodeCapsule | 2025-03-02 | 代码胶囊 |
| stardream_curlconverter_service | main | cpython666/stardream_curlconverter_service | 2025-03-01 | 利用NodeJS的express实现后台接口，curlconverter库实现请 |
| stardream_python_sandbox_service | main | cpython666/stardream_python_sandbox_service | 2025-03-01 | 执行Python代码的代码沙箱，FastAPI做后端，命令行运行python代码 |
| appsmith | main | cpython666/appsmith | 2025-02-28 | appsmith存储仓库 |
| StarDream-manage | main | cpython666/StarDream-manage | 2025-01-08 | 星梦启航-网站管理端 |
| AlgorithmPython | main | cpython666/AlgorithmPython |  |  |
| AwesomeWeb | main | cpython666/AwesomeWeb |  |  |
| CodeNotes | main | cpython666/CodeNotes |  |  |
| CoolBgs | master | cpython666/CoolBgs |  |  |
| DailyNews | main | cpython666/DailyNews |  |  |
| DanmuSpider | main | cpython666/DanmuSpider |  |  |
| DjangoBlog | master | cpython666/DjangoBlog |  |  |
| FuckSpider | main | cpython666/FuckSpider |  |  |
| GitProject | master | w-x-x-w/GitProject |  |  |
| Godot | main | w-x-x-w/Godot |  |  |
| HandwritingCanvas | main | cpython666/HandwritingCanvas |  |  |
| Learn-Electron | master | cpython666/Learn-Electron |  |  |
| Learn-Go | main | w-x-x-w/Learn-Go |  |  |
| LearnSpider | main | cpython666/SpiderChallenges |  |  |
| PyQt6_Apps | master | cpython666/PyQt6_Apps |  |  |
| Python-Project-Pro | main | cpython666/Python-Project-Pro |  |  |
| Python-Project | main | cpython666/Python-Project |  |  |
| Self-introduction-web | main | w-x-x-w/Self-introduction-web |  |  |
| Spider-Tools | main | cpython666/Spider-Tools |  |  |
| StarDream-1 | main | w-x-x-w/StarDream |  |  |
| StarDream-Intro | main | cpython666/StarDream-Intro |  |  |
| StarDream-VitePress | master | cpython666/StarDream-VitePress |  |  |
| StarDream-v3 | master | cpython666/StarDream-v3 |  |  |
| StarDreamAPI | main | cpython666/StarDreamAPI |  |  |
| StarDreamCode-backend | main | cpython666/StarDreamCode-backend |  |  |
| StarDreamCode-frontend | main | cpython666/StarDreamCode-frontend |  |  |
| StarDreamScrapy | main | cpython666/StarDreamScrapy |  |  |
| StarScout | codex/external-optimization-v2.9.6 | StarDreamTech/StarScout |  |  |
| Stardream-mysql | main | cpython666/Stardream-mysql |  |  |
| Stardream-redis | main | cpython666/Stardream-redis |  |  |
| Thousand-Image-Generator | main | cpython666/Thousand-Image-Generator |  |  |
| WTF-EVM-Opcodes | main | WTFAcademy/WTF-EVM-Opcodes |  |  |
| WTF-Ethers | main | WTFAcademy/WTF-Ethers |  |  |
| WTF-zkSync | main | WTFAcademy/WTF-zkSync |  |  |
| WebSpider | 1.2 | w-x-x-w/WebSpider |  |  |
| ai-app-automation | main | (无远程) |  |  |
| business-intelligence-homework | master | gitee:hao-wenhai/business-intelligence-homework |  |  |
| crawlab-demo | master | cpython666/crawlab-demo |  |  |
| dhlj-se-agent | 0.1.4 | zcli-charlie/dhlj-se-agent |  |  |
| django-vercel | main | cpython666/django-vercel |  |  |
| dsh-bili-scroll | codex/fix-settings-persistence | c1overzz/dsh-bili-scroll |  |  |
| flask | main | w-x-x-w/flask |  |  |
| flutter | stable | flutter/flutter |  |  |
| scrapy-drissionpage | main | cpython666/scrapy-drissionpage |  |  |
| stardream-oss | main | cpython666/stardream-oss |  |  |
| stardream_services | main | cpython666/stardream_services |  |  |
| starscout-skill | main | StarDreamTech/starscout-skill |  |  |
| tuchuang | master | gitee:w-_-x/tuchuang |  |  |
| w-x-x-w | main | w-x-x-w/w-x-x-w |  |  |
| wechat-home-service | main | cpython666/wechat-home-service |  |  |
| workbuddy2api-panel | main | linguo2625469/workbuddy2api-panel |  |  |

## 只在 GitHub、本地 ~/git_pro 未发现的较新项目
| 远程仓库 | 默认分支 | 最近推送 | 可见性 | 说明 |
|---|---|---|---|---|
| StarDreamTech/StarDreamTech.github.io | main | 2026-11-11 | 公开 | 星梦科技组织主页，GitHub Pages 发布到 https://stardreamtech.github.io/ |
| StarDreamTech/starbuddy | main | 2026-10-31 | 公开（11-11 起） | 星搭子：常驻桌面的星芽个人电脑助手（已转到组织；第 0 期，公开前不要上组织主页） |
| StarDreamTech/StarPersona | main | 2026-11-11 | 公开 | 星相：指纹浏览器 / 多账号环境管理器（新建） |
| StarDreamTech/StarDash | main | 2026-11-11 | 公开 | 星盘：跨平台菜单栏/托盘状态面板（新建，对标 CalmBar） |
| cpython666/lemo-opuscar | main | 2026-10-22 | 公开 | A toolbox of film styles made in code fo |
| cpython666/dsh-bili-scroll | main | 2026-10-22 | 公开 | DSH 插件：每天替你刷一轮 B站，读字幕挑出值得的、写一份日报，值得的 @ 你 |
| cpython666/dsh-purge | master | 2026-10-21 | 公开 | 让 AI 更专注地辅助学习与动手实验 —— DeepSeek Harness 附 |
| cpython666/OpenStock | main | 2026-10-20 | 公开 | OpenStock is an open-source alternative  |
| cpython666/cpython666-waline | main | 2026-10-12 | 私有 |  |
| cpython666/workbuddy2api-panel | main | 2026-10-12 | 公开 | 把腾讯WorkBuddy账号变成 OpenAI 兼容 API 的多账号网关，同时 |
| cpython666/any-pr | main | 2026-10-11 | 公开 |  |
| cpython666/godot_pro | main | 2026-10-11 | 私有 |  |
| cpython666/rea | main | 2026-10-09 | 公开 | Reverse engineer anything with agents, f |
| cpython666/ModelTrace | main | 2026-10-09 | 公开 | 主动探测模型归因 |
| cpython666/IP-Proxy-Pool | main | 2026-08-18 | 公开 |  |
| cpython666/go_pro | master | 2026-07-06 | 公开 |  |
| cpython666/SiteTree | main | 2026-07-06 | 私有 |  |
| cpython666/ast_pro | main | 2026-07-01 | 公开 |  |
| cpython666/auto_trade | master | 2026-07-01 | 公开 |  |
| cpython666/earn_pro | master | 2026-07-01 | 公开 |  |
| cpython666/free-stockdb | main | 2026-06-29 | 公开 | 每日更新！免费股票日k、分时k线数据，etf分钟数据，截至到 2026-07 月最新 |
| cpython666/pixel2motion | main | 2026-06-13 | 公开 | AI logo animation skill: turn raster log |

## 维护
- 新建/删除/改名项目或本地目录变化时，更新本技能对照表。
- 本地目录名与远程名不同的要注明（如 LearnSpider → cpython666/SpiderChallenges，hyperliquid-trader-stats → cpython666/hyperliquid_trader_stats，StarDream-1 → w-x-x-w/StarDream）。
