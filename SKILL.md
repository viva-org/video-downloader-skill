---
name: video-downloader-skill
description: "使用 yt-dlp 从 YouTube、Bilibili、Twitter 等数个平台下载视频和音频。支持画质选择、格式转换、音频提取，并内置 Bilibili 反防盗链优化。"
---

# Video Downloader 技能

此技能通过调用 `scripts/video_download.py` 脚本，实现从各大主流视频平台下载内容的功能。

## 何时使用

当用户的意图是**下载**、**保存**或**抓取**在线视频或音频时，应使用此技能。常见触发指令包括：

- “下载这个 Bilibili 视频...”
- “把这个 YouTube 视频的音频提取出来，转成 MP3。”
- “保存一下这个 Twitter 视频，要 1080p 画质。”
- “这个链接里的视频能下载吗？”

## 命令结构

```bash
python3 scripts/video_download.py "<URL>" [OPTIONS]
```

## 核心参数

| 参数 | 简写 | 描述 | 默认值 |
|---|---|---|---|
| `--output` | `-o` | 指定输出目录 | 当前目录 |
| `--quality` | `-q` | 设置视频画质 (`best`, `1080p`, `720p`...) | `best` |
| `--format` | `-f` | 设置视频格式 (`mp4`, `webm`, `mkv`) | `mp4` |
| `--audio-only` | `-a` | 只下载音频并转为 MP3 | 关闭 |
| `--cookies` | `-c` | 指定用于身份验证的 Cookies 文件 | 无 |

## 使用示例

1.  **基本下载 (最佳画质, MP4)**

    ```bash
    python3 scripts/video_download.py "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
    ```

2.  **下载指定画质的 Bilibili 视频**

    ```bash
    python3 scripts/video_download.py "https://www.bilibili.com/video/BV1xx411c7mD" -q 1080p
    ```

3.  **仅提取音频**

    ```bash
    python3 scripts/video_download.py "https://www.youtube.com/watch?v=..." -a
    ```

4.  **使用 Cookies 下载**

    ```bash
    python3 scripts/video_download.py "<URL>" -c /path/to/cookies.txt
    ```

## 支持平台

此技能底层使用 `yt-dlp`，理论上支持其所支持的[数个网站](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md)，包括但不限于：

- YouTube
- Bilibili
- Twitter / X
- Vimeo
- Facebook
- TikTok

## 注意事项

- **依赖**: 脚本会自动处理 `yt-dlp` 的安装，无需手动干预。
- **文件名**: 下载后的文件名将根据视频标题自动生成。
- **播放列表**: 默认只下载单个视频，不处理整个播放列表。
