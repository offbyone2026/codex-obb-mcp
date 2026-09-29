# 项目协作与研发效率 MCP

> 痛点：工作室协作（任务/文档/代码评审）。独立工作室虽小，发行前后仍需任务管理、文档沉淀与代码协同。

## 1. Notion MCP（官方）

- 来源：`makenotion/notion-mcp-server`（官方）
- 安装：npm @notionhq/notion-mcp-server + Integration token
- 能力：页面/数据库读写、搜索、任务列表、文档结构化
- 适用：GDD 知识库、任务看板、发行 checklist
- 价值：官方维护，与 Notion 文档体系无缝

## 2. Atlassian MCP（Jira + Confluence 官方）

- 来源：`atlassian/atlassian-mcp-server`（官方）
- 安装：npm + Atlassian 站点凭据
- 能力：Jira issue 管理（创建/查询/更新/评论）、Confluence 文档读写
- 适用：团队规范流程的 bug 跟踪、sprint 管理
- 价值：官方实现，覆盖国内团队常备的 Jira 流程

## 3. GitHub MCP（官方）

- 来源：`github/github-mcp-server`（官方，GitHub 托管版）
- 安装：客户端直接连官方托管版，或本地部署自建
- 能力：仓库管理、Issue/PR/Review、CI 状态、代码搜索
- 适用：代码协作、自动化 PR 评审、release 流程
- 价值：本机 GitHub PAT 已有，直连成本最低；本地推送问题可用 -c credential.helper= 规避

## 接入建议

| 场景 | 推荐 |
|------|------|
| 任务/文档/看板 | Notion MCP |
| Jira/Confluence 流程 | Atlassian MCP |
| 代码与发布 | GitHub MCP |

## 与既有仓库的关系

- 本仓库（codex-obb* 三仓）的发布管理可由 GitHub MCP 代劳（PR/Release），客户端 manifest 拉取仍走 raw/jsdelivr。
- GDD/checklist 放 Notion 或本地 skills 均可；保持 skills 里 indie-project-planning 的模板为唯一事实源，Notion 只做呈现。

## 注意

- 三个都是官方 server，配置凭据时注意最小权限：Notion 用页面级 token，GitHub 用只读+repo 组合，Jira 用只读 API token。
- 国内访问 GitHub/Notion 需加速器；Confluence 若自建则在内网直连。
