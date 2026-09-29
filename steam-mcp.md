# Steam MCP（Steam 平台数据/发行）

## 方案一：sandraschi/steam-mcp（14 tools，推荐主力）

基于 uv 启动、HTTP 服务（默认 localhost:11020），读取 Steam 平台数据，适合账号资料、库存、成就与工坊查询。

```bash
uvx steam-mcp
```

```json
{
  "mcpServers": {
    "steam": { "command": "uvx", "args": ["steam-mcp"] }
  }
}
```

工具分类（14 tools）：
- Profile：玩家档案、好友列表、最近游玩
- Library：游戏库、游戏详情、可玩状态
- Stats：成就列表与解锁状态
- Store & News：商店应用信息、价格、新闻/更新
- Workshop：创意工坊订阅、收藏

## 方案二：TMHSDigital/Steam-MCP（26 tools，含写操作）

分三组：
- No-Auth（11）：公共档案、游戏库、成就、商店数据
- API Key（8）：需要 Steam Web API Key 的高级查询
- Publisher（7）：发行商后台操作（需要发行商权限），覆盖营销素材、折扣、捆绑包、直播频道管理

适合 OffByOne Studio 作为 Steam 发行商后的运营自动化。

## 方案三：chaosman42/steam-mcp（15 tools，Python）

轻量 Python 实现，聚焦玩家数据与库信息，便于本地集成。

## 选型建议

- 查询/账号侧：方案一（零配置）+ 方案二 No-Auth 组
- 发行运营侧：方案二 Publisher 组（游戏上架、折扣、素材管理）
