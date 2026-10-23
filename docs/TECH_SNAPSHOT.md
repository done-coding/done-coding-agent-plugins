# TECH_SNAPSHOT — done-coding-agent-plugins

> 文档定位：快照型 · 覆盖更新、只写当前状态。

## 结构

```
.claude-plugin/marketplace.json     Claude Code 市场目录（name: done-coding）
.agents/plugins/marketplace.json    Codex 市场目录（name: done-coding）
```

无代码、无依赖、无构建，不发布 npm。两份目录的插件条目一一对应：插件 `done-coding`，`source = { "source": "npm", "package": "@done-coding/cli-skills" }`，不钉版本（取 `latest`）。

## 关键事实（2026-10-23 实测：Claude Code 2.1.283、Codex 0.162.1）

- 两宿主均支持 npm 插件来源：安装时拉取 npm 包、不执行 install 脚本，插件根下 `skills/` 即 skill。
- 包内无插件清单时：Claude 以市场条目为清单（`claude plugin list` 显示 `Version: unknown`）；Codex 自动生成 `.codex-plugin/plugin.json`。
- Codex 安装后可用 skill 为 `done-coding:cli-generator` 等 4 项；Claude 安装成功、已启用，插件缓存含 4 个 skill。
- 插件名 `done-coding` 即 skill 命名空间前缀；市场名 `done-coding`，安装 id `done-coding@done-coding`。

## 验收方式

`claude plugin validate .`；以本地目录作市场，在临时 `CLAUDE_CONFIG_DIR` / `CODEX_HOME` 中 marketplace add + 安装，Codex 用 `codex exec` 列出 `done-coding:` 前缀 skill。
