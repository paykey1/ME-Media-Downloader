# ME媒体中心 0.24.0 更新公告

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

---

# ME Media Center 0.24.0 Release Notes

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
