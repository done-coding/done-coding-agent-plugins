---
id: oekr57
title: 市场条目展示字段对齐 superpowers（category / policy / interface）
modules: [packaging]
created: 2026-10-23
source: 用户 2026-10-23 在 done-coding-cli 会话中授权（与 cli 仓批次 ek4duc 同轮）
after: ""
---

# PROGRESS — oekr57

独占：`.claude-plugin/`、`.agents/plugins/`（两份同改）。

## 进度

- [x] 1wq2lp Codex 目录加 `interface.displayName`，条目加 `category: Developer Tools` 与 `policy`（AVAILABLE / ON_INSTALL，取值以 Codex 0.162.1 程序内枚举核实）；Claude 条目加 `category: development`（官方市场惯用值）。
- [x] 验收：`claude plugin validate .` 通过；隔离 `CODEX_HOME` 下 `codex plugin marketplace add <本仓>` + `codex plugin list` 正常列出 `done-coding@done-coding`。
- [x] 快照：TECH_SNAPSHOT 记展示字段与包内清单现状；治理 SNAPSHOT `packaging` 行更新。
- 版本号由包内清单提供（done-coding-cli 批次 ek4duc），不写进市场条目。

## 交付

| 条目 | sha | 结果 |
|---|---|---|
| 1wq2lp | e11e5b8 | 两份目录展示字段补齐 |
