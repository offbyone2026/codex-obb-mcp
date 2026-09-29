# Cocos Creator MCP（2D/移动端国产引擎）

> 痛点：Cocos 是国内 2D/小游戏/移动端主力引擎之一，此前清单未覆盖。开源实现两个。

## 1. DaxianLee/cocos-mcp-server（主流选择，1300+ 星）

- 来源：`DaxianLee/cocos-mcp-server`
- 安装：npm 启动 MCP server + Cocos Creator 编辑器扩展（扩展商店搜 Cocos MCP 或手动导入）
- 能力：
  - 场景/节点层级读取与修改
  - 组件/属性操作（Transform、Sprite、UI 布局）
  - 资源管理（导入/查找/预览）
  - 项目结构与代码文件操作
- 适用：Cocos Creator 3.x，2D 小游戏、微信小游戏、休闲手游开发

## 2. RomaRogov/cocos-mcp（HTTP 版备选）

- 来源：`RomaRogov/cocos-mcp`
- 安装：编辑器内 HTTP server 扩展 + MCP client 配置
- 能力：编辑器内 HTTP 服务，节点/场景操作
- 价值：HTTP 协议便于跨进程/远程调试

## 接入建议

| 场景 | 推荐 |
|------|------|
| Cocos Creator 3.x 主开发 | DaxianLee/cocos-mcp-server |
| 需要远程/跨进程 | RomaRogov/cocos-mcp |

## 注意

- 编辑器扩展需在 Cocos Creator 中手动启用；版本匹配 3.x。
- 微信小游戏构建后运行在浏览器/真机预览，MCP 只控制编辑器态。
