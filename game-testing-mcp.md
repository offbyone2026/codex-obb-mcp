# 游戏测试与平衡 MCP

> 痛点：UI/流程自动化测试、数值平衡校验。此前无专门工具，只有 playtesting 技能。

## 1. Playwright MCP（官方，UI/端到端测试）

- 来源：`microsoft/playwright-mcp`（微软官方）
- 安装：npx @playwright/mcp 或接入客户端
- 能力：
  - 浏览器/Web 游戏 UI 自动化：点击、填表、导航、截图
  - SPA 动态内容抓取、断言
  - 录制与回放脚本
- 适用：Web 游戏（Phaser/Three.js）、后台管理页、发行页面（Steam 商店页预览）
- 价值：官方维护，跨浏览器，是游戏 Web 端测试的通用底座

## 2. mcp-game-helper（战斗平衡/数值分析）

- 来源：`xhulz/mcp-game-helper`
- 能力：
  - 战斗平衡分析（胜率/输出曲线）
  - 技能数值评估、组合强度
  - 关卡节奏检查（难度曲线）
- 适用：数值策划、平衡调优，配合 combat-system-design 技能
- 价值：把"平衡"从拍脑袋变成数据校验

## 接入建议

| 痛点 | 推荐 |
|------|------|
| Web/UI 自动化测试 | Playwright MCP |
| 战斗平衡/数值 | mcp-game-helper |

## 与既有技能配合

- 测试流程走 `playtesting` 技能；Web 端用例由 Playwright MCP 自动执行。
- 平衡问题用 mcp-game-helper 出数据报告，再进 `combat-system-design` 技能改配置。

## 注意

- Playwright MCP 只覆盖浏览器态；原生客户端游戏仍需 `playtesting` 技能的人工/半自动流程。
- mcp-game-helper 需要接入方提供数据文件（JSON/CSV），先约定数据格式。
