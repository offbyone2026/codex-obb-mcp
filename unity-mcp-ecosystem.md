# Unity MCP 生态补充

> 补充 `unity-mcp.md` 之外的 Unity 工具。痛点：CoplayDev 版覆盖不全、需要 C# 脚本执行、性能/体积敏感。

## 1. unityctl（179 命令，最全命令行面）

- 来源：社区（awesome-mcp-servers gaming 列表收录）
- 安装：npm 包 + Unity Editor 侧插件（TCP 通信）
- 能力：179 命令，覆盖 Scene/GameObject/Asset/Editor 菜单/播放模式/批处理
- 适用：追求命令面最大覆盖的自动化

## 2. UnityCode MCP（Rust 实现，轻量高性能）

- 来源：`hackerzhuli/UnityCodeMCP`（Rust）
- 安装：预编译二进制 + Unity 侧 TCP server 插件
- 能力：执行 C# 代码片段、读取控制台日志、场景/组件操作
- 价值：Rust 实现无 Node 依赖，启动快、内存小，适合常驻

## 3. UnityCodeMCPServer（C# 脚本即写即跑）

- 来源：`Signal-Loop/UnityCodeMCPServer`
- 能力：向 Unity 注入并执行 C# 脚本、获取返回值、编辑器菜单调用
- 适用：测试驱动开发，Agent 直接写 C# 断言场景状态

## 4. MCP4Unity（轻量备选）

- 来源：`Purisky/MCP4Unity`
- 能力：场景/资产/脚本基础操作，结构简单易审查
- 适用：仅需基础操作的场景

## 5. IvanMurzak/Unity-MCP（老牌稳定）

- 来源：`IvanMurzak/Unity-MCP`
- 能力：Editor 侧 Python/Node 双实现，场景/资产/游戏对象管理
- 价值：社区久、issue 少，可作兜底

## 接入建议

| 痛点 | 推荐 |
|------|------|
| 命令面最大 | unityctl |
| 轻量常驻/性能敏感 | UnityCode MCP（Rust） |
| 跑 C# 测试/断言 | UnityCodeMCPServer |
| 基础操作/稳定兜底 | IvanMurzak/Unity-MCP 或 MCP4Unity |

## 注意

- 各实现插件与 MCP server 的端口/TCP 协议不同，同一编辑器实例一次只挂一个 server，避免端口冲突（默认 8765 / 8080 / 13000 不一）。
- Unity 批处理模式（-batchmode）下部分插件不可用，需人工确认。
