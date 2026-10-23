---
id: 0fmk8c
title: 同步 @done-coding/cli-skills 进插件（锁版本 + 确定性改名），含跨仓 issue 收件仓注册的透出验收
modules: [packaging]
created: 2026-10-02
parent: ""
dropped: 不再需要：插件内容直接取 npm 发布的 @done-coding/cli-skills（Claude / Codex 均实测支持 npm 插件来源），本仓不拷贝 skill、无同步脚本
dropped_at: 2026-10-23
merged_into: b8zi11
---

## 要做

- 以 `@done-coding/cli-skills` 为 CLI 类 skill **唯一源头**：本仓锁定其版本，同步脚本在**发布前**把其 `skills/` 拷入插件目录并提交；本仓 [MUST NOT] 手改这些拷贝（改动回 done-coding-cli 提 issue）。
- 同步时确定性改写：按 `gqk0pg` 的命名表改名；skill 正文互相引用的名字随之改；`npx <cli>@latest` 是否改固定版本在实施时定（防 skill 文本与 CLI 参数漂移）。
- 备选方案需比较后定：插件可声明依赖其他插件（`claude plugin prune` 说明存在自动安装的依赖）——cli-skills 自成插件、本插件依赖它，可免拷贝，但带它自己的前缀、做不到改名。
- **收件仓注册透出**（用户定为当前最迫切能力）：多个 monorepo 项目会持续向 done-coding-cli / admin / template-hub 提 issue。能力本体由 done-coding-cli 实现（backlog `qdoeql`，经 issue `ff5p5s` 提优先级；注册表 `~/.done-coding/harness/scope/`，手工版已建，即格式样本），经 `cli-harness` 进入本插件为 `/done-coding:harness`；本仓不另实现。

## 前置（done-coding-cli，issue `ff5p5s`）

ⓐ 发布 `@done-coding/cli-harness`（2026-10-02 npm 404）；ⓑ 实现 `qdoeql`；ⓒ `create-done-coding` 并入 x-create 推断规则（3 必答 + 按约定推断 + 回显确认）。

## 完成判据

- 同步脚本重跑零 diff；插件内 CLI 类 skill 与所锁版本 cli-skills 一致，差异仅限约定的确定性改写；
- 隔离环境装插件后：在任意目录一句话让 AI 用 hub 模板建项目，走 `/done-coding:create`，只问 3 个必答、其余推断并回显确认；
- 经 `/done-coding:harness` 能列出已注册收件仓，并向其中一个成功提 issue。
