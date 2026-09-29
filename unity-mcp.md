# Unity MCP（Unity 编辑器控制）

## 方案一：CoplayDev/unity-mcp（13.3k stars，MIT，C#）

AI 助手与 Unity Editor 之间的桥梁，内置 C# MCP 客户端 + MCP server，可管理资源、控制场景、编辑脚本、执行自动化任务。

- 仓库：https://github.com/CoplayDev/unity-mcp
- 特点：纯 C# 实现、无外部依赖、编辑器内 GUI 管理工具、支持多模型（Claude/OpenAI/Gemini 等）
- 工具覆盖：场景对象增删改查、资源导入/导出/查找、脚本读写、Play mode 控制、截图等

### 安装

1. 将 unity-mcp 目录放入项目的 `Packages/` 下（或用 UPM git URL 安装）
2. 首次进入 Unity 后通过 Window → Unity MCP → Settings 配置模型端点（支持 OpenAI 兼容接口）
3. 在 Settings 中复制配置 JSON 写入客户端 mcpServers

## 方案二：AnkleBreaker-Studio/unity-mcp-server（268 tools）

基于 C# 的 Unity 编辑器 MCP server，提供更细粒度的编辑器操作工具集（268 个工具），适合深度自动化。

- 仓库：https://github.com/AnkleBreaker-Studio/unity-mcp-server
- 覆盖：GameObject/Component 全量操作、资源管线、场景管理、输入模拟、运行态控制

## 统一 mcpServers 配置示例

```json
{
  "mcpServers": {
    "unity": {
      "command": "node",
      "args": ["<unity-mcp-server 路径>/dist/index.js"]
    }
  }
}
```
