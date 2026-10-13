# ME 本地 API / MCP 接入指南

## 版本与能力

| 能力 | 支持情况 |
|---|---|
| 媒体检索、详情、入库任务、导入、整理（五个 `media_*` 工具） | ME 0.26.0 支持 |
| 插件发现、执行及本人任务查询（三个 `plugin_*` 工具） | 不包含于 ME 0.26.0；需要提供这些工具的 ME 版本 |

不要依据本文更新时间判断客户端能力。开启所需权限后调用 `tools/list`，以实际返回为准；不存在的工具不可调用。插件命令来自已安装插件，ME 不内置任何特定插件业务，也不提供通用解析、下载或追更接口。

[在线说明](https://github.com/paykey1/ME-Media-Downloader/tree/main/docs/local-api)与软件导出使用同一份指南；导出末尾可附当时的连接地址，永远不包含令牌。

## 开启与授权

进入“设置 → 本地 API / MCP → 管理连接”。默认关闭，每次启动 ME 都保持关闭；用户明确开启后才监听 `127.0.0.1`，端口由系统分配。关闭再开启可能改变端口，需重新复制配置。令牌加密保存在本机，仅通过“复制连接配置”交给信任的客户端，不放 URL、日志或公开文档。更换令牌会关闭服务并使旧令牌失效。

| 权限 | 能力 |
|---|---|
| `read` | 检索、媒体详情、内容及入库任务查询 |
| `write` | 修改标题、人工标签、自动标签屏蔽键、评分、备注 |
| `import` | 仅从用户选定并授权的目录复制导入 |
| `plugins` | 发现和执行插件声明的 Agent 命令、查询该调用方的插件任务；默认不勾选 |

`plugins` 与媒体权限独立，**不是只读授权**。已信任插件声明的写入命令不依赖媒体 `write` 开关；它仍受插件自身权限、启用、激活和信任规则限制。只读需求不要授权不需要的插件调用。旧权限不会自动增加 `plugins`。修改权限和导入目录需关闭服务后重新开启。插件发现列表不等于敏感操作已获得授权。

插件必须声明接口 2 的 `agent` 命令上下文。未信任插件的 `write`/`delete` 命令返回 `PLUGIN_APPROVAL_REQUIRED`；外部请求不能代替用户确认、设置插件信任或激活插件。原生插件具有较广的系统权限，仅授权可信插件与客户端。

## REST 连接

`<base>` 是设置显示的 API 地址；所有请求带 `Authorization: Bearer <token>`。JSON 请求带 `Content-Type: application/json`，以 UTF-8 编码。Host 必须是监听地址 `127.0.0.1:<port>`；拒绝任何 Origin，不支持浏览器网页跨域访问。

| 路径 | 方法 | 工具 | 参数 |
|---|---|---|---|
| `<base>/v1/search` | POST | `media_search` | 下节检索字段 |
| `<base>/v1/read` | POST | `media_read` | `assetId` |
| `<base>/v1/assets/{assetId}/content` | GET | — | 路径中的已入库素材 ID |
| `<base>/v1/task` | POST | `media_task` | `taskId`，媒体入库任务 |
| `<base>/v1/import` | POST | `media_import` | `paths`, `detectSimilar?`, `detectExactDuplicates?`, `similarityThreshold?` |
| `<base>/v1/update` | POST | `media_update` | `assetId`, `title?`, `tags?`, `suppressedAutoTagKeys?`, `rating?`, `note?` |
| `<base>/v1/plugins/discover` | POST | `plugin_discover` | `{}` |
| `<base>/v1/plugins/invoke` | POST | `plugin_invoke` | `pluginId`, `command`, `input?`, `idempotencyKey?` |
| `<base>/v1/plugins/task` | POST | `plugin_task` | `taskId`，插件任务 |

除内容下载外，REST 成功返回 JSON，失败为 `{"error":"CODE"}`。所有 JSON 顶层参数拒绝未知字段。单个请求最大 1 MiB，并发最多 16。不要将大文件内容编码放入调用参数。

```javascript
const base = process.env.ME_API_URL; // 从用户复制的配置取得
const token = process.env.ME_API_TOKEN;
async function call(route, args) {
  const response = await fetch(base + route, {
    method: 'POST',
    headers: { Authorization: `Bearer ${token}`, 'Content-Type': 'application/json' },
    body: JSON.stringify(args)
  });
  const result = await response.json();
  if (!response.ok) throw new Error(result.error);
  return result;
}
const page = await call('/v1/search', { type: 'image', manualUntagged: true, limit: 20 });
```

## 媒体参数与返回

检索字段均可选；以 `tools/list` 的 schema 和目标版本校验为准。

| 字段 | 类型和限制 |
|---|---|
| `query`, `platform`, `creatorId`, `workId`, `assetId`, `batchId`, `taskId`, `collectionId`, `smartCollectionId` | 字符串，最长 500 |
| `type` | `image` / `video` / `audio` / `other` |
| `assetIds` | 1–1000 个非空 ID，单项最长 500 |
| `favorite`, `untagged`, `manualUntagged`, `includeDescendants` | 布尔值；`manualUntagged` 表示无人工标签，不是字符串 |
| `tags` | 最多 100 个非空标签，单项最长 80；`tagMode` 为 `all` 或 `any` |
| `shapes` | 数组：`landscape`, `portrait`, `square` |
| `colors` | 数组：`red`, `orange`, `yellow`, `green`, `cyan`, `blue`, `purple`, `pink`, `brown`, `black`, `gray`, `white`, `transparent`, `unknown` |
| `formats` | 数组：`jpeg`, `png`, `gif`, `webp`, `avif`, `bmp`, `tiff`, `heic`, `heif`, `mp4`, `mov`, `webm`, `mp3`, `wav`, `flac`, `m4a`, `other`, `animated`, `live-photo`, `still` |
| `minRating`, `maxRating` | 0–5 整数 |
| `sizeMin`, `sizeMax` | 非负安全整数，字节 |
| `minWidth`, `minHeight`, `minMegapixels`, `maxMegapixels`, `isoMin`, `isoMax` | 0–10000000 的有限数字，最小值不可大于最大值 |
| `cameraModel`, `lensModel` | 最长 200 的字符串 |
| `importedAfter`, `importedBefore`, `capturedAfter`, `capturedBefore` | 可解析的日期字符串，以 YYYY-MM-DD 开头 |
| `locationId`, `storageKind`, `folderPrefix` | 字符串，最长 1000；storageKind 为 `download` / `manual` / `legacy` / `reference`；folderPrefix 为相对目录，不含反斜杠、空段或 `..` |
| `automaticGroupId`, `seriesGroupId` | 主体提供的分组 ID，原样使用，分别为 `auto:` / `series:` 加摘要；不可自行编造 |
| `category` | 仅 `series` |
| `sortBy` | `importedAt`, `title`, `size`, `rating`, `width`, `height`, `duration`, `episode` |
| `sortDirection`, `cursor`, `limit` | `asc`/`desc`；不透明字符串游标；1–200 整数 |

不同筛选组按 AND，同组数组按 OR，标签组合由 tagMode 控制。检索返回 `{items,total,nextCursor,...}`；原样传递游标，游标失效后重新查询第一页。`items` 和详情不包含内部磁盘 `path` 或 `importKey`。详情另含 `contentPath`，下载该相对地址仍需同一令牌与读取权限。内容以附件返回，不提供任意路径下载。

导入 `paths` 是 1–1000 个绝对文件或目录路径，只能位于用户授权根目录内（会解析真实路径）；递归导入且保留源文件。`detectSimilar` 默认 false，`detectExactDuplicates` 默认 true，`similarityThreshold` 为 0–100 整数，默认 50。导入等待复制完成或人工选择后返回，不是立即应答；超时后不要盲目重复导入，媒体导入没有幂等键。

媒体任务返回 `{taskId,state,assetIds,error,sourceCleanup,similarityThreshold?,pendingChoice?}`；不存在时可返回 null。`pendingChoice` 仅提供候选列表，由 ME 界面人工处理。常见状态：`queued`, `copying`, `waiting_storage`, `awaiting_choice`, `committed`, `failed`。媒体任务查询按 `read` 授权，不实行插件的连接任务隔离。

整理必须提供 assetId，可修改字符串 title/note、字符串数组 tags、最多 10000 项 suppressedAutoTagKeys，以及 0–5 整数 rating。返回更新后的素材信息。接口不删除或移动原文件，也不提供自动批准重复文件处理。

## 插件参数、返回与生命周期

`plugin_discover` 返回 `{commands:[{pluginId,id,contexts,permissions,effects,inputSchema,outputSchema,...}]}`。只列出当前启用、已激活、声明 agent 上下文的接口 2 命令。调用时将条目的 `id` 填入 `command`，遵守其 inputSchema；命令可以因状态变化不再可用。

`plugin_invoke` 的 pluginId/command 为非空字符串；input 默认 `{}`，必须是对象并符合命令 schema。可选 idempotencyKey 为 1–100 字符，同一身份中同键同内容返回原任务，不同内容报冲突。短期重试使用原键，不要生成新键重复写入。返回快照包含 `taskId,pluginId,command,state,progress`，可另有 `result` 或 `error:{code,retryable}`。`plugin_task` 接受该 taskId，返回相同快照。状态为 `queued/running/succeeded/failed/cancelled`。结果符合插件输出 schema，受主体大小限制；错误不含内部堆栈。

```javascript
const { commands } = await call('/v1/plugins/discover', {});
// 先让用户选择命令并按它的 inputSchema 准备 input，不自动调用发现的全部命令。
const selected = commands.find(c => c.pluginId === 'example.tagger' && c.id === 'ping');
if (selected) {
  const task = await call('/v1/plugins/invoke', {
    pluginId: selected.pluginId, command: selected.id, input: {}, idempotencyKey: 'request-001'
  });
  const status = await call('/v1/plugins/task', { taskId: task.taskId });
}
```

身份由 ME 创建，不能传 `caller`、`userId`、`workspaceToken`、`confirmed` 等顶层参数。MCP 每个初始化会话独立；REST 同令牌、同一次服务运行共享任务身份，因此拿到同一令牌的程序不是彼此隔离的 REST 用户。MCP 不可读 REST 或其它会话的插件任务，反之亦然。

任务仅存在内存。单个 MCP 会话最多一小时，过期需重新初始化，不能接管旧任务。普通请求结束或暂时网络断开不取消任务；显式 DELETE 会话、会话过期、关闭服务或更换令牌会取消相应身份的排队及正在执行的任务，不影响其它身份的任务。取消不能撤销已经发生的写入。停止再开启服务创建新 REST 身份，不能查询之前运行的插件任务。

每插件串行执行，最多 32 个等待任务；调度器最多保留 1000 个任务，完成记录可能被回收，幂等键不是永久存储。忙碌时稍后重试。执行前再次核对启用、激活、信任和包身份，更新或权限变化可能导致排队任务失败。

## MCP 客户端

使用 `<mcp>`，Streamable HTTP JSON 响应模式；无 stdio、SSE 事件推送或 OAuth 自动发现。客户端必须支持自定义 Bearer 头。支持协议 `2025-03-26` 和 `2025-06-18`，初始化协商后使用返回版本。

1. POST `initialize`，参数含 protocolVersion、capabilities 和 clientInfo；请求 Accept 同时包含 `application/json, text/event-stream`。
2. 保存响应头 `Mcp-Session-Id`，随后请求携带该头和协商的 `MCP-Protocol-Version`。
3. 发送无 id 的 `notifications/initialized`，成功为 HTTP 202。
4. 调用 `tools/list`，按实际工具 schema 使用 `tools/call`。
5. 用完发送 `DELETE <mcp>` 并携带会话及认证头，结束会话。普通客户端 close 不一定发送 DELETE。

```json
{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"media_search","arguments":{"type":"image","limit":20}}}
```

```json
{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"plugin_task","arguments":{"taskId":"<returned-task-id>"}}}
```

成功工具结果在 `result.content[0].text` 中，是需解析的 JSON 文本；失败为 `result.isError:true`，text 为稳定错误码。JSON-RPC 协议错误在 `error`，认证/会话错误也可能是 HTTP 错误。最多 64 个 MCP 会话，`GET /mcp` 为 405，不代表 POST 工具调用不受支持。

## 错误与处理

| 错误码 | 处理 |
|---|---|
| `UNAUTHORIZED` (401) | 重新取得用户授权配置，不打印令牌 |
| `PERMISSION_DENIED`, `LIBRARY_LOCKED`, `ORIGIN_OR_HOST_DENIED` (403) | 检查权限、ME 解锁状态或连接方式；不能通过更换请求参数绕过 |
| `SESSION_NOT_FOUND` (404), `UNSUPPORTED_PROTOCOL` | 重新初始化或使用协商版本 |
| `INVALID_ARGUMENTS`, `INVALID_QUERY`, `INVALID_IMPORT_PATH`, `IMPORT_PATH_DENIED` | 核对 schema、参数类型和授权目录 |
| `JSON_REQUIRED` (415), `INVALID_JSON`, `INVALID_ACCEPT` (406), `REQUEST_TOO_LARGE` (413) | 修正编码、请求头或缩小参数 |
| `BUSY`, `SESSION_LIMIT` (429) | 降低并发或结束不用的会话 |
| `ASSET_NOT_FOUND`, `NOT_FOUND`, `UNKNOWN_TOOL`, `METHOD_NOT_ALLOWED` | 核对 ID、路径、方法和 tools/list |
| `PLUGIN_UNAVAILABLE`, `PLUGIN_BLOCKED` | 检查版本、隐私/锁定及插件服务状态 |
| `PLUGIN_DISABLED`, `PLUGIN_ACTIVATION_REQUIRED`, `PLUGIN_COMMAND_INVALID` | 在 ME 中启用或激活，或重新发现命令 |
| `PLUGIN_PERMISSION_DENIED`, `PLUGIN_APPROVAL_REQUIRED` | 检查声明权限；敏感授权须用户在 ME 中操作 |
| `PLUGIN_REQUEST_INVALID`, `PLUGIN_INPUT_INVALID`, `PLUGIN_OUTPUT_INVALID` | 核对插件输入输出契约 |
| `PLUGIN_TASK_NOT_FOUND`, `PLUGIN_CALLER_INVALID` | 确认原会话/运行仍有效；不能读取其它身份任务 |
| `PLUGIN_IDEMPOTENCY_CONFLICT`, `PLUGIN_PACKAGE_CHANGED` | 不复用冲突幂等键；确认插件更新后的任务状态 |
| `PLUGIN_BUSY`, `PLUGIN_TIMEOUT`, `PLUGIN_EXECUTION_FAILED` | 读取任务错误及 retryable；写操作重试前核对实际结果 |

其它主体或插件错误可能出现；保留错误码并向用户说明，不展示堆栈、凭据或私有路径。REST 的插件校验错误通常为 HTTP 400；MCP 工具业务错误通常为 HTTP 200 配合 isError，不能只检查 HTTP 成功。
