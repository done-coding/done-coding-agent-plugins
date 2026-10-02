# 治理指令层 — done-coding-claude

> 承接本目录治理工作的会话 [MUST] 遵守。完整方法论见 harness-workspace skill，本文件只落本仓的 [MUST] 条款。

## 单态流转

- 条目正文任一时刻只在一个文件里；生命周期 = `git mv`：`backlog/` → `schedule/<批次>/` → 交付后删正文、批次目录 `git mv` 进 `archive/`（只留 `PROGRESS.md`）。
- 四出口齐全：判不做 / 过期 → `dropped/`（追 `dropped:` + `dropped_at:`）· 合并 → `dropped/` + `merged_into:` · 批次内未完成 → 交付前 `git mv` 回 `backlog/` · 批次取消 → 全部回 `backlog/`、删批次目录。
- [MUST NOT] 引入 `picked` 等中间态；[MUST NOT] 直接删条目。
- 当轮诞生的需求可直接落 `schedule/`，但 [MUST] 同轮填 `modules` + 重生成清单（可见 + 过闸）。

## 条目 frontmatter（[MUST] 齐全）

```yaml
---
id: k3f9x2 # 6 位 base36 随机，[MUST NOT] 自增 / 日期前缀
title: 一句话标题
modules: [packaging] # 取 MODULES.md 领域名
created: 2026-10-02
parent: "" # 拆批 / 冻结期改需求时填父条目 id
---
```

`issue/` 条目只要 `id / title / created / from`，`modules` 由分诊方补。

## 并行与骨架

- 两个在途批次领域集合相交即不得并行（`dc-harness check` 机械判定）；同窗口串行连跑的批次在 `PROGRESS.md` frontmatter 写同一个 `window:` 豁免。
- 触及 `.claude-plugin/` [MUST] 在 `PROGRESS.md` 写明独占。

## 提交

- 显式 pathspec，[MUST NOT] `-a` / `-am` / `git add -A`；提交骨架文件前 `git diff --cached -- <file>` 逐 hunk 确认。
- 提交单位 = 一个自包含可验证的完整变更；[MUST NOT] 提 WIP。
- 改了 `backlog/` `issue/` `dropped/` `schedule/` `archive/` 的会话 [MUST] 同轮 `dc-harness lists` 并把清单一起提交。

## 收口（交付前 [MUST] 按序）

ⓐ 未完成条目 `git mv` 回 `backlog/` → ⓑ 刷项目快照 + 本目录 `SNAPSHOT.md` 对应行 → ⓒ 删条目正文、批次目录 `git mv` 进 `archive/`，`PROGRESS.md` 每条带交付 sha → ⓓ `dc-harness lists` → ⓔ `dc-harness check` 退 0 → ⓕ `claude plugin validate .` 退 0（插件清单落地后）。

快照改动可早于归档随交付笔落盘；[MUST NOT] 先归档、快照回头再补。

## issue 分诊（用户触发）

读 `issue/` 全部正文 → 实测定位根因 → 当轮 `git mv` 到 `schedule/`（补 `modules`）/ `backlog/` / `dropped/` + 重生成清单。[MUST NOT] 批次会话顺手分诊；[MUST NOT] 建回执 / 通知。

## 本仓专属

- `skills/` 下由 cli-skills 同步来的 CLI 类 skill [MUST NOT] 手改，改动回 done-coding-cli 提 issue。
- 改 `~/.claude` 体系层（如移除本机原版 skill）不在本仓批次内做，按全局规则另走 `~/.claude` 的 specs + Gate。
