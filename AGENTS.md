# AI 指令 — done-coding-agent-plugins

done-coding 的 AI 编码工具**插件市场目录**（Claude Code 与 Codex 共用）：`.claude-plugin/marketplace.json` + `.agents/plugins/marketplace.json` 两份目录，插件内容来源 = npm 已发布的包（`done-coding` 插件 ← `@done-coding/cli-skills`）。本仓不放 skill 内容。

> 指令文件约定：规则正文只写 `AGENTS.md`；同级 `CLAUDE.md` 只含 `@AGENTS.md`，[MUST NOT] 往 `CLAUDE.md` 写规则。

## 命令

| 命令 | 作用 |
|---|---|
| `dc-harness lists` | 重生成治理清单 |
| `dc-harness check` | 治理闸（退 0 = 通过） |

## 开发模式（harness-workspace）

- 治理目录 `docs/governance/`（纪律见其 `AGENTS.md`）；现状入口 = `docs/BUSINESS_SNAPSHOT.md` + `docs/TECH_SNAPSHOT.md` + `docs/governance/SNAPSHOT.md`。
- **领域**：`packaging`（两份市场目录与插件条目）/ `method`（方法类 skill，待定），以 `docs/governance/MODULES.md` 为唯一真源。
- **批次单 = AI 开发窗口的最小接入单元**：一张单含 N 个领域，一张单 = 一个会话 = 一次交付。单领域批次只是 N=1，[MUST NOT] 据此开「领域会话」。
- **批次串**：一个窗口串行做完的几批——每批任务表末项写「交付后立即开始下一批 `<id>`」，串末写收工。接到串首 id 就一路做到串末，[MUST NOT] 交付一批就停下等人派单。
- 外部仓反馈只进 `docs/governance/issue/`，分诊由用户触发；改了治理目录 [MUST] 同轮 `dc-harness lists`。

### 承接批次 = 自带推理义务

需求入池前已经过对话澄清，条目正文 + 快照 + 契约三者齐备。**细节差异 [MUST] 自行推理补齐，[MUST NOT] 事无巨细一步一问。**
进度 [MUST] 随手写进本批次 `PROGRESS.md`，[MUST NOT] 把状态攒在上下文里。

### 只有四种情形可以停，其余都是偷懒

ⓐ **缺权限**：破坏性写 / 不可逆动作 / push / 扩大对外暴露面（授权在册 ≠ 执行许可，[MUST] 有当轮授权）。
ⓑ **前提塌了**：需求前提不成立或与既有契约冲突 → [MUST] 带证据报告，[MUST NOT] 猜一个继续。
ⓒ **缺资源**：缺凭据 / 环境 / 外部服务等自己拿不到的东西。
ⓓ **交付完成**：未完成条目已清回池 / 快照已刷 / 批次目录已归档 / 交付 commit 含快照改动 / 清单重生成零 diff。

> 真歧义可停：不同理解导致**实质不同的实现**，且读遍代码 / 快照 / 契约 / git 仍判不定。查得到的、推得出的都不算。

## 硬规则

1. [MUST] 插件内容一律来自已发布的 npm 包，本仓 [MUST NOT] 拷贝或手改 skill；skill 改动回所属包的仓库（如 done-coding-cli）提 issue。
4. [MUST] 两份市场目录（Claude / Codex）的插件条目保持一一对应（同名、同来源）；新增 / 改动时两边同改，并以 `claude plugin validate .` 及两宿主本地安装实测验收。
2. [MUST] 插件内容 [MUST NOT] 含个人 / 业务信息（本机路径、私人目录、账号）——仓库公开。
3. [MUST] 改全局体系（`~/.dotfiles`）不在本仓批次内做，向其 issue 收件箱提。
