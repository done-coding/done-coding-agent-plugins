# done-coding-agent-plugins

done-coding 的 AI 编码工具**插件市场**：只放市场目录，插件内容来自 npm 发布的包，Claude Code 与 Codex 共用。

| 插件 | 内容来源 | 提供的 skill |
|---|---|---|
| `done-coding` | npm [`@done-coding/cli-skills`](https://www.npmjs.com/package/@done-coding/cli-skills)（`latest`） | `create-done-coding` 用模板建项目 · `cli-generator` 具名批次生成 · `module-generate` 模块模板生成 · `cli-harness` 治理清单 / 治理闸 / 跨仓 issue |

## 安装

**Claude Code**（会话内）：

```
/plugin marketplace add done-coding/done-coding-agent-plugins
/plugin install done-coding@done-coding
```

**Codex**：

```bash
codex plugin marketplace add done-coding/done-coding-agent-plugins
codex plugin add done-coding@done-coding
```

装好后 skill 以 `done-coding:<名>` 出现，AI 按任务自动选用。skill 内调用的 CLI 走已装命令或 `npx`，无需另装。

## 更新

插件不钉版本，取 npm `latest`：`@done-coding/cli-skills` 发新版后，Claude 用 `/plugin` 更新插件，Codex 用 `codex plugin marketplace upgrade` 后重装。

## 注意

- 同一 skill 不要既装插件、又放进 `~/.claude/skills` / `~/.agents/skills`（如用 `dc-cli-skills install` 装过）：两者同时加载会让 AI 选择歧义。装插件前先删掉目录里的同名 skill。
- 新增插件 = 在 `.claude-plugin/marketplace.json`（Claude）与 `.agents/plugins/marketplace.json`（Codex）各加一条，来源指向已发布的 npm 包；本仓不放 skill 内容。
