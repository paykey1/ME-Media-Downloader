# ME local API / MCP guide

## Versions and capabilities

| Capability | Availability |
|---|---|
| Media search, details, import tasks, import and editing: five `media_*` tools | Supported by ME 0.26.0 |
| Plugin discovery, invocation and caller-owned tasks: three `plugin_*` tools | Not included in ME 0.26.0; requires an ME version exposing these tools |

After enabling the required scopes, use `tools/list` to detect actual support. The date of a documentation update does not establish client support. Plugin commands come from installed plugins. ME does not embed a particular plugin's business logic or expose a general parsing, downloading or subscription API here.

The [online guide](https://github.com/paykey1/ME-Media-Downloader/tree/main/docs/local-api) and exported guide use the same source. An export may append current connection addresses, but never the token.

## Enable and authorize

Open Settings → Local API / MCP → Manage connection. The service is off by default and remains off each time ME starts. Explicitly enabling it binds only to `127.0.0.1` on a system-assigned port. Restarting the service may change the port; copy the configuration again. Tokens are stored encrypted locally and are disclosed through Copy connection configuration. Share them only with trusted clients, never in URLs, logs or public documents. Rotating the token closes the service and invalidates the old token.

| Scope | Access |
|---|---|
| `read` | Search, media details, content and media import-task status |
| `write` | Edit titles, manual tags, suppressed automatic-tag keys, ratings and notes |
| `import` | Copy files only from user-selected authorized directories |
| `plugins` | Discover and invoke declared Agent commands and query caller-owned plugin tasks; unchecked by default |

`plugins` is independent of media scopes and **is not read-only**. A trusted plugin's declared write command does not depend on the media `write` checkbox. Plugin permissions, enabled state, activation and trust checks still apply. Do not grant unnecessary plugin access for a read-only use case. Existing scopes never automatically grant `plugins`. Stop and restart the service to change scopes or import roots. Discovery does not imply approval for sensitive operations.

Plugins must declare API 2 commands with the `agent` context. Untrusted `write`/`delete` commands return `PLUGIN_APPROVAL_REQUIRED`. External requests cannot approve operations, trust a plugin or activate one. Native plugins have broad operating-system access; authorize only trusted plugins and clients.

## REST connection

`<base>` is the API address shown in settings. Every request requires `Authorization: Bearer <token>`. JSON requests require `Content-Type: application/json` and UTF-8. Host must match `127.0.0.1:<port>`. Any Origin header is rejected; browser cross-origin access is not supported.

| Path | Method | Tool | Arguments |
|---|---|---|---|
| `<base>/v1/search` | POST | `media_search` | Search fields below |
| `<base>/v1/read` | POST | `media_read` | `assetId` |
| `<base>/v1/assets/{assetId}/content` | GET | — | Indexed media ID in the path |
| `<base>/v1/task` | POST | `media_task` | `taskId`, a media import task |
| `<base>/v1/import` | POST | `media_import` | `paths`, `detectSimilar?`, `detectExactDuplicates?`, `similarityThreshold?` |
| `<base>/v1/update` | POST | `media_update` | `assetId`, `title?`, `tags?`, `suppressedAutoTagKeys?`, `rating?`, `note?` |
| `<base>/v1/plugins/discover` | POST | `plugin_discover` | `{}` |
| `<base>/v1/plugins/invoke` | POST | `plugin_invoke` | `pluginId`, `command`, `input?`, `idempotencyKey?` |
| `<base>/v1/plugins/task` | POST | `plugin_task` | `taskId`, a plugin task |

Except content downloads, successful REST responses contain JSON; failures contain `{"error":"CODE"}`. Unknown top-level argument fields are rejected. Requests are limited to 1 MiB of JSON and 16 concurrent operations. Do not embed large files in arguments.

```javascript
const base = process.env.ME_API_URL; // From the user's connection configuration
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

## Media arguments and responses

All search fields are optional. Follow the target version's validation and schema from `tools/list`.

| Fields | Type and limits |
|---|---|
| `query`, `platform`, `creatorId`, `workId`, `assetId`, `batchId`, `taskId`, `collectionId`, `smartCollectionId` | Strings up to 500 characters |
| `type` | `image` / `video` / `audio` / `other` |
| `assetIds` | 1–1000 nonempty IDs, up to 500 characters each |
| `favorite`, `untagged`, `manualUntagged`, `includeDescendants` | Booleans; manualUntagged means no manual tags, not a string |
| `tags` | Up to 100 nonempty tags of at most 80 characters each; `tagMode` is `all` or `any` |
| `shapes` | Array of `landscape`, `portrait`, `square` |
| `colors` | Array of `red`, `orange`, `yellow`, `green`, `cyan`, `blue`, `purple`, `pink`, `brown`, `black`, `gray`, `white`, `transparent`, `unknown` |
| `formats` | Array of `jpeg`, `png`, `gif`, `webp`, `avif`, `bmp`, `tiff`, `heic`, `heif`, `mp4`, `mov`, `webm`, `mp3`, `wav`, `flac`, `m4a`, `other`, `animated`, `live-photo`, `still` |
| `minRating`, `maxRating` | Integers 0–5 |
| `sizeMin`, `sizeMax` | Nonnegative safe integers, bytes |
| `minWidth`, `minHeight`, `minMegapixels`, `maxMegapixels`, `isoMin`, `isoMax` | Finite numbers 0–10000000; minimum cannot exceed maximum |
| `cameraModel`, `lensModel` | Strings up to 200 characters |
| `importedAfter`, `importedBefore`, `capturedAfter`, `capturedBefore` | Parseable date strings starting with YYYY-MM-DD |
| `locationId`, `storageKind`, `folderPrefix` | Strings up to 1000 characters; storageKind is `download` / `manual` / `legacy` / `reference`; folderPrefix is relative, with no backslashes, empty segments or `..` |
| `automaticGroupId`, `seriesGroupId` | Use host-supplied IDs unchanged: `auto:` / `series:` followed by a digest; do not invent IDs |
| `category` | Only `series` |
| `sortBy` | `importedAt`, `title`, `size`, `rating`, `width`, `height`, `duration`, `episode` |
| `sortDirection`, `cursor`, `limit` | `asc`/`desc`; opaque string cursor; integer 1–200 |

Different filter groups use AND, arrays within a group use OR, and tagMode controls tags. Search returns `{items,total,nextCursor,...}`. Pass cursors unchanged; restart from the first page if a cursor becomes invalid. Media items and details omit internal `path` and `importKey`. Details include `contentPath`; downloading that relative URL still requires the token and read permission. Content is an attachment, not an arbitrary-path download API.

Import `paths` contains 1–1000 absolute file or directory paths beneath user-authorized roots, checked after real-path resolution. Import is recursive and preserves source files. `detectSimilar` defaults to false; `detectExactDuplicates` defaults to true. `similarityThreshold` is an integer 0–100, default 50. Import waits until copying finishes or user choice is needed; it does not immediately acknowledge background work. Do not blindly repeat timed-out imports; media import has no idempotency key.

Media tasks return `{taskId,state,assetIds,error,sourceCleanup,similarityThreshold?,pendingChoice?}` or null if missing. pendingChoice exposes candidates only; the user resolves them in ME. Common states: `queued`, `copying`, `waiting_storage`, `awaiting_choice`, `committed`, `failed`. Media task queries use read permission, not the connection ownership rules for plugin tasks.

Editing requires assetId and accepts string title/note, string-array tags, at most 10000 suppressedAutoTagKeys, and integer rating 0–5. It returns the updated media item. The API does not delete or move original files or approve duplicate-file choices.

## Plugin arguments, results and lifecycle

`plugin_discover` returns `{commands:[{pluginId,id,contexts,permissions,effects,inputSchema,outputSchema,...}]}`. Only enabled, activated API 2 commands declaring agent context are listed. Copy the entry's `id` into `command` and follow inputSchema. A command can become unavailable after discovery.

For `plugin_invoke`, pluginId and command are nonempty strings. input defaults to `{}` and must be an object matching the command schema. Optional idempotencyKey is 1–100 characters. The same key and content within one identity returns the original task; different content conflicts. Reuse the original key for short-term retries to avoid duplicate writes. The snapshot contains `taskId,pluginId,command,state,progress` and optionally `result` or `error:{code,retryable}`. `plugin_task` takes the returned taskId and returns the same snapshot. States are `queued/running/succeeded/failed/cancelled`. Results follow the plugin output schema and host size limits. Errors do not include internal stacks.

```javascript
const { commands } = await call('/v1/plugins/discover', {});
// Ask the user to choose a command and prepare input from its schema.
// Never automatically invoke every discovered command.
const selected = commands.find(c => c.pluginId === 'example.tagger' && c.id === 'ping');
if (selected) {
  const task = await call('/v1/plugins/invoke', {
    pluginId: selected.pluginId, command: selected.id, input: {}, idempotencyKey: 'request-001'
  });
  const status = await call('/v1/plugins/task', { taskId: task.taskId });
}
```

ME creates caller identities. Top-level caller, userId, workspaceToken or confirmed parameters are forbidden. Each initialized MCP session has its own identity. REST requests sharing one token during one service run share an identity; those clients are not separate REST users. MCP cannot query REST or other sessions' plugin tasks, and vice versa.

Tasks are memory-only. MCP sessions last at most one hour; reinitialize after expiry without taking over old tasks. A completed HTTP request or temporary network disconnect does not cancel a task. Explicit session DELETE, expiry, service shutdown or token rotation cancels the corresponding identity's queued/running tasks without cancelling other identities' tasks. Cancellation cannot undo writes already performed. Restarting the service creates a new REST identity that cannot query prior plugin tasks.

Commands execute serially per plugin, with at most 32 waiting commands. The dispatcher retains at most 1000 tasks; completed records may be reclaimed. Idempotency keys are not permanent storage. Retry later when busy. Enabled state, activation, trust and package identity are rechecked before execution; updates or authorization changes can fail queued tasks.

## MCP clients

Use `<mcp>` with Streamable HTTP JSON responses. There is no stdio, SSE event stream or OAuth discovery. Clients must support custom Bearer headers. Protocols `2025-03-26` and `2025-06-18` are supported; use the version returned by initialization.

1. POST initialize with protocolVersion, capabilities and clientInfo. Accept must include both `application/json, text/event-stream`.
2. Save the response's Mcp-Session-Id and send it with the negotiated MCP-Protocol-Version in subsequent requests.
3. Send notifications/initialized without an id. Success is HTTP 202.
4. Call tools/list and follow returned schemas when calling tools/call.
5. Send DELETE to `<mcp>` with session and authorization headers to terminate the session. Closing a client does not necessarily send DELETE.

```json
{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"media_search","arguments":{"type":"image","limit":20}}}
```

```json
{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"plugin_task","arguments":{"taskId":"<returned-task-id>"}}}
```

Successful tool results contain JSON text in `result.content[0].text`. Parse it to obtain the value. Tool failures set result.isError to true and text to an error code. Protocol errors use the JSON-RPC error field; authentication/session errors may be HTTP errors. At most 64 MCP sessions are allowed. GET /mcp returns 405 because SSE is unavailable, not because POST tools are unsupported.

## Errors and recovery

| Code | Action |
|---|---|
| `UNAUTHORIZED` (401) | Obtain authorized configuration again; do not print tokens |
| `PERMISSION_DENIED`, `LIBRARY_LOCKED`, `ORIGIN_OR_HOST_DENIED` (403) | Check scopes, unlock state or connection method; do not bypass with forged parameters |
| `SESSION_NOT_FOUND` (404), `UNSUPPORTED_PROTOCOL` | Reinitialize or use the negotiated version |
| `INVALID_ARGUMENTS`, `INVALID_QUERY`, `INVALID_IMPORT_PATH`, `IMPORT_PATH_DENIED` | Check schema, argument types and authorized roots |
| `JSON_REQUIRED` (415), `INVALID_JSON`, `INVALID_ACCEPT` (406), `REQUEST_TOO_LARGE` (413) | Fix encoding/headers or reduce arguments |
| `BUSY`, `SESSION_LIMIT` (429) | Reduce concurrency or end unused sessions |
| `ASSET_NOT_FOUND`, `NOT_FOUND`, `UNKNOWN_TOOL`, `METHOD_NOT_ALLOWED` | Check IDs, paths, method and tools/list |
| `PLUGIN_UNAVAILABLE`, `PLUGIN_BLOCKED` | Check version, privacy/lock and plugin service state |
| `PLUGIN_DISABLED`, `PLUGIN_ACTIVATION_REQUIRED`, `PLUGIN_COMMAND_INVALID` | Enable/activate in ME or discover commands again |
| `PLUGIN_PERMISSION_DENIED`, `PLUGIN_APPROVAL_REQUIRED` | Check declared permissions; sensitive authorization requires user action in ME |
| `PLUGIN_REQUEST_INVALID`, `PLUGIN_INPUT_INVALID`, `PLUGIN_OUTPUT_INVALID` | Check plugin input/output contracts |
| `PLUGIN_TASK_NOT_FOUND`, `PLUGIN_CALLER_INVALID` | Verify the original session/run still exists; other identities' tasks are inaccessible |
| `PLUGIN_IDEMPOTENCY_CONFLICT`, `PLUGIN_PACKAGE_CHANGED` | Do not reuse conflicting keys; check task state after plugin updates |
| `PLUGIN_BUSY`, `PLUGIN_TIMEOUT`, `PLUGIN_EXECUTION_FAILED` | Inspect error and retryable; verify actual effects before retrying writes |

Other host or plugin errors may occur. Preserve error codes and explain them without exposing stacks, credentials or private paths. REST plugin validation errors usually use HTTP 400; MCP business errors normally use HTTP 200 with isError. HTTP success alone does not prove tool success.
