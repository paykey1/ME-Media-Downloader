# ME媒体中心 0.25.0 更新公告

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

---

# ME Media Center 0.25.0 Release Notes

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
