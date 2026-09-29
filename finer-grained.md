# 精细化 MCP 工具清单

目的：把“大而全”的引擎 MCP 拆成**按子系统细粒度启用**的工具子集，控制上下文预算（每个 MCP 的工具 schema 都会占用上下文），同时补充素材/视频方向的精细工具。客户端按 manifest 拉取后，可按子集开关启用，避免一次性挂载所有工具。

## 一、既有 5 大 MCP 的细粒度子集

按 `mcp_servers.json` 的 category 字段拆分，可只启用当前任务需要的子集：

### Godot MCP（42 tools，npm `godot-mcp-server`，端口 9080）
| 子集 | 覆盖工具 | 适用任务 |
|------|----------|----------|
| scene | 场景树/节点操作 | 搭场景、改节点 |
| script | GDScript 读写/运行 | 写脚本、调试 |
| project | 项目配置/导入 | 工程设置、资源导入 |
| asset | 资源管理 | 素材整理、导入导出 |
| visualization | 编辑器可视化 | 截图、视口控制 |

### Unreal MCP（280 命令，pip `unrealmcp`，TCP 55557）
| 子集 | 适用任务 |
|------|----------|
| asset | 资产操作（导入/重定向/批量） |
| blueprint | 蓝图编辑/节点操作 |
| material | 材质/贴图参数 |
| datatable | 数据表 CRUD |
| actor | Actor 放置/变换/组件 |
| niagara | Niagara 粒子系统 |
| statetree | 状态树/AI 状态 |
| input | 输入映射/增强输入 |
| umg | UI 控件/UMG |
| profiling | 性能剖析/统计 |

### Blender MCP（157 tools，`uvx mcp-for-blender`，socket 9876）
| 子集 | 适用任务 |
|------|----------|
| mesh | 建模/拓扑/网格操作 |
| material | 材质节点/属性 |
| texture | 贴图/UV |
| scene | 场景/相机/灯光/集合 |
| render | 渲染/合成/Eevee-Cycles |

### Steam MCP（14 tools，`uvx steam-mcp`，端口 11020）
| 子集 | 适用任务 |
|------|----------|
| profile | 个人资料/好友 |
| library | 游戏库/启动 |
| stats | 成就/统计 |
| store | 商店信息/价格 |
| workshop | 创意工坊 |

### Unity MCP（40 tools，CoplayDev/unity-mcp）
| 子集 | 适用任务 |
|------|----------|
| scene | 场景/层级 |
| asset | 资源/导入 |
| script | C# 脚本编辑 |
| automation | 批量操作/构建 |

## 二、新增精细方向 MCP（v1.2.0 引入）

| MCP | 方向 | 能力摘要 | 文档 |
|-----|------|----------|------|
| **sora** | 视频生成 | OpenAI Sora 2 官方 API：文生视频/图生视频/remix/状态轮询/下载/列表/删除 | [sora-mcp.md](sora-mcp.md) |
| **ludo** | AI 素材全栈 | 精灵/图标/UI/贴图、图转 GLB+PBR、自动绑定、spritesheet 动画、短视频、音效/BGM/配音/TTS、异步任务队列 | [ludo-mcp.md](ludo-mcp.md) |

## 三、上下文预算管理建议

1. **按需启用**：客户端 `obb_agent.py` 拉取清单后，在 Codex config.toml 中按任务类型启用对应 server，闲置的 `enabled = false`；
2. **子集化路由**：大 MCP（如 Blender 157 tools）在 SKILL.md 指令中只点名所需工具组，其余不调用；
3. **技能先行**：用 `skills/` 仓的 SKILL.md 做路由层（description 触发），SKILL.md 内部再指明用哪个 MCP 子集，避免 Agent 盲目遍历全部工具；
4. **配额提醒**：Ludo 异步任务需先查余额；Sora 生成为付费 API 调用，长任务建议先 5s 测试帧再上 20s 正式帧。
