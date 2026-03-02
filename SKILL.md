---
name: video-to-text
description: 视频转文字工具。使用 bilibili-api 下载B站视频，yt-dlp 下载其他网站视频，FFmpeg 提取音频，faster-whisper 转写为文字。适用于需要将视频内容转换为文本字幕或文档的场景。
---

# Video to Text

将视频URL或本地文件转换为文字稿。

## 使用方法

```bash
python3 /root/.openclaw/workspace/skills/video-to-text/scripts/video_to_text.py <视频URL或本地文件> [选项]
```

## 参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `url` | 视频URL或本地文件路径 (必填) | - |
| `-m, --model` | Whisper模型大小 | `base` |
| `-l, --language` | 指定语言代码 | 自动检测 |
| `-o, --output` | 输出文件路径 | 打印到终端 |
| `--keep-files` | 保留下载的音视频文件 | 否 |
| `--sessdata` | B站 SESSDATA | 配置文件中 |
| `--bili-jct` | B站 bili_jct | 配置文件中 |
| `--budi3` | B站 buvid3 | 配置文件中 |

## 模型选择

| 模型 | 大小 | 速度 | 精度 |
|------|------|------|------|
| `tiny` | ~75MB | 最快 | 最低 |
| `base` | ~150MB | 快 | 一般 |
| `small` | ~500MB | 中等 | 较好 |
| `medium` | ~1.5GB | 慢 | 好 |
| `large` | ~3GB | 最慢 | 最好 |

## 示例

```bash
# B站视频（需要认证信息）
python3 scripts/video_to_text.py "https://www.bilibili.com/video/BVxxx"

# 指定中文模型
python3 scripts/video_to_text.py "https://www.bilibili.com/video/BVxxx" -l zh

# 本地文件
python3 scripts/video_to_text.py "/path/to/video.mp4" -m small

# 保存到文件
python3 scripts/video_to_text.py "https://www.bilibili.com/video/BVxxx" -o result.txt
```

## 支持的平台

- **B站** (bilibili.com) - 需要认证信息
- **YouTube** - 使用 yt-dlp
- **抖音/TikTok** - 使用 yt-dlp
- **Twitter/X** - 使用 yt-dlp
- 以及 yt-dlp 支持的所有网站
- **本地文件** - 支持 mp4, wav, m4a, webm, mkv 等格式

## B站认证信息配置

### 方法1: 配置文件

编辑脚本开头的 `BILIBILI_CREDENTIALS` 字典：

```python
BILIBILI_CREDENTIALS = {
    "sessdata": "你的SESSDATA",
    "bili_jct": "你的bili_jct",
    "buvid3": "你的buvid3"
}
```

### 方法2: 命令行参数

```bash
python3 scripts/video_to_text.py "https://www.bilibili.com/video/BVxxx" \
    --sessdata "xxx" \
    --bili-jct "xxx" \
    --buvid3 "xxx"
```

### 获取认证信息

1. 登录 B 站网页版 (bilibili.com)
2. 按 F12 打开开发者工具
3. Application → Cookies → bilibili.com
4. 找到以下值：
   - `SESSDATA`
   - `bili_jct`
   - `buvid3`

⚠️ **注意**: 这些信息相当于你的登录凭证，请勿泄露给他人！

## 依赖

- `bilibili-api-python` - B站API调用
- `yt-dlp` - 通用视频下载
- `ffmpeg` - 音视频处理
- `faster-whisper` - 语音转写
- `aiohttp` - 异步HTTP请求
- `requests` - HTTP请求

已在服务器上安装完成。
