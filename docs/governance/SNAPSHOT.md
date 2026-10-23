# SNAPSHOT — 治理视图（上层组合）

> 文档定位：快照型。每领域一行摘要 + 跨领域依赖 + 独占点；细节走链接，[MUST NOT] 复制项目快照内容。
> 领域清单唯一真源：`MODULES.md`。项目全貌：`../BUSINESS_SNAPSHOT.md` · `../TECH_SNAPSHOT.md`。

| 模块 | 一行摘要 |
|---|---|
| `packaging` | 市场目录已建：Claude / Codex 两份 marketplace.json，插件 `done-coding` ← npm `@done-coding/cli-skills`；两宿主本地安装实测通过；展示字段（category / policy）已对齐 superpowers |
| `method` | 待用户裁决是否经本市场分发（backlog `hd8ue4`） |

## 跨领域依赖

`method` 若分发，同样以 npm 包为来源，在 `packaging` 的两份目录各加一条。

## 外部依赖

插件内容依赖 done-coding-cli 发布的 `@done-coding/cli-skills`（2026-10-23 已发 0.3.0）；skill 改动回 done-coding-cli。

## 共享骨架 / 独占点

| 点 | 规则 |
|---|---|
| `.claude-plugin/`、`.agents/plugins/`（两份市场目录） | 改动方在 `PROGRESS.md` 声明独占，两份同改 |
