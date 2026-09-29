# ME Media Center

A Windows desktop app for parsing, downloading, organizing, and viewing media you are authorized to save.

**Current release: 0.22.1** · [Download and checksums](https://github.com/paykey1/ME-Media-Downloader/releases/latest) · [Release notes](https://github.com/paykey1/ME-Media-Downloader/releases/tag/v0.22.1)

- **Parsing and downloads:** creator profiles and individual posts across Douyin, Xiaohongshu, Bilibili, X, Instagram, and TikTok; media selection, batch downloads, pause and resume.
- **Saved parsing history:** save results locally, send them to the download center, parse again, or delete saved records.
- **Media library:** organize photos and videos with folders, tags, collections, search, ratings, and HASH duplicate detection; view images and play videos.
- **Creator library:** private cloud backup and two-way sync, with platform filters and search.
- **Sharing community:** discover and share creators, browse tags and public sharer nicknames, rate, like, comment and reply, and import creators into your local library.
- **Storage and language:** Simplified Chinese and English interfaces; new installations store managed data in the program's AppData folder. Existing users can migrate legacy data from General settings using copy-and-verify recovery.

### What's new in 0.22.1

Online updates now retry temporary interruptions and support validated resume, including fallback from differential downloads. Differential metadata and cache handling, update dialogs, and installation failure recovery have been improved. Large media selections are no longer truncated at 10,000 items; a 24,001-item submission was verified across five persisted batches and restart recovery.

If an older version cannot download the update, download the full installer from the release page and install to the existing location after exiting normally. Keep AppData and media folders.

### Also included from 0.22.0

Series Library (Beta) adds search, favorites, episode downloads, full-series assembly with H.264 / H.265 options, and sequential playback. Local episodes are grouped by title and ordered by episode number. Playback settings now include a configurable seek interval (15 seconds by default). Download destinations, large submissions, quitting, and interface layouts have also been improved.

### Installation and updates

Download the Windows installer and its SHA256 checksum from the latest release. Exit the app before installing an update and keep your existing application data. The installer includes managed runtimes and media tools.

The installer is unsigned, so Windows may show an unknown-publisher warning. Verify the download source and checksum before installation. Download only media you are authorized to save. Third-party licenses are included with the installer.

This repository distributes installers, checksums, and public documentation. Older illustrated guides are retained as historical references and may differ from the current interface.

---

# ME媒体中心

在 Windows 本机解析、下载、整理、浏览和播放你有权保存的媒体内容。

**当前版本：0.22.1** · [下载安装包与校验文件](https://github.com/paykey1/ME-Media-Downloader/releases/latest) · [本次更新说明](https://github.com/paykey1/ME-Media-Downloader/releases/tag/v0.22.1)

- **解析与下载：**支持抖音、小红书、Bilibili、X、Instagram、TikTok 等平台的博主主页与单作品解析，以及媒体筛选、批量下载、暂停和继续。
- **解析历史：**本地保存解析结果，可直接提交下载中心、重新解析或删除保存记录。
- **媒体中心：**通过文件夹、标签、收藏、搜索、评分和 HASH 去重管理图片与视频，支持图片查看与视频播放。
- **博主库：**支持私人云端备份与双向同步，可按平台筛选和搜索。
- **共享社区：**发现与分享博主，查看标签和分享者公开昵称，支持评分、点赞、评论、楼中楼回复，并可将博主导入本地博主库。
- **存储与语言：**支持简体中文和英文；新安装将应用数据存放在程序目录的 AppData 中，旧用户可在常规设置中通过复制校验与异常恢复机制迁移数据。

### 0.22.1 更新重点

在线更新支持短暂中断后的有限重试与校验续传，差分回退到完整下载也使用相同恢复机制。改进差分元数据、缓存匹配、更新弹窗和安装失败后的恢复。大批量媒体选择不再截断为前 10,000 条，已验证 24,001 条媒体的五批提交、保存与重启恢复。

如果旧版仍无法下载更新，请从发布页获取完整安装包，正常退出后安装到原位置，保留 AppData 和媒体目录。

### 同时包含 0.22.0 的功能

新增剧集库（Beta），支持搜索、收藏、分集下载、全集拼接和顺序连播；本地剧集按作品归类、按集数排列。拼接可选 H.264 / H.265，播放设置可自定义快进快退间隔（默认 15 秒）。同时优化下载位置、大批量提交、退出流程与界面布局。

### 安装与升级

从最新发布页下载安装包及 SHA256 校验文件。升级前请正常退出程序，并保留已有应用数据。安装包内置受管理的运行环境与媒体工具。

安装包尚未签名，Windows 可能显示“未知发布者”。安装前请核对下载来源与校验值，仅下载你有权保存的媒体。第三方组件许可证随安装包提供。

本仓库用于分发安装包、校验文件与公开文档。旧版图文说明作为历史资料保留，界面可能与当前版本不同。
