---
harness-workspace: initialized
initialized: 2026-10-02
tier: medium-lite   # 中档精简：backlog / dropped / schedule / archive / issue，无 modules/
issue-inbox: enabled
scheduling-domain: none
---

# 治理总纲 — done-coding-agent-plugins

本目录按 harness-workspace 组织：**需求单态**（一条需求正文只在一个文件里，生命周期靠 `git mv` 表达）、**清单与正文分离**（清单由 `dc-harness lists` 生成）、**批次 = 一会话 = 一次交付**。

## 文档职责

| 文档 / 目录 | 职责 | 维护方式 |
|---|---|---|
| `AGENTS.md` | 指令层：批次 / 并行 / 提交纪律 | 手写，按规则更新协议改 |
| `MODULES.md` | 领域清单（唯一真源，`dc-harness check` 从此解析合法 `modules`） | 新增落点时同批改 |
| `SNAPSHOT.md` | 治理视图：每领域一行 + 依赖 + 独占点 | 交付时同笔更新 |
| `../BUSINESS_SNAPSHOT.md` / `../TECH_SNAPSHOT.md` | 项目全貌 | 交付时同笔更新 |
| `BACKLOG.md` `SCHEDULE.md` `ARCHIVE-DONE.md` `ISSUE.md` `DROPPED.md` | 清单（无正文） | **仅** `dc-harness lists` 生成，[MUST NOT] 手改 |
| `backlog/` | 需求池：`<id>-<slug>.md` | 任何会话可新建 |
| `issue/` | 外部仓反馈收件箱（唯一状态 = 未分诊） | 外部仓写入；分诊由用户触发 |
| `dropped/` | 判不做 / 过期 / 被合并（带 `dropped:` 理由） | `git mv` 进入，[MUST NOT] 删 |
| `schedule/<批次id>-<slug>/` | 在途批次：`PROGRESS.md` + 条目正文 | 下发时建，交付时移走 |
| `archive/<批次id>-<slug>/` | 已交付批次：仅 `PROGRESS.md` | 交付时 `git mv` 进入 |

## 初始化标记

- 本 README frontmatter 即初始化标记；重跑初始化走增量补缺，[MUST NOT] 覆盖活资产。
- 调度领域：**无**。

## 外部仓怎么提反馈

在本仓根外执行 `dc-harness issue <本仓根> -t "<一句话>" -s <slug> -b <正文.md>`（写 issue 文件 + 重生成 `ISSUE.md` + 只提交这两个文件）。正文写**现象 + 复现路径**，`modules` 不填；[MUST NOT] 改本仓其他文件、[MUST NOT] 等回执。结果看 `ISSUE.md` / `DROPPED.md`。
