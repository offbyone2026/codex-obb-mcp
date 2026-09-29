# Sora MCP —— Codex 视频生成

OpenAI 官方视频生成模型为 **Sora 2 API**（`sora-2` / `sora-2-pro`）。Codex 官方未内置视频生成 MCP，标准做法是挂载社区 Sora MCP server，工具直接调用 OpenAI 官方 Sora 2 接口（使用同一把 OpenAI API Key，与现有图片生成 imagegen 同源）。

## 推荐实现（直接连 OpenAI 官方 API）

| 项目 | 语言 | 工具集 | 特点 |
|------|------|--------|------|
| **Porkbutts/sora-mcp-server** | Node.js (>=18) | 8 个工具 | 最完整：文生视频/图生视频/remix/轮询/下载/列表/删除 |
| Doriandarko/sora-mcp | Node.js (>=18) | 4 类能力 | stdio + HTTP 双 server，社区最流行（40+ stars） |
| JoeyWasHere/sora-mcp | Python (>=3.10) | 4 类能力 | Python 版，支持本地/自建 Sora API |

> 另有托管方案 AceDataCloud/SoraMCP（`uvx mcp-sora` 或远端 streamable-http），走第三方 AceDataCloud token，非 OpenAI 官方 Key，仅在拿不到 Sora API 权限时作为备选。

## Porkbutts/sora-mcp-server 工具清单

| 工具 | 说明 | 关键参数 |
|------|------|----------|
| `create_video` | 文本生成视频 | prompt、model(sora-2/sora-2-pro)、size(1920x1080/1080x1920/1280x720/720x1280/1024x1024)、seconds(5/10/15/20) |
| `create_video_with_image` | 参考图生成视频（首帧） | prompt、image_url 或 image_base64、model/size/seconds |
| `get_video_status` | 查询生成任务状态 | video_id |
| `download_video` | 获取/下载成品 | video_id、variant(video/thumbnail/spritesheet) |
| `list_videos` | 视频库分页列表 | limit(1-100)、order、after |
| `delete_video` | 删除云端视频 | video_id |
| `remix_video` | 基于已有视频生成变体 | video_id、prompt |
| `wait_for_video` | 轮询至完成/失败 | video_id、poll_interval_seconds(默认10)、timeout_seconds(默认600) |

## 安装与接入

```bash
git clone https://github.com/Porkbutts/sora-mcp-server
cd sora-mcp-server
npm install
npm run build
# 设置 OpenAI API Key（需已开通 Sora 权限）
$env:OPENAI_API_KEY = "sk-..."
```

Codex 改壳版（config.toml 或客户端注入）：

```toml
[mcp_servers.sora]
command = "node"
args = ["D:/sora-mcp-server/dist/index.js"]
env = { OPENAI_API_KEY = "sk-...", DOWNLOAD_DIR = "D:/Downloads/sora" }
```

## 视频提示词工程（官方推荐）

描述 Sora 视频 prompt 时按五要素组织：

1. **镜头（Shot type）**：Wide shot / Close-up / Tracking shot
2. **主体（Subject）**：画面中是谁/什么
3. **动作（Action）**：正在发生什么
4. **场景（Setting）**：在哪里发生
5. **光照/氛围（Lighting）**：时段、情绪

示例：
> "Wide tracking shot of a teal coupe driving through a desert highway, heat ripples visible, hard sun overhead."

## 内容限制（Sora API 强制）

- 内容须适合 18 岁以下受众
- 禁止版权角色、版权音乐
- 禁止真实人物/公众人物
- 参考图禁止含人脸

## 与图片生成的协同

- 图片生成（imagegen skill / gpt-image-1）产出的角色/场景图 → `create_video_with_image` 做首帧图生视频，实现角色一致性动画；
- Sora 生成的 spritesheet/缩略图 → 回注素材管线。

## 本机部署建议

1. 在 `D:\work\mcp-servers\` 下 clone 并按上表构建；
2. 与现有 Blender MCP（socket 9876）一样在客户端 `obb_agent.py` 的 MCP 配置段注册；
3. `DOWNLOAD_DIR` 指向工作室素材目录（如 `D:\work\Assets\videos\`）。
