# 需求文档：done-coding Claude Code 插件（首版）

> 文档定位：快照型 · 状态：**待确认** · 日期：2026-10-02 · 等级：Moderate
> 来源：用户 2026-10-02 定调（hub 会话讨论）

## 背景

done-coding 生态的 Agent Skill 现分散两处：

- **CLI 类**：源头在 done-coding-cli 的 `@done-coding/cli-skills`（`cli-harness` / `create-done-coding` / `cli-generator` / `module-generate`），经 `dc-cli-skills install` 拷进 `.claude/skills/`；skill 内命令走 `npx <cli>@latest`，对 CLI 零运行时依赖。
- **方法类**：`~/.claude/skills/harness-*` 等，只在本机；18 个本机 skill 中 13 个引用 `~/.claude/` 下的 knowledge / protocols / contracts / templates / flows 等文件，换一台机器即失效。

用户定调（原话）：「done-coding-skill 只管自身的，done-coding-claude 则还有其他的，其可以再安装 done-coding-cli 后依赖包装为自身的，对外界是透明的」。

目标：一个可公开安装的 Claude Code 插件 `done-coding`，装上即得项目创建、harness 系列方法、全局 CLAUDE.md 初始化等能力，调用形如 `/done-coding:<skill>`。

## REQ-1：插件外壳与安装

THE SYSTEM SHALL 把本仓做成 Claude Code 插件 + 插件市场：

- 插件名 `done-coding`；仓库公开（远端与首次 push 另行授权）；
- 用户经 `/plugin marketplace add <本仓地址>` + `/plugin install done-coding@<市场名>` 安装，无需预装 done-coding-cli 或任何 npm 包；
- 验收：在隔离的 Claude 配置目录（不含本机 `~/.claude/skills`）中按上述两步安装成功，`/done-coding:` 下列出全部首版 skill。

## REQ-2：CLI 类 skill 由 cli-skills 包装进来（对外透明）

THE SYSTEM SHALL：

- 以 `@done-coding/cli-skills` 为 CLI 类 skill 的**唯一源头**，本仓锁定其版本，经同步脚本在**发布前**把其 `skills/` 拷入插件目录并提交；本仓 [MUST NOT] 手改这些拷贝；
- 用户安装插件时不执行任何 npm 安装（插件安装 = 克隆仓库）；
- 验收：同步脚本重跑零 diff；插件内 CLI 类 skill 与所锁版本 cli-skills 的 `skills/` 逐字节一致（或仅含 design 阶段约定的确定性改写，如 `@latest` → 固定版本）。

## REQ-3：方法类 skill 迁入（逐条重判）

THE SYSTEM SHALL 把本机方法类 skill 中**通用、可公开**者迁入插件；迁移 [MUST] 逐条重过判据，[MUST NOT] 因「原来就这么写」整搬：

- 判据：ⓐ 对任意项目成立（非个人用途）；ⓑ 不含个人 / 业务信息（路径、仓名、账号、私人目录）；ⓒ 依赖文件可随插件打包。
- 初判（design 阶段逐条复核，用户可否决）：

| 初判 | skill |
|---|---|
| 进插件 | `harness-workspace`、`harness-search`、`harness-foresight`、`harness-setup`、`harness-prune`、`harness-handoff`、`harness-sbar`、`ready-compact`、`harness-refactor`、`harness-split`、`harness-codex`、`harness-debug` |
| 待定（依赖个人治理体系较重） | `harness-rebuke`（11 处 `~/.claude` 引用）、`test-ui`（依赖本机 cdp-ui 脚本）、`harness-teacher` |
| 留本机 | `juejin-article`（个人发文流程） |
| 另议 | hub 项目级 `x-create`（依赖 hub 本机清单，候选并入 CLI 类，由 cli-skills 承接） |

- 命名：保留 `harness-` 前缀（区分方法族与 CLI 族；去冗余规则只针对 `done-coding` 冠名，插件前缀已提供 `done-coding:`）。
- 验收：每个迁入 skill 在 design 中有判据结论；插件内容 grep 不到个人路径 / 私人目录名。

## REQ-4：依赖文件随插件打包

THE SYSTEM SHALL 把迁入 skill 引用的 knowledge / protocols / templates 等文件按需带入插件，引用改为相对 skill 自身目录（或插件根），只带被引用的部分。

- 验收：插件内除 REQ-5 明确写入的 `~/.claude/CLAUDE.md` 外，零 `~/.claude/` 读依赖；在 REQ-1 的隔离环境中各 skill 引用的文件均可读到。

## REQ-5：全局 CLAUDE.md 初始化

THE SYSTEM SHALL 提供一个 skill，把 done-coding 通用的全局偏好写入用户的 `~/.claude/CLAUDE.md`：

- **合并不覆盖**：只写入 / 更新标记块内的内容，块外用户内容一字不动；重复执行幂等；
- 写入前展示将写入的内容与 diff，经用户确认再落盘；
- 内容取自现有全局 CLAUDE.md 的**通用部分**（去个人化后逐条重判）。
- 验收：对「不存在 / 空 / 已有用户内容 / 已有旧版标记块」四种初始状态各执行两次，块外内容不变、第二次零变更。

## 范围外

- 本机 `~/.claude/skills` 原版的移除：属 `~/.claude` 体系层改动，插件实装验证后按全局规则另走 `~/.claude` 的 specs + Gate。
- 发布到官方插件市场；Codex / Cursor 等多平台适配（YAGNI）。
- done-coding-cli 清理 cli-ai / cli-mrm：已提 issue `6w35pj`，与本 spec 无依赖。
- 本仓工程骨架（lint / 提交钩子 / 同步脚本语言）在 design 阶段定；hub 现无「Claude 插件仓」模板，不为单仓新建模板。

## 待用户确认

ⓐ REQ-3 初判表（尤其「待定」三项与 `x-create` 去向）；
ⓑ REQ-5 内容来源是否就是现有全局 CLAUDE.md 的通用部分；
ⓒ 远端放哪（GitHub `done-coding` 组织 / gitee）。
