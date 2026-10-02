# 领域模块目录（MODULES）

> 文档定位：设计视图 · 回答「有哪些领域、各自代码住哪儿」；现状见 `SNAPSHOT.md`。
> 本仓初始化时尚无代码，领域按已定需求的能力边界划分；落点出现后以 git 跟踪文件为准校正本表。

## 领域模块

| 领域 | 落点 | 职责 |
|---|---|---|
| `packaging` | `.claude-plugin/`（插件清单 / 市场清单）、同步脚本、`skills/` 下由 `@done-coding/cli-skills` 同步来的 CLI 类 skill | 插件外壳、安装与发布、CLI 类 skill 的同步与对外改名、本地开发与验收闭环 |
| `method` | `skills/workspace/`、`skills/search/` 及其随带的依赖文件 | 方法类 skill 的内容（自本机 `harness-workspace` / `harness-search` 迁入并去个人化） |

无横向（调度）领域。
