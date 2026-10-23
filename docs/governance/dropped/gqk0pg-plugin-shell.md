---
id: gqk0pg
title: 插件外壳与安装：plugin.json + marketplace.json，对外命名 /done-coding:*
modules: [packaging]
created: 2026-10-02
parent: ""
dropped: 被 b8zi11 取代：本仓改为纯市场目录（双宿主 marketplace.json，插件来源 = npm @done-coding/cli-skills），不再自建插件外壳与对外改名表
dropped_at: 2026-10-23
merged_into: b8zi11
---

## 背景（用户 2026-10-02 定调）

一个可公开安装的 Claude Code 插件 `done-coding`：装上即得 CLI 类能力（一句话让 AI 建项目、治理工具、跨仓 issue）与 workspace / search 两个方法。分层：cli-skills 只管 CLI 自身 skill，本仓把它包装为自身、对外透明。

## 要做

- 插件名 `done-coding`；本仓同时是插件市场。安装 = `/plugin marketplace add <本仓地址>` + `/plugin install done-coding@<市场名>`，不需预装 done-coding-cli 或任何 npm 包（插件安装即克隆仓库）。
- 对外命名（用户定）：插件命名空间 `done-coding:` 承担归属，skill 名 [MUST NOT] 再带 `dc-` / `done-coding` / `harness-` 冠名：

| 插件指令 | 来源 |
|---|---|
| `/done-coding:create` | cli-skills `create-done-coding`（并入 x-create 推断规则后） |
| `/done-coding:harness` | cli-skills `cli-harness`（清单 / 治理闸 / issue / scope） |
| `/done-coding:search` | 本机 `harness-search` |
| `/done-coding:workspace` | 本机 `harness-workspace` |

  cli-skills 其余 skill 按同一判据去冗余（如 `cli-generator` → `generator`）。CLI 二进制名（`dc-harness` 等）在 PATH 共享空间，保留 `dc-`，不受本条约束。
- 实测记录：能否省略 `done-coding:` 前缀直接调用。

## 前置

- 远端放 GitHub `done-coding` 组织还是 gitee：**待用户定**；仓库公开，首次 push 需当轮授权。

## 完成判据

- `claude plugin validate .` 退 0；
- 隔离环境（不含本机 `~/.claude/skills`）按两步安装成功，`/done-coding:` 下列出首版全部 skill，名字与上表一致。

## 范围外

全局 CLAUDE.md 初始化（首版不做）；官方插件市场上架；Codex / Cursor 等多平台适配。
