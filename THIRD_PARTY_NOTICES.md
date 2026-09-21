# 第三方组件说明

安装包预置固定版本的平台解析组件，并在首次启动时复制到应用自己的独立可写目录。组件不会写入系统 Python 环境，普通用户无需另行下载。

## uv

- 版本：`0.12.9`
- 用途：在构建时准备隔离的 Python 3.12.10 与解析器环境，并为组件修复提供同一受管工具
- 许可证：Apache License 2.0 或 MIT License
- 项目主页：https://github.com/astral-sh/uv
- 存储位置：`%LOCALAPPDATA%\of-media-archiver\platform-tools`

安装包同时附带 uv 的 Apache 2.0 与 MIT 许可证全文。uv 不读取本机项目配置，并被要求只使用应用管理的 Python，不注册到 Windows，也不修改系统 Python。

## gallery-dl

- 版本：`1.32.10`
- 用途：X / Twitter 等站点的公开媒体信息提取
- 许可证：GNU General Public License v2.0（GPL-2.0-only）
- 项目主页：https://github.com/mikf/gallery-dl
- 安装方式：随安装包提供，首次启动复制到 `%LOCALAPPDATA%\of-media-archiver\platform-tools\gallery-dl\.venv`

桌面程序通过独立进程和受限 JSON 协议调用 gallery-dl，不复制或修改其源码。若将 gallery-dl 与安装包一起重新分发，应同时履行 GPL v2 的许可证和对应源码提供义务。

## F2

- 版本：`0.0.1.7`
- 用途：抖音公开博主作品解析
- 许可证：Apache License 2.0
- 项目主页：https://github.com/Johnserf-Seed/f2
- 安装方式：随安装包提供，首次启动复制到应用自己的独立 Python 环境

## yt-dlp

- 版本：`2026.08.19`
- 用途：Bilibili 与“其它平台”的公开作品信息、画质及音视频轨提取
- 许可证：The Unlicense
- 项目主页：https://github.com/yt-dlp/yt-dlp
- 安装方式：随安装包提供，首次启动复制到 `%LOCALAPPDATA%\of-media-archiver\platform-tools\yt-dlp\.venv`

## imageio-ffmpeg

- 版本：`0.6.0`
- 用途：为 Bilibili 与“其它平台”的分离音视频轨下载提供独立 FFmpeg 可执行文件
- 许可证：BSD-2-Clause（Python 包）；随包 FFmpeg 7.1 Gyan essentials 二进制启用 --enable-gpl 与 --enable-version3，适用 GPL-3.0-or-later
- 项目主页：https://github.com/imageio/imageio-ffmpeg
- 安装方式：与 yt-dlp 一起随安装包提供

## curl-cffi

- 用途：为 yt-dlp 提供浏览器 TLS 请求模拟能力，兼容要求浏览器网络特征的公开页面
- 许可证：MIT License
- 项目主页：https://github.com/lexiforest/curl_cffi
- 安装方式：作为 yt-dlp 的官方 `curl-cffi` 可选依赖随安装包提供

# aria2

## ffprobe (FFmpeg)

- 版本：9.0.1，Gyan essentials 构建
- 用途：读取本地视频和音频的完整媒体属性
- 许可证：GPL-3.0-or-later；完整许可证随 bundled-runtime/platform-tools/ffprobe 分发
- 官方项目：https://ffmpeg.org/
- 对应源码：https://github.com/FFmpeg/FFmpeg/commit/bf1b838f2a
- 构建与来源：https://github.com/GyanD/codexffmpeg/releases/tag/9.0.1
- 安装方式：安装包内置，首次启动复制至用户可写组件目录，无需联网安装

This product includes aria2 1.37.0, licensed under GNU General Public License version 2 or later. The license text is distributed as `LICENSE-ARIA2-GPL2`. Source code is available from https://github.com/aria2/aria2/tree/release-1.37.0.

## 7-Zip

- 用途：在本地以“存储”级别生成 7z/zip 压缩包及分卷文件
- 许可证：GNU LGPL；部分代码适用 BSD 3-Clause 与 unRAR restriction
- 项目主页：https://www.7-zip.org/
- 安装方式：`7z.exe`、`7z.dll` 与许可证文本随安装包提供，用户无需另行安装

## Requests

- 版本：`2.32.5`
- 用途：百度网盘上传和分享文件下载桥接
- 许可证：Apache License 2.0
- 项目主页：https://requests.readthedocs.io/
- 安装方式：随百度网盘隔离运行环境一同提供

## FFmpeg 二进制与源码出处

FFmpeg 与 ffprobe 通过独立进程调用。FFmpeg 7.1 与 ffprobe 9.0.1 的 GPL v3 许可证全文随包置于 `bundled-runtime/LICENSE-FFMPEG-GPL3.txt`；各 Python 包许可证随对应 dist-info 目录保留，Electron 的许可证文件随应用提供。

- FFmpeg 7.1 构建及源码出处：https://github.com/GyanD/codexffmpeg/releases/tag/7.1
- FFmpeg 上游源码：https://github.com/FFmpeg/FFmpeg/commit/b08d7969c5
- ffprobe 9.0.1 对应源码：https://github.com/FFmpeg/FFmpeg/commit/bf1b838f2a
- gallery-dl 对应源码：https://github.com/mikf/gallery-dl/tree/v1.32.10
- aria2 对应源码：https://github.com/aria2/aria2/tree/release-1.37.0
- 7-Zip 源码与许可证：https://www.7-zip.org/download.html

第三方组件的名称和著作权属于各自作者，应用不主张拥有这些组件。
