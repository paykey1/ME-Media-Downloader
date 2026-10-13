# ME Agent Skill / 智能体技能

[me-media-mcp](me-media-mcp/SKILL.md) teaches an agent to connect to ME Media Center and use its local media and plugin APIs. It includes the API contract and requires no additional executable helper or Python/Node runtime of its own.

## 安装

将下面这句话交给支持 GitHub Skill 安装的 Agent（例如带 skill-installer 的 Codex）：

```text
请从 https://github.com/paykey1/ME-Media-Downloader/tree/main/skills/me-media-mcp 安装 me-media-mcp Skill。
```

也可以下载仓库，将完整的 `skills/me-media-mcp` 文件夹放入 Agent 支持的技能目录。Codex 的位置为 `$CODEX_HOME/skills/me-media-mcp`；未设置 CODEX_HOME 时为 `~/.codex/skills/me-media-mcp`。其它 Agent 请使用其官方技能目录，保留 `SKILL.md`、`agents/` 和 `references/` 的相对结构。安装器可能需要自己的运行环境。

**安装 Skill 不会自动安装 ME、注册 MCP 连接、开启服务或授予权限。** 在运行 ME 的同一台电脑上，进入“设置 → 本地 API / MCP → 管理连接”，由用户开启需要的权限，再通过“复制连接配置”将 MCP 地址和认证头配置到可信客户端的私密配置中。不要把令牌贴到公开文档或聊天记录。客户端需要支持带 Bearer 认证头的 Streamable HTTP；只有技能加载能力、没有 MCP 或本地 HTTP 执行能力的 Agent 无法调用接口。远程云端 Agent 不能通过自己的 `127.0.0.1` 访问你的电脑。

安装并配置连接后可以说：

```text
使用 me-media-mcp，找出媒体库中没有人工标签的图片，先列出前 20 项，不修改素材。
```

ME **0.26.0** 支持五个媒体工具；插件调用与记住开关状态需要提供这些能力的版本。以实际 `tools/list` 为准，Skill 更新不代表已安装程序自动获得新能力。ME 完全退出后 MCP 停止；重启后端口可能改变，需重新复制连接配置。

## Install (English)

Ask an agent with GitHub skill installation support:

```text
Install me-media-mcp from https://github.com/paykey1/ME-Media-Downloader/tree/main/skills/me-media-mcp.
```

Alternatively, copy the complete `skills/me-media-mcp` folder into your agent's supported skill directory. For Codex, use `$CODEX_HOME/skills/me-media-mcp`, or `~/.codex/skills/me-media-mcp` if CODEX_HOME is unset. Preserve the bundled references and metadata. Other agents may use different directories or require reloading skills; follow their documentation.

**Skill installation does not install ME, register an MCP server, enable the service or authorize access.** Run ME on the same machine as the executing client. Enable the required scopes in Settings → Local API / MCP → Manage connection, then use Copy connection configuration to set the MCP URL and Bearer header in your trusted client's private configuration. Do not post tokens in chat or public files. The client needs Streamable HTTP with custom authentication headers, or an authorized local HTTP execution tool for REST fallback. A remote cloud runtime's loopback cannot reach your computer.

Try: “Use me-media-mcp to list the first 20 images without manual tags in my library, without changing anything.” ME **0.26.0** supports five media tools; plugin tools and persistent switch behavior require a supporting version. Detect capabilities with `tools/list`. Exiting ME stops MCP, and a new service run may use a different port.

[中文 API 说明](../docs/local-api/guide.zh-CN.md) · [English API guide](../docs/local-api/guide.en-US.md)
