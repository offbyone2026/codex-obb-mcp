# 音频与音乐 MCP（TTS / 歌曲生成 / DAW 控制）

> 痛点：配音、BGM、音乐制作。补充 ElevenLabs、Suno、Sonauto 与 Ableton Live 控制。

## 1. ElevenLabs MCP（官方，TTS/配音首选）

- 来源：`elevenlabs/elevenlabs-mcp`（官方）
- 安装：托管版（ElevenLabs API key）或本地部署（uvx/pip）
- 能力：
  - 文本转语音（多语言、多音色）
  - 语音克隆、音频处理（降噪/分段）
  - 长文本分块朗读
- 适用：NPC 配音、过场旁白、多语言语音包

## 2. Suno MCP（音乐生成）

- 来源：`unforced/suno-mcp`
- 安装：Node + Chrome DevTools Protocol（CDP）或官方 API（视版本）
- 能力：自定义歌词/风格描述生成歌曲、等待完成、下载 MP3
- 适用：BGM、主题曲、音效音乐化
- 注意：需 Suno 账号/API 额度；CDP 版需本机 Chrome

## 3. music-mcp（Sonauto API，备选）

- 来源：`zaptrem/music-mcp`
- 安装：npm + Sonauto API key
- 能力：文生音乐、风格控制、导出音频
- 适用：Sonauto 用户；作为 Suno 的替代供应商

## 4. ableton-live-mcp（DAW 控制）

- 来源：`joaobalzer/ableton-live-mcp`
- 安装：pip + Ableton Live 开启 TCP 端口（默认 9877）连接 Object Model
- 能力：transport（播放/停止）、tracks、clips、MIDI、devices、scenes、mixing、automation
- 适用：专业编曲/混音自动化，程序化生成音乐段落
- 价值：唯一能真正"操作 DAW"的 MCP，覆盖音乐制作痛点

## 接入建议

| 痛点 | 推荐 |
|------|------|
| 配音/语音 | ElevenLabs MCP（官方） |
| BGM/歌曲 | Suno MCP 或 music-mcp |
| 专业编曲/混音 | ableton-live-mcp |

## 与既有技能配合

- 配音/BGM 生成后走 `game-audio-design` 技能定规格与引擎 Bus 接入。
- 语音包本地化与 `game-localization` 技能衔接。

## 注意

- 商业 API 有配额；批量生成前先确认余额。
- Ableton Live 需在项目内开启远程控制（Options → Preferences → Link/Tempo/Remote）。
