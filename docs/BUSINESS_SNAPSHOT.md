# BUSINESS_SNAPSHOT — done-coding-claude

> 文档定位：快照型（覆盖更新，只描述当前状态；[MUST NOT] 留流水账）。技术细节见 `TECH_SNAPSHOT.md`，治理视图见 `governance/SNAPSHOT.md`。

## 是什么

done-coding 的 **Claude Code 插件**（插件名 `done-coding`）：装上后在任意项目里以 `/done-coding:<skill>` 使用 done-coding 能力——一句话让 AI 用 hub 模板建项目、治理工具与跨仓 issue、workspace / search 两个方法。

## 服务谁

| 使用方 | 怎么用 |
|---|---|
| 用户本人（1 人 + 多 AI 会话，多台机器） | 装插件后在任意项目会话里用 |
| done-creating 等应用仓的会话 | 向 done-coding 各仓提基于实践的 issue（收件仓查 `~/.done-coding/harness/scope/`） |

## 与其他仓的关系

- **done-coding-cli**：CLI 类 skill 的源头是其 `@done-coding/cli-skills`；本仓只同步、改名、打包，不改内容。
- **done-coding-template-hub**：建项目所用模板的来源。

## 当前状态

已初始化治理目录，尚无插件产物；首版需求在 `governance/backlog/`。
