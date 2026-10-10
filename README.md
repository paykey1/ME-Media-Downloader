# ME Media Center

A Windows desktop app for parsing, downloading, organizing, and viewing media you are authorized to save.

**Current release: 0.25.0** · [Download and checksums](https://github.com/paykey1/ME-Media-Downloader/releases/latest) · [Release notes](https://github.com/paykey1/ME-Media-Downloader/releases/tag/v0.25.0)
BaiduYun：:https://pan.baidu.com/s/1gZxu-O0ZKVIxitlApfcwwg?pwd=37b5

- **Parsing and downloads:** creator profiles and individual posts across Douyin, Xiaohongshu, Bilibili, X, Instagram, and TikTok; media selection, batch downloads, pause and resume.
- **Saved parsing history:** save results locally, send them to the download center, parse again, or delete saved records.
- **Media library:** organize photos and videos with folders, tags, collections, search, ratings, and HASH duplicate detection; view images and play videos.
- **Creator library:** private cloud backup and two-way sync, with platform filters and search.
- **Sharing community:** discover and share creators, browse tags and public sharer nicknames, rate, like, comment and reply, and import creators into your local library.
- **Storage and language:** Simplified Chinese and English interfaces; new installations store managed data in the program's AppData folder. Existing users can migrate legacy data from General settings using copy-and-verify recovery.

### What's new in 0.25.0

- Added batch creator follow-up and update checks. Select platforms and creators, view individual progress and results, and pause, stop or resume a round. One creator's failure does not stop the entire round. Retrying older failed or unfinished files is off by default.
- Update checks can report new works without downloading. Each creator has a separate successful checkpoint; the first check can establish a baseline or use a chosen date.
- Added tag management, virtual folders and a recycle bin. Organizing virtual folders leaves files on disk in place. External imports support moving, copying or indexing only. Recycle-bin retention defaults to 30 days and is configurable.
- Grouped media context-menu actions and added customization. Moved the recycle-bin entry to the sidebar and enabled dragging folders directly to reorder them.
- Added parsing of Fanqie series share links and selection of available download quality after parsing. Quality options depend on each work and the returned sources; inaccessible content is not offered as downloadable.
- Improved discovery information, progress and error reporting for magnet and torrent tasks. Actual speed still depends on available peers and network conditions.
- Fixed manual parse pauses and stops being reported as network failures, while retaining partial results and creator records. Select-all respects default exclusions, and creator cards use a more compact layout.
- Fixed open image viewers not following language changes and improved startup migration diagnostics and recovery.
- Revised application updates: differential downloads are disabled. Compatible small updates can use verified application resources; runtime or dependency changes require the full installer. Use the full installer for this release.

Exit normally before upgrading and preserve AppData and media files. Do not delete your library to troubleshoot startup problems. Series online playback and the image-comic entry remain disabled. FANBOX, Ci-en and Patreon remain in development.

### Previously in 0.24.0

- **Pixiv support**: Parse creator profiles, download artwork, save creators to the library, sync them to the cloud, and share them with the community.
- **Fantia creator management**: Save creators, edit tags, sync to the cloud, and share creator profiles. Creator cards open the Subscription Center, where you choose a post limit or date range before starting a scan.
- **Improved image viewing**: Open images in independent windows and use multiple viewers at once. Fullscreen hides window borders and controls; leaving fullscreen restores the previous window state.
- **Improved HASH duplicate detection**: Review the scan scope and confirm before starting. See actual preparation and detection progress, cancel a scan, or retry after a failure.
- **Organized series folders**: Series appear under one Series Library, with episodes grouped by title. Existing indexed content is regrouped in the interface without moving or renaming files on disk.
- **Smoother folder sorting**: A translucent folder preview follows the pointer, with a clear insertion line. Folder order is saved automatically.
- **More reliable downloads**: Added bounded automatic retries for interrupted Pixiv downloads and fixed missing creator-library records.
- **Improved Transfer Center**: Progress updates preserve your file-list scroll position. Each Retry Unfinished round reports its results when it ends.
- **Startup feedback**: A loading screen appears after unlocking while the main window is being prepared.
- **Development status labels**: FANBOX, Ci-en, and Patreon are marked as In Development in the Subscription Center.
- Fixed several interface interactions, window-restoration issues, and task-status messages.

### Previously in 0.23.0

Baidu Netdisk download is also available:
[Download version 0.23.0 from Baidu Netdisk](https://pan.baidu.com/s/1gZxu-O0ZKVIxitlApfcwwg?pwd=37b5) · Extraction code: `37b5`

- **Faster media previews**: Prioritize thumbnails currently in view and reuse the local thumbnail cache to reduce waiting after restarting and during fast scrolling.
- **Improved playback**: Videos start playing when opened. The player supports independent windows and adjusts window dimensions to the media.
- **Improved image browsing**: Added translucent previous/next arrows. Clicking the black background no longer closes the image viewer accidentally.
- **Transfer Center improvements**: Double-click downloaded images and videos, or choose “Open,” to use the built-in image viewer and player.
- **Customizable top navigation**: Drag sections to reorder them, with drag animations and automatically saved positions.
- **Local creator tags**: Edit and save tags. Cloud imports inherit cloud-provided tags; newly parsed creators start without tags.
- **Series Library improvements**: Recently viewed and favorite series retain details locally and support manual refresh. Enable automatic following for unfinished favorites to queue new episodes for download, add them to the library and receive notifications.
- **New statistics features**: Opt in to anonymous usage statistics, with improved administrator tools for user management, activity and retention statistics.
- **New boss key**: You know what it's for.
- Refined layouts across several screens.
- Improved interface interactions.
- **Bug fixes**: Fixed the app exiting after unlocking, incorrect quality selection in some downloads and various interface issues.

### Previously in 0.22.1

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

**当前版本：0.25.0** · [下载安装包与校验文件](https://github.com/paykey1/ME-Media-Downloader/releases/latest) · [本次更新说明](https://github.com/paykey1/ME-Media-Downloader/releases/tag/v0.25.0)
备用下载百度网盘：链接:https://pan.baidu.com/s/1gZxu-O0ZKVIxitlApfcwwg?pwd=37b5 提取码:37b5

- **解析与下载：**支持抖音、小红书、Bilibili、X、Instagram、TikTok 等平台的博主主页与单作品解析，以及媒体筛选、批量下载、暂停和继续。
- **解析历史：**本地保存解析结果，可直接提交下载中心、重新解析或删除保存记录。
- **媒体中心：**通过文件夹、标签、收藏、搜索、评分和 HASH 去重管理图片与视频，支持图片查看与视频播放。
- **博主库：**支持私人云端备份与双向同步，可按平台筛选和搜索。
- **共享社区：**发现与分享博主，查看标签和分享者公开昵称，支持评分、点赞、评论、楼中楼回复，并可将博主导入本地博主库。
- **存储与语言：**支持简体中文和英文；新安装将应用数据存放在程序目录的 AppData 中，旧用户可在常规设置中通过复制校验与异常恢复机制迁移数据。

### 0.25.0 更新重点

- 博主库新增批量追更与检查更新：可选择平台和博主，显示每位博主的进度与结果，支持暂停、停止和接续；个别失败不会中断整轮任务。补下历史失败或未完成文件默认关闭。
- 检查更新可仅报告新作品，不自动下载；每位博主分别保存成功检查记录。首次可建立基线或指定日期。
- 媒体管理新增标签管理、虚拟文件夹及回收站。文件夹整理不移动磁盘文件；外部导入可选择移动、复制或仅建立索引。回收站默认保留 30 天，可在设置中调整。
- 优化媒体右键菜单，按用途归类并支持自定义；回收站移至侧栏，文件夹可直接拖动排序。
- 新增番茄剧集分享链接解析；解析后可在下载区选择实际可用清晰度。可用档位取决于作品与解析结果，无法访问的内容不会作为可下载资源。
- 改善磁力和种子任务的发现信息、下载进度及错误反馈；下载速度仍取决于资源做种情况和网络条件。
- 修复手动暂停或停止解析被误报为网络失败的问题，保留已取得的结果和博主资料；批量全选遵守默认排除设置，博主卡片布局更紧凑。
- 修复已打开图片窗口不跟随语言切换的问题，改善启动迁移的异常提示及恢复流程。
- 调整在线更新机制：停止启用差分下载；兼容的小型更新支持校验后的应用资源更新，环境或依赖变更使用完整安装包。本次升级请使用完整安装包。

升级前正常退出软件，保留 AppData 和媒体文件，不要通过删除资料库来处理启动异常。剧集在线播放与图片漫画入口保持关闭。FANBOX、Ci-en、Patreon 仍为开发中。

### 此前 0.24.0 的更新

- **新增 Pixiv 支持**：支持博主主页解析、作品下载、博主入库、云同步及社区分享。
- **Fantia 博主管理升级**：支持保存到博主库、编辑标签、云同步和社区分享；博主卡片可直接跳转订阅中心，自行设置扫描数量或日期范围后开始。
- **图片浏览体验升级**：支持独立窗口、多窗口查看；全屏隐藏窗口边框和控制栏，退出后恢复原窗口状态。
- **HASH 去重优化**：开始前增加确认步骤，显示扫描范围；运行时展示真实准备和检测进度，支持取消及失败重试。
- **媒体目录整理**：剧集内容统一归入“剧集库”，同一作品集中展示各集文件。旧内容根据已有索引自动归并展示，不移动或改名实际文件。
- **目录拖动优化**：拖动时显示半透明文件夹预览和明显的插入指示线，提升排序操作的流畅度，并自动保存顺序。
- **下载稳定性提升**：优化 Pixiv 下载中断后的有限自动重试；修复部分博主未入库的问题。
- **传输中心优化**：下载进度刷新不再打断文件列表滚动；“重试未完成”每轮结束后显示结果通知。
- **启动反馈优化**：输入解锁密码后显示加载界面，避免等待主窗口时误以为程序未启动。
- **开发状态标注**：订阅中心为 FANBOX、Ci-en、Patreon 增加“开发中”提示。
- 修复多处界面交互、窗口恢复和任务状态反馈问题。

### 此前 0.23.0 的更新

百度网盘：[下载 0.23.0 安装包](https://pan.baidu.com/s/1gZxu-O0ZKVIxitlApfcwwg?pwd=37b5) · 提取码：`37b5`

- **媒体预览提速**：优先加载视野中的预览图，复用本地封面缓存，减少重启后和快速滚动时的等待。
- **播放体验优化**：打开视频默认开始播放；播放器支持独立多窗口、窗口随媒体尺寸调整。
- **图片浏览优化**：新增半透明左右切换箭头，点击黑色区域不再误关浏览器。
- **传输中心优化**：已下载的图片和视频，双击或选择“打开”后使用内置浏览器和播放器。
- **顶部导航自定义**：支持拖动调整分区顺序，加入拖动动画并自动保存位置。
- **本地博主标签**：支持编辑并保存标签；云端导入继承云端标签，自行解析新增博主默认无标签。
- **剧集体验升级**：最近浏览和收藏保存本地详情，新增手动更新；未完结收藏支持自动追更，新集自动安排下载、入库并发送通知。
- **新增统计功能**：支持自愿开启匿名使用统计，并完善后台用户管理、活跃与留存统计。
- **新增老板键**：你懂的。
- 部分UI界面、排版优化。
- 加强UI交互体验。
- **问题修复**：修复解锁后程序退出、部分下载画质选择异常及多处界面交互问题。

### 此前 0.22.1 的更新

在线更新支持短暂中断后的有限重试与校验续传，差分回退到完整下载也使用相同恢复机制。改进差分元数据、缓存匹配、更新弹窗和安装失败后的恢复。大批量媒体选择不再截断为前 10,000 条，已验证 24,001 条媒体的五批提交、保存与重启恢复。

如果旧版仍无法下载更新，请从发布页获取完整安装包，正常退出后安装到原位置，保留 AppData 和媒体目录。

### 同时包含 0.22.0 的功能

新增剧集库（Beta），支持搜索、收藏、分集下载、全集拼接和顺序连播；本地剧集按作品归类、按集数排列。拼接可选 H.264 / H.265，播放设置可自定义快进快退间隔（默认 15 秒）。同时优化下载位置、大批量提交、退出流程与界面布局。

### 安装与升级

从最新发布页下载安装包及 SHA256 校验文件。升级前请正常退出程序，并保留已有应用数据。安装包内置受管理的运行环境与媒体工具。

安装包尚未签名，Windows 可能显示“未知发布者”。安装前请核对下载来源与校验值，仅下载你有权保存的媒体。第三方组件许可证随安装包提供。

本仓库用于分发安装包、校验文件与公开文档。旧版图文说明作为历史资料保留，界面可能与当前版本不同。
