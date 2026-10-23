# 判不做 / 已过期（DROPPED）

> 文档定位：快照型清单 · **[MUST] 由 `scripts/governance-lists.py` 重生成，[MUST NOT] 手工维护**
> **[MUST NOT] 直接删条目**——删掉会丢「为什么不做」，而那正是防同一需求反复被提的东西。

共 **3** 条。

| id | 标题 | 判不做理由 | 文件 |
|---|---|---|---|
| `0fmk8c` | 同步 @done-coding/cli-skills 进插件（锁版本 + 确定性改名），含跨仓 issue 收件仓注 | 不再需要：插件内容直接取 npm 发布的 @done-coding/cli-skills（Claude / Co | [0fmk8c-sync-cli-skills.md](dropped/0fmk8c-sync-cli-skills.md) |
| `gqk0pg` | 插件外壳与安装：plugin.json + marketplace.json，对外命名 /done-coding:* | 被 b8zi11 取代：本仓改为纯市场目录（双宿主 marketplace.json，插件来源 = npm @d | [gqk0pg-plugin-shell.md](dropped/gqk0pg-plugin-shell.md) |
| `gvrk4u` | 本地开发与验收闭环：--plugin-dir 日常加载、本地市场安装验收、validate 门禁 | 并入 b8zi11 批次：本地以目录作市场 + plugin validate + 临时配置目录安装实测即验收闭 | [gvrk4u-local-dev-loop.md](dropped/gvrk4u-local-dev-loop.md) |
