# BUSINESS_SNAPSHOT — done-coding-agent-plugins

> 文档定位：快照型 · 覆盖更新、只写当前状态。

## 定位

done-coding 的 AI 编码工具**插件市场目录**：让 Claude Code 与 Codex 用各自的插件命令装上 done-coding 的 skill，与 superpowers 等第三方插件同一生态位。本仓只维护「有哪些插件、各从哪来」，插件内容来自 npm 已发布的包。

## 插件

| 插件 | 来源 | 提供 |
|---|---|---|
| `done-coding` | npm `@done-coding/cli-skills`（`latest`） | `create-done-coding` · `cli-generator` · `module-generate` · `cli-harness`（宿主内以 `done-coding:<名>` 出现） |

## 使用方

- 个人机器：Claude `/plugin marketplace add done-coding/done-coding-agent-plugins` + `/plugin install done-coding@done-coding`；Codex `codex plugin marketplace add …` + `codex plugin add done-coding@done-coding`（见 README）。
- dotfiles 作为使用方，只在各宿主配置里声明市场与启用的插件，本仓不感知 dotfiles。

## 待定

- 方法类 skill（harness-workspace / harness-search）是否以插件形式经本市场分发（backlog `hd8ue4`，需用户裁决；现由 dotfiles 统一维护）。
