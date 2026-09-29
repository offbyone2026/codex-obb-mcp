# Unreal Engine MCP（UE5 编辑器控制）

## 方案一：aadeshrao123/Unreal-MCP（pip 安装，280 命令）

C++ 插件在 UE5 编辑器内作为 TCP server（localhost:55557），Python MCP server（unrealmcp）将工具调用翻译为 TCP 命令，自动发现运行中的编辑器。

```bash
pip install unrealmcp
```

```json
{ "mcpServers": { "unreal": { "command": "unrealmcp", "args": [], "env": {} } } }
```

工具分类（13 类，280 命令）：资产（查找/导入/复制/重命名/删除）、蓝图（创建/编译/组件/变量/函数/图节点）、材质（创建/构建节点图/应用/实例）、数据表（schema/增删改行）、Data Assets、Actor（生成/变换/删除/属性）、Niagara VFX、StateTree、Mass Entity、Enhanced Input（actions/mapping contexts/triggers/modifiers）、UMG Widget（增删移动/属性）、性能分析（traces/瓶颈诊断/flame charts/帧分析）。

## 方案二：GenOrca/unreal-mcp（68 tools，9 类）

- Actor 操作 17：spawn/duplicate/transform/delete、surface raycasting、frustum 查询、属性 get/set
- 资产管理 2：按名称/类型搜索过滤、静态网格详情
- 材质系统 11：表达式创建与连接、材质实例参数、重编译
- 蓝图图 10：图结构读取、节点/引脚/变量增删改、整图编译
- 行为树 12：行为树创建读取、Blackboard 资产与键管理、完整 BT 层级构建
- UMG Widget 6：Widget Blueprint 创建、15 类控件增删、Canvas Slot 布局、编译
- 编辑器工具 6：选中管理、材质/网格替换
- 游戏设置 3：GameMode 配置、输入动作与映射
- 工具 1：输出日志检索

## 方案三：IvanMurzak/Unreal-MCP（61 built-in tools + 3 系统工具）

- 蓝图编写：创建/编辑/编译 Blueprint，结构化错误/警告反馈循环
- C++ 编辑与编译：读/搭/改项目 C++，Live Coding / UBT 编译
- 视觉反馈：viewport/game-view/camera/isolated-actor 截图
- 自定义工具/提示词/资源注册
- 云端 ai-game.dev 或自托管 GameDev-MCP-Server

## 方案四：ChiR24/Unreal_mcp（npx，Remote Control API）

```bash
npm install -g unreal-engine-mcp-server
```

基于 UE Remote Control API + Python Editor Script，覆盖资产/角色/编辑器控制/关卡/动画物理/Niagara/Sequencer/音频/系统（console/UBT/tests/logs/CVars）。

```json
{
  "mcpServers": {
    "unreal-engine": {
      "command": "npx", "args": ["unreal-engine-mcp-server"],
      "env": { "UE_HOST": "127.0.0.1", "UE_RC_HTTP_PORT": "30010", "UE_RC_WS_PORT": "30020" }
    }
  }
}
```

> 选型建议：主力开发用方案一（工具最全、零配置）；需要蓝图整图编辑时配合方案二。
