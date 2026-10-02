---
id: hd8ue4
title: 迁入 workspace / search 两个方法类 skill（逐条重判 + 依赖随包）
modules: [method]
created: 2026-10-02
parent: ""
---

## 要做

- 首版只迁 `harness-workspace` → `skills/workspace/`、`harness-search` → `skills/search/`（用户定）；其余本机 skill 不进。
- 迁移 [MUST] 逐条重过判据：对任意项目成立、不含个人 / 业务信息（路径、仓名、账号、私人目录）、依赖文件可随插件打包；[MUST NOT] 因「原来就这么写」整搬。
- 依赖随包：两 skill 引用的 `~/.claude/` 下 knowledge / protocols / templates 等文件（`harness-workspace` 2 处、`harness-search` 1 处）按需带入插件，引用改为相对 skill 自身目录；只带被引用的部分。
- 正文里对 `harness-*` 名字的自引用改为插件命名。

## 完成判据

- 插件内 grep 不到个人路径 / 私人目录名、零 `~/.claude/` 读依赖；
- 隔离环境中两 skill 可触发，引用文件均可读到；
- 逐条判据结论写进批次 `PROGRESS.md`。

## 范围外

本机 `~/.claude/skills/harness-workspace`、`harness-search` 原版的移除：属 `~/.claude` 体系层改动，插件版验证可用后按全局规则另走 `~/.claude` 的 specs + Gate（不移除会与插件版同时触发）。
