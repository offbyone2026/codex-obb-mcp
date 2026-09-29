# Steam 生态与发行运营 MCP 补充

> 补充 `steam-mcp.md` 之外的发行/运营工具。痛点：Steamworks 后台操作、评测分析、itch.io 参展、游戏数据库。

## 1. TMHSDigital/steam-mcp（25 工具，含写操作）

- 来源：`TMHSDigital/steam-mcp`
- 安装：npm/uv 安装 + Steam API key（读取）与 Publisher key（写操作）
- 能力（18 读 + 7 写）：
  - 商店数据、玩家统计、评测、定价
  - 成就、排行榜、工坊、库存、大厅
  - 写操作：SetUserStats、SetLeaderboardScore、AddItem 等（需 Publisher key）
  - Partner 管理工具（steamPartnerLogin、uploadStoreImage、uploadTrailer）本地使用
- 适用：发行商侧运营（成就下发、排行榜写入、商店素材上传）
- 注意：无 Publish 工具；Partner 工具需本机 Chromium profile

## 2. exi/mcp-steam（Steam 平台集成）

- 来源：`exi/mcp-steam`
- 能力：Steam 用户信息、游戏库、商店页查询
- 适用：玩家侧数据（竞品分析、自家游戏可见性检查）

## 3. steam-review-mcp（评测分析）

- 来源：`fenxer/steam-review-mcp`
- 能力：按游戏拉取 Steam 评测并做情绪/主题分析
- 适用：发行后差评监控、竞品口碑调研

## 4. itch-jams-mcp（itch.io 游戏 jams）

- 来源：`petrarka/itch-jams-mcp`
- 能力：直接爬取 itch.io 浏览/搜索 Game Jams，无需 API key
- 适用：找参赛窗口、做市场热度调研、42 小时冲刺

## 5. gamebrain-api-clients（GameBrain 游戏数据库）

- 来源：`ddsky/gamebrain-api-clients`
- 能力：跨平台游戏元数据查询（发行日、平台、评分）
- 适用：市场调研、竞品数据、发行窗口选择

## 接入建议

| 痛点 | 推荐 |
|------|------|
| Steamworks 运营写操作 | TMHSDigital/steam-mcp |
| 评测/口碑监控 | steam-review-mcp |
| itch.io 参展/jams | itch-jams-mcp |
| 游戏元数据/市场调研 | gamebrain-api-clients |

## 与既有技能配合

- 发行流程走 `steam-release` 技能；运营数据由 TMHS steam-mcp 落地执行。
- 评测分析结果喂给 `playtesting` 技能的问题分级。

## 注意

- 写操作类工具（SetUserStats 等）只应用于自家游戏，误写他人游戏会被 Steam 封 Publisher key。
- Partner 工具不走标准 MCP bin，需本地 Steamworks 登录态，接入时单独配置。
