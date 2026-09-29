# AI 3D 资产生成 MCP（文生3D / 图生3D）

> 痛点：美术资源瓶颈。Blender MCP 管建模改模，但"从零生成 3D 资产"此前缺失。以下工具直接产出可导入引擎的模型。

## 1. mcp-3d-gen（多供应商聚合，首选）

- 来源：`kevinten-ai/mcp-3d-gen`
- 安装：npm 包 + API key（Tripo3D / Hyper3D Rodin / Meshy 三选一或全配）
- 能力：
  - 文生 3D / 图生 3D
  - 输出 GLB / FBX / OBJ（引擎可直接导入）
  - 贴图烘焙、减面、格式转换等后处理
- 适用：Godot/Unity 项目占位模型与正式资产批量生成
- 价值：一个 server 覆盖三家供应商，避免绑定单一厂商

## 2. game-asset-mcp（Hugging Face 生成）

- 来源：`MubarakHAlketbi/game-asset-mcp`
- 安装：Python/uv + HF API 配置
- 能力：通过 HF 模型文生 2D 精灵与 3D 资产，面向游戏资源格式
- 适用：需要开源模型、不想买商业 API 的场景

## 3. ai-forge-mcp（AAA 资源管线，565 tools）

- 来源：`HurtzDonutStudios/ai-forge-mcp`
- 能力：覆盖建模、贴图、材质、LOD、导入导出全流程的 AAA 级资产管线
- 适用：追求生产级质量的团队；工具面最大但较重
- 注意：工具数多，需在客户端做分组/按需加载

## 接入建议

| 场景 | 推荐 |
|------|------|
| 商业 API 批量生成 | mcp-3d-gen（Tripo/Meshy/Rodin） |
| 开源/免费模型 | game-asset-mcp |
| 生产级全管线 | ai-forge-mcp |

## 与既有技能配合

- 生成 → `game-asset-pipeline` 技能（批量组织命名）→ `game-asset-pipeline` 引擎导入规范
- 生成后如需改模，交给 Blender MCP 精修

## 注意

- 各家 API 有配额/余额，批量任务先查余额再开工。
- GLB 建议再走一次减面/压缩，避免运行时内存超预算。
