# ME媒体中心 0.22.1

本次主要修复在线更新与差分更新的稳定性，并加强大批量下载提交验证。

### 更新修复

- 安装包下载遇到短暂中断时会有限重试；服务器支持时从断点续传，不支持时重新完整下载，并进行完整校验。
- 修复备用更新查询丢失差分资源、发布时间及更新说明的问题；主查询超时后仍可尝试备用查询。
- 修复差分缓存分块图与旧安装包可能错配的问题，加强下载响应与安装包校验。
- 差分无法完成时，经用户确认切换到可续传的完整下载，避免重复确认或重复启动下载。
- 修复安装失败后界面卡在“安装中”、下载完成后找不到安装入口等问题，补充诊断信息。

### 大批量下载

- 包含对旧版“选择超过 10,000 条媒体时仅提交前 10,000 条”的修复。
- 已验证 24,001 条媒体完整拆成 5 个批次，保存并重启恢复后无遗漏；每批最多 5000 条，不增加同时运行的下载批次数。

### 升级说明

旧版本的更新器不会在下载新版本之前自动得到修复。如果 0.21.1 或 0.22.0 仍无法在线更新，请从本发布页下载完整安装包，正常退出程序后安装到原位置。请保留 AppData 与媒体目录，无需卸载或清空数据。

本次验证覆盖模拟断流和真实 Electron 更新流程；办公室网络中断的具体原因仍需根据新版诊断确认，不保证所有网络环境均能连接下载源。

---

# ME Media Center 0.22.1

This maintenance release improves online and differential updates and strengthens large-download submission checks.

### Update fixes

- Added bounded retries and validated resume after temporary interruptions. If the server ignores range requests, the full download restarts and is verified in full.
- Restored differential assets, release dates and release notes in fallback update checks, with a separate fallback timeout budget.
- Fixed potential mismatches between cached blockmaps and older installers, and strengthened response and installer verification.
- Differential fallback now uses the resumable full downloader after confirmation, without duplicate prompts or duplicate full downloads.
- Fixed stuck installation states and restored access to downloaded installers; improved diagnostic evidence.

### Large downloads

- Includes the fix for older versions truncating selections above 10,000 media items.
- Verified all 24,001 selected items across five persisted batches and restart recovery. Each batch remains capped at 5,000 items without increasing concurrent batches.

### Upgrading

An older updater cannot receive these fixes before it downloads the new version. If online updates still fail in 0.21.1 or 0.22.0, download the full installer from this release, exit the application normally and install to the existing location. Keep AppData and media folders; uninstalling or clearing data is unnecessary.

Validation covers injected disconnects and the actual Electron update stack. The specific office-network failure remains unconfirmed; connectivity still depends on the network and download service.
