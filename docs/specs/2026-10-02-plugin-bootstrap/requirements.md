# 需求文档：done-coding Claude Code 插件（首版）

> 文档定位：快照型 · 状态：**待确认** · 日期：2026-10-02 · 等级：Moderate
> 来源：用户 2026-10-02 定调（hub 会话讨论）

## 背景

done-coding 生态的 Agent Skill 现分散两处：

- **CLI 类**：源头在 done-coding-cli 的 `@done-coding/cli-skills`（`cli-harness` / `create-done-coding` / `cli-generator` / `module-generate`），经 `dc-cli-skills install` 拷进 `.claude/skills/`；skill 内命令走 `npx <cli>@latest`，对 CLI 零运行时依赖。
- **方法类**：`~/.claude/skills/harness-*` 等，只在本机；18 个本机 skill 中 13 个引用 `~/.claude/` 下的 knowledge / protocols / contracts / templates / flows 等文件，换一台机器即失效。

用户定调（原话）：「done-coding-skill 只管自身的，done-coding-claude 则还有其他的，其可以再安装 done-coding-cli 后依赖包装为自身的，对外界是透明的」。

目标：一个可公开安装的 Claude Code 插件 `done-coding`，装上即得 CLI 类能力（一句话让 AI 建项目、治理工具、跨仓 issue）与 workspace / search 两个方法，调用形如 `/done-coding:<skill>`。

## REQ-1：插件外壳与安装

THE SYSTEM SHALL 把本仓做成 Claude Code 插件 + 插件市场：

- 插件名 `done-coding`；仓库公开（远端与首次 push 另行授权）；
- 用户经 `/plugin marketplace add <本仓地址>` + `/plugin install done-coding@<市场名>` 安装，无需预装 done-coding-cli 或任何 npm 包；
- 验收：在隔离的 Claude 配置目录（不含本机 `~/.claude/skills`）中按上述两步安装成功，`/done-coding:` 下列出全部首版 skill。

## REQ-2：CLI 类 skill 由 cli-skills 包装进来（对外透明）

THE SYSTEM SHALL：

- 以 `@done-coding/cli-skills` 为 CLI 类 skill 的**唯一源头**，本仓锁定其版本，经同步脚本在**发布前**把其 `skills/` 拷入插件目录并提交；本仓 [MUST NOT] 手改这些拷贝；
- 用户安装插件时不执行任何 npm 安装（插件安装 = 克隆仓库）；
- 同步时按 REQ-7 确定性改名（源头 cli-skills 命名不动）；建项目 skill 以 cli 并入 x-create 推断规则后的 `create-done-coding` 为准（cli issue `ff5p5s`）；
- 验收：同步脚本重跑零 diff；插件内 CLI 类 skill 与所锁版本 cli-skills 的 `skills/` 内容一致，差异仅限 design 阶段约定的确定性改写（改名、`@latest` → 固定版本等）。

## REQ-3：方法类 skill 只迁两个

THE SYSTEM SHALL 首版只迁入 `harness-workspace`、`harness-search`（用户 2026-10-02 定）；迁移 [MUST] 逐条重过判据（对任意项目成立、不含个人 / 业务信息、依赖文件可随插件打包），[MUST NOT] 因「原来就这么写」整搬。

- 其余本机 skill 首版不进；`x-create` 候选由 cli-skills 承接，不在本仓。
- 命名见 REQ-7（去 `harness-` 前缀）。
- 验收：两个 skill 在 design 中有逐条判据结论；插件内容 grep 不到个人路径 / 私人目录名。

## REQ-4：依赖文件随插件打包

THE SYSTEM SHALL 把迁入 skill 引用的 knowledge / protocols / templates 等文件按需带入插件，引用改为相对 skill 自身目录（或插件根），只带被引用的部分。

- 验收：插件内零 `~/.claude/` 读依赖；在 REQ-1 的隔离环境中各 skill 引用的文件均可读到。

## REQ-6：跨仓 issue 收件仓注册（经 cli-harness 透出）

用户定调：会有多个 monorepo 级项目并行启动，持续向 done-coding-cli / admin / template-hub 反馈 issue，这是当前最迫切的能力。

THE SYSTEM SHALL 让插件用户在任一项目里能查到「哪些仓接收 issue、各自受理什么、收件箱在哪」，并据此 `dc-harness issue` 提交：

- 能力本体由 done-coding-cli 实现（backlog `qdoeql`，经 issue `ff5p5s` 提优先级：`~/.done-coding/harness/scope/` 成员仓注册 / 列表 / 路径校验；手工注册表已于 2026-10-02 建立，即格式样本），经 cli-skills 的 `cli-harness` skill 按 REQ-2 进入插件；本仓不另实现；
- 前置：`@done-coding/cli-harness` 已发布到 npm（2026-10-02 实测 404，skill 的 `npx` 入口不可用）。
- 验收：隔离环境装插件后，经 `/done-coding:harness` 能列出已注册收件仓并向其中一个成功提 issue。

## REQ-7：对外命名

THE SYSTEM SHALL 以插件命名空间 `done-coding:` 承担归属，skill 名 [MUST NOT] 再带 `dc-` / `done-coding` / `harness-` 冠名（用户 2026-10-02 定）：

| 插件指令 | 来源 |
|---|---|
| `/done-coding:create` | cli-skills `create-done-coding`（并入 x-create 推断规则后） |
| `/done-coding:harness` | cli-skills `cli-harness`（清单 / 治理闸 / issue / scope） |
| `/done-coding:search` | 本机 `harness-search` |
| `/done-coding:workspace` | 本机 `harness-workspace` |

- cli-skills 其余 skill 按同一判据去冗余（如 `cli-generator` → `generator`），design 阶段列全；
- CLI 二进制名（`dc-harness` 等）在系统 PATH 共享空间，保留 `dc-` 前缀，不受本条约束；
- skill 正文中互相引用的名字随之改写；
- 验收：插件内 skill 目录名与上表一致；能否省略 `done-coding:` 前缀直接调用，design 阶段实测记录。

## 范围外

- 全局 CLAUDE.md 初始化（原 REQ-5）：首版不做，后续版本再议。
- 其余本机方法类 skill（首版只迁两个，见 REQ-3）。
- 本机 `~/.claude/skills` 原版的移除：属 `~/.claude` 体系层改动，插件实装验证后按全局规则另走 `~/.claude` 的 specs + Gate。
- 发布到官方插件市场；Codex / Cursor 等多平台适配（YAGNI）。
- done-coding-cli 清理 cli-ai / cli-mrm：已提 issue `6w35pj`，与本 spec 无依赖。
- 本仓工程骨架（lint / 提交钩子 / 同步脚本语言）在 design 阶段定；hub 现无「Claude 插件仓」模板，不为单仓新建模板。

## 依赖与顺序

首版交付依赖 done-coding-cli 三件事（均在 issue `ff5p5s`）：ⓐ 发布 `@done-coding/cli-harness`；ⓑ 实现 `qdoeql`；ⓒ `create-done-coding` 并入 x-create 推断规则。未完成前，本仓可先完成 REQ-1 / REQ-3 / REQ-4 / REQ-7。

## 待用户确认

ⓐ 远端放哪（GitHub `done-coding` 组织 / gitee）。
