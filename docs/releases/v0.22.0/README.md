# ME媒体中心 0.22.0

本次更新新增「剧集库」，短剧爱好者的福音哦\~直接对接某平台的APP解析下载。

完善了剧集下载、整理与播放体验，并优化下载流程和界面交互。

### 新增剧集库（Beta）

- 支持作品搜索、详情查看、手动解析、最近搜索、最近浏览和收藏。
- 支持下载指定剧集、补充下载未下载剧集，以及播放已下载剧集。
- 默认保存至「媒体库位置\剧集库\剧名」，下载任务统一由传输中心管理。

### 剧集拼接与连续播放

- 支持全集下载完成后拼接为完整视频，保留分集文件，单独展示拼接进度。
- 可沿用源视频参数，或自定义 H.264 / H.265 编码及视频、音频码率。
- 支持按集数顺序连播、下一集预加载，以及具有有效章节索引的整剧集数定位。

### 媒体管理与播放器

- 媒体中心新增剧集库分类，按作品聚合展示，剧内固定按集数升序排列。
- 优化竖版封面、作品封面与播放器打开速度。
- 设置新增「播放」，快进、快退间隔可自定义，默认 15 秒。
- 播放器控制按钮改为以图标为主；移除智能收藏夹入口，保留普通收藏夹。

### 下载与界面优化

- 下载默认使用已设置的媒体库位置，同时保留独立下载目录设置。
- 优化大量媒体提交下载时的响应，以及暂停任务后的退出流程。
- 开启下载完成后关机时，底部状态栏显示渐变呼吸文字提醒。
- 优化启动解锁界面、目录右键菜单、导航图标、英文窄窗口布局及任务栏图标。
- 修复开发版与安装版存储目录相互关联的问题。

剧集库目前为 Beta。解析与下载范围取决于来源服务及账号权限；连播衔接和拼接速度受文件参数与设备性能影响。

---

# ME Media Center 0.22.0

This update introduces Series Library and improves episode downloads, organization, playback, and everyday usability.

### Introducing Series Library (Beta)

- Search for titles, view details, parse episodes on demand, and access recent searches, browsing history, and favorites.
- Download selected or remaining episodes and play downloaded episodes.
- Series downloads are managed in Transfer Center and saved under “Library location\剧集库\Series title” by default.

### Series Assembly and Sequential Playback

- Combine a complete downloaded series into one video, with separate assembly progress and individual episode files retained.
- Use source parameters or customize H.264 / H.265 encoding and video/audio bitrates.
- Play episodes in order with next-episode preloading, and navigate by episode within assembled videos that have a valid chapter index.

### Media Library and Player

- A dedicated series category groups episodes by title and sorts them in ascending episode order.
- Improved portrait covers, series covers, and player opening responsiveness.
- New Playback settings offer a customizable seek interval, with a 15-second default.
- Player controls now prioritize icons. Smart collection entries have been removed; regular collections remain available.

### Downloads and Interface Improvements

- Downloads use the configured library location by default, with separate download locations still available.
- Improved responsiveness when submitting large collections and improved quitting after pausing downloads.
- A breathing, color-changing status-bar reminder indicates an active shutdown-after-downloads task.
- Refined startup unlock, folder context menus, navigation icons, narrow English layouts, and taskbar icons.
- Fixed storage-directory crossover between development and installed builds.

Series Library is currently in Beta. Parsing and download availability depend on the source service and account permissions. Playback transitions and assembly speed depend on file parameters and device performance.
