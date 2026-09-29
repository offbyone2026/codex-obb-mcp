# Godot MCP（Godot 4.x 引擎控制）

## 方案一：godot-mcp-server（npm，推荐）

MCP server 通过 stdio 与 Godot 编辑器内的 MCP Bridge 插件（HTTP localhost:9080）通信，可直接读写场景、节点、脚本与资源。

- 仓库：`ricky-yosh/godot-mcp-server`（Godot 4 项目场景/节点/脚本/资源读写）
- 更完整实现：`Raunaksplanet/godot-mcp-server`（40+ tools，场景操作/脚本/文件 I/O/项目设置/信号/导出/插件，WebSocket localhost:9080）
- npm 发行版：`godot-mcp-server@0.5.0`（42 tools，6 类：文件操作 4、场景操作 11、脚本操作 6、项目工具 14、资源生成 1、可视化 6）

### 安装配置

```json
{
  "mcpServers": {
    "godot": {
      "command": "npx",
      "args": ["-y", "godot-mcp-server"],
      "env": { "GODOT_PORT": "9080" }
    }
  }
}
```

插件：Godot AssetLib 搜索 "mcp" → 安装 "Godot AI Assistant tools MCP" → Project Settings → Plugins 启用。

### 工具清单（42 tools 摘要）

- 场景操作：godot_create_scene / godot_load_scene / godot_save_scene / godot_get_scene_tree / godot_add_node / godot_remove_node / godot_reparent_node / godot_duplicate_node / godot_instantiate_scene
- 属性操作：godot_set_property / godot_get_property
- 脚本操作：godot_create_script / godot_read_script / godot_write_script / godot_run_script / godot_validate_script / godot_attach_script / godot_hot_reload_scripts
- 文件/资源：godot_list_files / godot_read_file / godot_write_file / godot_resource_load / godot_assign_resource / godot_list_resources
- 项目工具：godot_run_project / godot_stop_project / godot_get_project_info / godot_query_classdb / godot_get_scene_dump / godot_get_input_map / godot_rescan_filesystem
- 可视化：godot_map_project（localhost:6510 交互式项目关系图）

## 方案二：NPGameDev/godot-mcp-toolkit

Godot 编辑器插件 + 桥接 server，112 个内置 MCP 工具（150+ 操作），支持 GDScript 扩展 API、只读模式、会话令牌鉴权。

```bash
npm install -g @npgamedev/godot-mcp-server
```

## 方案三：godot-mcp-runtime（运行时控制）

区别于纯编辑器工具，运行项目时注入 UDP 桥接（localhost:9900），支持运行时截图、输入模拟、UI 发现、实时 GDScript 执行，可让 AI 验证自己改动的运行结果。

```json
{ "mcpServers": { "godot": { "command": "godot-mcp-runtime" } } }
```

## 方案四：godot-mcp（headless，校验/导出）

`@zbrkic/godot-mcp` 支持无头模式检查/验证/测试/导出：get_project_settings、list_export_presets、export_project、run_tests、validate_scene、validate_script、run_scene、format_gdscript、inspect_scene_tree、find_nodes、get_node_properties、get_node_connections、list_resources、verify_api、get_help 等 20 个工具。
