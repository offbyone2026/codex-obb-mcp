# Unreal MCP 生态补充

> 补充 `unreal-mcp.md` 之外的 Unreal 工具。痛点：280 命令主实现之外，需要 Python 脚本、轻量桥接、蓝图专项。

## 1. kvick-games/UnrealMCP（TCP/JSON，轻量协议）

- 来源：`kvick-games/UnrealMCP`
- 安装：Unreal 插件（C++/Editor）+ MCP server（stdin/stdout）
- 能力：通过 TCP/JSON 与编辑器通信，操作资产、场景、蓝图基础节点
- 价值：协议清晰、依赖少，适合作为第二个可用实现

## 2. GenOrca/Unreal-MCPython（Python 脚本控制）

- 来源：`GenOrca/Unreal-MCPython`
- 安装：Python 包 + Unreal Python Editor Script Plugin
- 能力：调用 Unreal Python API（unreal 模块），执行编辑器脚本、批量资产处理
- 适用：批处理、管线自动化（贴图重命名、资产校验、导出）

## 3. appleweed/UnrealMCPBridge（蓝图/编辑器桥）

- 来源：`appleweed/UnrealMCPBridge`
- 能力：编辑器内桥接 MCP，提供蓝图操作与场景控制
- 适用：蓝图为主的工作流

## 4. runeape-sats/unreal-mcp（社区备选）

- 来源：`runeape-sats/unreal-mcp`
- 能力：基础场景/资产操作，社区维护
- 价值：多一个兜底实现

## 接入建议

| 痛点 | 推荐 |
|------|------|
| 通用编辑操作 | kvick-games/UnrealMCP 或既有 280 命令实现 |
| Python 批处理管线 | GenOrca/Unreal-MCPython |
| 蓝图专项 | UnrealMCPBridge |

## 注意

- 各实现插件互不兼容，需按项目启用其中一个；启用后重启编辑器加载插件。
- UE5 首次加载插件耗时较长，MCP 连接超时属正常，可调大 timeout。
