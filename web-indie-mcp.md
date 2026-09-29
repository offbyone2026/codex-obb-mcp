# Web 与独立引擎 MCP（Phaser / Bevy / Defold / RPG Maker / Three.js）

> 痛点：Web 2D/3D、Rust 引擎、轻量引擎与低代码引擎此前未覆盖。

## 1. Phaser Editor MCP（官方）

- 来源：`phaserjs/editor-mcp-server`（Phaser 官方团队）
- 安装：npm 包 + Phaser Editor 内启用
- 能力：场景编辑、游戏对象、资源管理，配合 Phaser 4
- 适用：HTML5 2D 游戏（浏览器发布）

## 2. Bevy MCP（Rust 引擎调试）

- 来源：`Nub/bevy_mcp` + `Ladvien/bevy_debugger_mcp`
- 安装：crate 集成到 Bevy 项目（bevy_remote_protocol / 调试插件）
- 能力：运行时实体/组件查看、指令下发、调试输出
- 适用：Rust Bevy 项目；无编辑器，靠运行时协议调试

## 3. Defold MCP

- 来源：`ChadAragorn/defold-mcp`
- 能力：Defold 项目资源/场景/脚本操作
- 适用：Defold 轻量 2D 引擎（Lua 脚本）

## 4. RPG Maker Mz MCP（RPG Maker MZ）

- 来源：社区（awesome-mcp-servers gaming 收录）
- 能力：RPG Maker MZ 事件/地图/数据库操作
- 适用：JRPG 快速原型与叙事游戏

## 5. three-js-mcp（Three.js 3D Web）

- 来源：社区（awesome-mcp-servers gaming 收录）
- 能力：Three.js 场景结构、模型加载、相机/灯光配置辅助
- 适用：3D Web 体验、产品配置器

## 接入建议

| 引擎 | 推荐 |
|------|------|
| Phaser 4 | phaserjs/editor-mcp-server |
| Bevy (Rust) | bevy_mcp + bevy_debugger_mcp |
| Defold | defold-mcp |
| RPG Maker MZ | Rpgmaker Mz MCP |
| Three.js | three-js-mcp |

## 注意

- Bevy 无编辑器，MCP 依赖项目内集成 crate，需在 Cargo.toml 加入对应依赖。
- RPG Maker MZ 与 Defold 社区实现较新，接入前先验证维护活跃度。
