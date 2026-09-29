# Blender MCP（Blender 建模/贴图自动化）

## 方案：mcp-for-blender addon + server（157 tools，本机已部署）

Blender 编辑器内 addon 以 GUI 启动并拉起 localhost:9876 socket，MCP server 通过 socket 与 Blender 通信，支持建模、材质、贴图、场景编排等 157 个工具。本机（Blender 4.5.14 LTS，D:\Blender）已完成部署与端到端验证。

### 安装要点

```bash
# 安装 addon 到用户 addons 目录
uv tool run mcp-for-blender install-addon --addons-dir <用户addons目录>

# GUI 启动 Blender 并启用 addon + 启动 server（拒绝 background 模式）
blender --python <启动脚本>  # 脚本内 enable blender_mcp 后调 start_server()
```

### 客户端配置

```json
{
  "mcpServers": {
    "blender": { "command": "uvx", "args": ["mcp-for-blender"] }
  }
}
```

### 工具覆盖（157 tools 摘要）

- 场景与对象：创建/变换/复制/删除对象、场景树遍历、物体属性读写
- 建模：网格编辑（顶点/边/面）、挤出/倒角/细分/布尔运算、修改器管理
- 材质与贴图：材质创建与节点图编辑、贴图导入、UV 展开
- 渲染：渲染设置、视角/相机控制、导出
- 交互验证：get_addon_status / get_scene_info 确认 socket 连通
