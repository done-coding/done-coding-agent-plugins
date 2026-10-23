---
id: k77b83
title: 改为插件市场目录仓：双宿主 marketplace.json，插件来源 = npm @done-coding/cli-skills
modules: [packaging]
created: 2026-10-23
source: issue b8zi11（用户 2026-10-23 在 done-coding-cli 会话中触发分诊并授权实施）
after: ""
---

# PROGRESS — k77b83

## 分诊

- b8zi11 → 本批次。方向在实施中再修订：插件内容不在本仓（不拷贝、不同步 skill），市场条目直接以 npm 已发布包为来源；仓库不做 monorepo（无包）。
- gqk0pg / 0fmk8c / gvrk4u → dropped（merged_into b8zi11，理由见各条目）；hd8ue4（方法类 skill）留 backlog 待用户裁决。

## 进度

- [x] 本地目录 done-coding-claude → done-coding-agent-plugins；仓内名称引用更新。
- [x] `.claude-plugin/marketplace.json`、`.agents/plugins/marketplace.json`：市场 `done-coding`，插件 `done-coding` ← npm `@done-coding/cli-skills`（不钉版本）。
- [x] 验收：`claude plugin validate .` 通过；临时 `CODEX_HOME` 以本仓目录作市场安装，Codex 可用 skill 为 `done-coding:cli-generator / cli-harness / create-done-coding / module-generate`；临时 `CLAUDE_CONFIG_DIR` 安装成功、已启用、缓存含 4 个 skill（临时目录无登录态，Claude 会话内识别未测，按官方插件 `skills/` 标准布局自动加载）。
- [x] 文档：README（双宿主安装 / 更新 / 防双份加载）、根指令 CLAUDE.md → AGENTS.md + 引用式 CLAUDE.md、治理指令 CLAUDE.md → AGENTS.md、MODULES packaging 行、三份快照。
- [x] 收口：dc-harness lists / check。

## 交付

| 条目 | 结果 |
|---|---|
| b8zi11 方向修订 | 本仓为纯市场目录，两宿主可装 done-coding 插件；远端仓与改名后的注册表重登见交付报告 |
