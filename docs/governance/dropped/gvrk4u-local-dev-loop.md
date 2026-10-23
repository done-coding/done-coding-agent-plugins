---
id: gvrk4u
title: 本地开发与验收闭环：--plugin-dir 日常加载、本地市场安装验收、validate 门禁
modules: [packaging]
created: 2026-10-02
parent: ""
dropped: 并入 b8zi11 批次：本地以目录作市场 + plugin validate + 临时配置目录安装实测即验收闭环；不再有 --plugin-dir 加载工作区 skill 的场景
dropped_at: 2026-10-23
merged_into: b8zi11
---

## 背景（用户 2026-10-02）

直接改 `~/.claude/skills` 反馈快，但会形成第二份源头且名字与发布版不同。定调：**本仓是唯一源头**，本地用插件方式直接加载工作区。

## 要做

| 场景 | 做法 |
|---|---|
| 日常改 skill | `claude --plugin-dir <本仓路径>` 直接加载工作区（经 `DC cc-switch` 启动时参数原样透传）；提供别名 / 启动脚本写进 README |
| 发布前验收 | `claude plugin marketplace add <本仓本地路径>` + install，走真实安装流程；`claude plugin validate .` |
| 他机 / 他人 | 远端市场安装 |

- [MUST NOT] 用软链把插件 skill 挂进 `~/.claude/skills`（无命名空间、与发布名不一致、装插件后成双份）。
- 实测并写明：改 skill 后是否需开新会话才生效。

## 完成判据

- README 写明三种场景的命令；按「日常」方式启动后 `/done-coding:` 下可见工作区内 skill，改一处文本后按记录的方式生效；
- 本地市场安装路径实跑一次成功。
