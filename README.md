# Codex OBB MCP 工具库

本仓库收录 OffByOne Studio 多功能开发平台（Codex 改壳版）可用的 MCP 工具清单与安装配置。客户端 obb_agent.py 依据主仓 manifest.json 自动拉取本仓库内容。

覆盖范围：Godot / Unity / Unreal Engine / Steam / Blender 等游戏开发与发行相关 MCP server。

## 目录

| 文件 | 内容 |
|------|------|
| [godot-mcp.md](godot-mcp.md) | Godot 4.x 引擎控制 MCP（场景/脚本/节点/导出） |
| [unity-mcp.md](unity-mcp.md) | Unity 编辑器控制 MCP |
| [unreal-mcp.md](unreal-mcp.md) | Unreal Engine 5 编辑器控制 MCP |
| [steam-mcp.md](steam-mcp.md) | Steam 平台数据/发行相关 MCP |
| [blender-mcp.md](blender-mcp.md) | Blender 建模/贴图自动化 MCP |
| [mcp_servers.json](mcp_servers.json) | 汇总安装配置（可直接写入客户端 mcpServers） |

> 说明：所有 MCP 均为本地运行（stdio/HTTP），需在客户端本地安装对应引擎与依赖。
