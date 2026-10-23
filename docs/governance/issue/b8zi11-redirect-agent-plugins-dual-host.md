---
id: b8zi11
title: 方向修订：改名 done-coding-agent-plugins（monorepo）、双宿主插件清单、cli-skills 0.3.0 为 skill 源头、方法类 skill 待定
created: 2026-10-23
from: done-coding-cli
---

## 现象

本仓 backlog（`gqk0pg` / `0fmk8c` / `hd8ue4` / `gvrk4u`）按 10-02 方向写成「只服务 Claude Code 的插件 done-coding-claude」。用户 2026-10-22 起已调整方向，且前置已部分满足，现有条目与之不符：

ⓐ **定位与命名**：仓名定为 **`done-coding-agent-plugins`**，走 monorepo；定位为「同一份 skill 按各 AI 宿主（Claude Code / Codex 等）的插件格式打包分发」，与 superpowers 等第三方插件同一生态位。插件**不感知 dotfiles**；dotfiles 只作为使用方声明式安装（见 dotfiles issue `plcr5b`）。插件名 `done-coding` 保持（指令前缀 `/done-coding:*`）。
ⓑ **双宿主清单**：同仓 `skills/` 共用，Claude 侧 `.claude-plugin/plugin.json` + `marketplace.json`，Codex 侧 `.codex-plugin/plugin.json` + `.agents/plugins/marketplace.json`；**两套清单版本号须一致**（本仓发布纪律，不由 dotfiles 兜底）。待核实：OpenAI 文档示例 `"$schema": "https://agent-plugins.org/schemas/1.0.0/plugin.schema.json"` 是否为跨宿主通用清单、能否收敛为一份（二手资料，未验证）。
ⓒ **skill 源头**：CLI 类 skill 唯一源头仍是 `@done-coding/cli-skills`（2026-10-23 已发布 0.3.0：create-done-coding / cli-generator / module-generate / cli-harness，均已去 Claude 专属写法）。cli 侧 `lerna.json` 已放行 SKILL.md 改动参与发版判定，只改 skill 正文也会发新版供同步。
ⓓ **方法类 skill 待定**：`hd8ue4` 原计划迁入 harness-workspace / harness-search，但两者现已在 dotfiles `home/.agents/skills/` 统一维护；进插件即成两份源头。需用户裁决：插件只打包 CLI 类 skill，或方法类源头整体迁入本仓、dotfiles 改为安装插件。
ⓔ **安装器关系**：`dc-cli-skills install`（`-t claude|codex|agents`、`-l` 软链）保留为不装插件场景的通用工具，非插件分发主路径。

## 前置状态

- ✅ cli 发版（cli-harness 0.1.0 首发、cli-skills 0.3.0 等，2026-10-23）。
- ⏳ 本仓改名（本地目录 / 仓内 6 处文档 / harness 注册表 `scope register` 重登）、建远端（需用户建）。

## 处置参考（非方案指定）

按上述方向修订 / 合并 4 条 backlog；指令文件按 harness-setup 新版 F9 落 `AGENTS.md` + 同目录 `@AGENTS.md` 的 `CLAUDE.md`。
