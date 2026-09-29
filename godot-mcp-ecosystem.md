# Godot MCP 生态补充

> 补充 `godot-mcp.md` 之外的 Godot 生态工具，按痛点分类。痛点：单一插件不够用、RAG 文档问答、编辑器热操作。

## 1. godot-mcp-server v2（编辑器运行时控制，首选增强）

- 来源：`MingHuiLiu/Godot-MCP-Server`（v2.0，含 runtime）
- 安装：npx 启动服务 + Godot 4 项目内安装 MCP Bridge 插件（AssetLib 搜 MCP Bridge）
- 能力：42 核心 tools + 112 toolkit（runtime）：场景树读改、节点属性、脚本执行、导出、运行态控制
- 与现有 godot-mcp.md 的关系：同源不同版本，优先 v2 分支，支持 C#/.NET

## 2. Coding-Solo/godot-mcp（编辑/运行/调试一体化）

- 来源：`Coding-Solo/godot-mcp`
- 安装：pip install godot-mcp（stdio），Godot 编辑器需启用 Remote Inspector / 调试端口
- 能力：项目管理、打开/编辑/保存场景、运行与停止游戏、读取远程调试输出、截屏
- 适用：命令行驱动的持续开发工作流（适合 Codex 改壳客户端）

## 3. mcp_godot_rag（Godot 官方文档 RAG 问答）

- 来源：`weekitmo/mcp_godot_rag`
- 安装：git clone + pip install -r requirements.txt，配置 Godot 4 文档路径索引
- 能力：对 Godot 官方文档做向量检索问答，回答"这个 API 怎么用/参数是什么"
- 价值：配合引擎控制类 MCP 形成"问文档→改代码→跑起来"闭环

## 4. Godot Peek（轻量结构查看）

- 来源：社区（awesome-mcp-servers gaming 列表收录）
- 能力：只读查看场景树、节点属性、资源引用，用于 Agent 快速理解项目结构
- 适用：大项目冷启动，先 Peek 再动手

## 接入建议

| 场景 | 推荐 |
|------|------|
| 日常改场景/跑游戏 | godot-mcp-server v2 |
| CLI/脚本化工作流 | Coding-Solo/godot-mcp |
| API 用法不熟 | mcp_godot_rag |
| 项目结构速览 | Godot Peek |

## 安装汇总

```
npx godot-mcp-server            # v2 服务端
pip install godot-mcp           # Coding-Solo 版
git clone https://github.com/weekitmo/mcp_godot_rag
```
