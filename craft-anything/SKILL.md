---
name: craft-anything
description: >-
  用于研究已发布软件（程序、应用、安装包、Electron、APK、固件、网页）的工作原理并复刻自己的版本：通过 Craft Anything 的 MCP
  工具或 craft-anything-cli 给出有证据的结论，并在项目里持续记录简报、计划、假设、发现和交接。
---
> 本机安装：`craft-anything-cli` 在 `/home/box/.local/bin/`（官方 v0.6.0 Release，已校验签名）。连接器未接时，可直接用命令行跑：每个工具都是一个子命令，例如 `craft-anything-cli triage <路径>`、`craft-anything-cli core-target-open --json '{"path": "..."}'`。MCP 启动命令：`craft-anything-cli mcp --all-tools`（需要读目标内部再加 `--deep`）。只用于研究和复刻自己有权使用的软件或公开网页，不用于破解、绕过授权。

# Craft Anything: evidence-first investigation

Use Craft Anything when an answer depends on something that was *built and shipped*: an executable, a library, an app bundle, an APK, an Electron app, a WebAssembly module, firmware, a crash dump or a network capture. If you have the source code and the question is about the source, read the source instead; that is faster and more direct.

## Connect only when you need it

- If the `craft-anything` tools are already in your tool list, go straight to work. Don't run setup or doctor first.
- Trust the live tool list and its schemas over this file; the server may be newer or older.
- If the tools are missing or failing to start, run `craft-anything-cli doctor` and then `craft-anything-cli setup --dry-run` and show the user the plan before applying anything. After a successful setup the user must restart or reconnect their app.
- **Never run `setup --yes` (or `setup --client …`) on an entry that already lists every tool.** `setup` writes the plain `mcp` command, so it drops an `--all-tools` that is already in the entry and the server falls back to the small core toolset. Read the client's config first: if the `args` of `craft-anything` end in `--all-tools`, leave the entry alone. `setup --dry-run` only prints the plan and is safe. To add a client, write the entry by hand with `--all-tools`.
- Only a small core toolset is listed at first. Call `list_toolsets` to see the others and `enable_toolset` to switch one on (native code, Android, Apple, web, runtime…).
- In Clean room (Deep mode off, the default) nothing inside a target is read: only outside-view tools are listed, and others are refused with `details.reason` `clean_room`. Tell the user the question needs Deep mode (`settings_set deep_mode true`, or the server started with `--deep`) instead of working around it.

## Working memory: keep it current

1. **Start or resume.** Call `core_investigation_show` first. If there is a handoff, continue from it and the plan. Also call `core_session_show` to see what is open.
2. **New question?** Before any analysis call, write the brief with `core_brief_write` (question, why, targets, constraints such as "don't run the program", what a finished answer looks like) and an initial plan with `core_plan_update` (short numbered steps, each `todo`/`doing`/`done`/`blocked` with a reason).
3. **After each batch of tool calls:** update plan status. For a testable claim, `core_hypothesis_record` with the prediction; when evidence arrives, `core_hypothesis_update` (supported, refuted, abandoned) with evidence ids.
4. **When something is settled:** `core_finding_record` with the statement and at least one evidence id. Findings are what reports are built from, never chat text.
5. **At the end of every turn:** `core_handoff_write`: where things stand, next steps, traps to avoid.
6. `core_journal_read` shows every earlier tool call when you need to know what was already tried.

## Method

- **Observe, derive, infer, and say which.** Label each claim.
- **Cite evidence ids** (`ev_…`) for every claim. A claim with no evidence id is a hypothesis.
- **Absence is not proof.** State the search boundary and coverage; record open unknowns with `core_unknown_add`.
- **Predict, then verify.** Write the expected result before testing; update the hypothesis if it disagrees.
- **Summary first, then page.** Use `offset`/`limit` or the evidence id. Never repeat an identical call that already succeeded or was rejected.
- **Format-aware, not filename-aware.** Let the parsers tell you what a file is.

## Where to start, by target

| Target | First step |
|---|---|
| Native executable or library (ELF, PE, Mach-O) | `core_target_open`, then the overview, search and function tools |
| Electron app, `.asar`, or a JavaScript bundle | `core_target_open`, then the JavaScript toolset |
| Android APK / DEX | `core_target_open`, then the Android toolset |
| .NET assembly | `core_target_open`, then the managed toolset |
| WebAssembly, Go, PE resources, firmware, crash dumps | the formats toolset |
| A live web page or Electron window | the browser toolset (observation only) |
| Two versions of the same app | open both, then the application toolset's comparison tools |

If the user says "my app" without naming it, ask which one. Never guess with an example file.

## Consent and safety

- Tools that run the target's code or change a connected device need the user's explicit OK. If a call returns `consent_required`, explain and ask; never work around it.
- Static analysis never runs the target. Don't claim runtime behaviour from static evidence alone.
- Never put secrets, cookies or personal data into notes, findings or handoffs.

## When something fails

| Error code | What to do |
|---|---|
| `not_found` | Open a target first (`core_target_open`), or check the path or name |
| `feature_missing` / `engine_missing` | Read the remediation; it names the toolset, engine or setting needed |
| `over_limit` | Page it or read it by evidence id (`evidence://<id>`) |
| `stale_revision` | Re-read with `core_investigation_show`, merge, retry |
| `consent_required` | Ask the user |

## Connection and recovery

| Symptom | What to do |
|---|---|
| No `craft-anything` tools in the app | `craft-anything-cli doctor`; if registration is missing, `setup --client <id> --dry-run`, show the plan, apply with `--yes` only after the user agrees |
| Registration looks right but no tools | Restart or reconnect the app |
| `craft-anything-cli` not found from a shell | Not on `PATH`; use its absolute path |
| A tool says an engine is missing | Follow its remediation |

Before you finish: mark each plan step done or blocked, make sure every conclusion matches a recorded finding, list what is still unknown, and write the handoff.

来源：storytold/craft-anything v0.6.0 `crates/setup/src/skill.md` 与 `skill_recovery.md`（Apache-2.0 / MIT）。
