# SNAPSHOT — 治理视图（上层组合）

> 文档定位：快照型。每领域一行摘要 + 跨领域依赖 + 独占点；细节走链接，[MUST NOT] 复制项目快照内容。
> 领域清单唯一真源：`MODULES.md`。项目全貌：`../BUSINESS_SNAPSHOT.md` · `../TECH_SNAPSHOT.md`。

| 模块 | 一行摘要 |
|---|---|
| `packaging` | 未开工：插件外壳 / cli-skills 同步 / 本地开发闭环均在 backlog |
| `method` | 未开工：workspace / search 迁入在 backlog |

## 跨领域依赖

`method` 的 skill 经 `packaging` 的插件外壳对外发布；`packaging` 不依赖 `method` 的内容。

## 外部依赖

CLI 类能力依赖 done-coding-cli（issue `ff5p5s`：发布 `@done-coding/cli-harness`、实现 scope 注册、`create-done-coding` 并入 x-create 推断规则）。

## 共享骨架 / 独占点

| 点 | 规则 |
|---|---|
| `.claude-plugin/`（插件 / 市场清单） | 改动方在 `PROGRESS.md` 声明独占 |
