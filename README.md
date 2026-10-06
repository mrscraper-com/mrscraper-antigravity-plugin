# MrScraper for Google Antigravity

MrScraper connects Google Antigravity to a hosted MCP server for fetching
public web pages, managed structured extraction, Google discovery, saved
scraper reruns, stored results, and account usage. The plugin also includes
four focused skills that help the agent choose the right workflow and preserve
raw page content.

## What this plugin adds

- The hosted Streamable HTTP endpoint at `https://mcp.mrscraper.com/mcp`.
- OAuth 2.1 authentication through Antigravity's MCP client; no credential is
  stored in this repository.
- Four skills: `mrscraper`, `mrscraper-fetch`, `mrscraper-scrape`, and
  `mrscraper-serp`.
- A fetch-first workflow that keeps raw page responses available for analysis,
  verification, and follow-up transformations.
- Managed extraction, site mapping, Google SERP discovery, saved reruns, and
  stored-result tools when those capabilities are useful.

The plugin works in Antigravity 2.0, the Antigravity CLI (`agy`), and the
standalone Antigravity IDE.

## Requirements

- A current version of [Google Antigravity](https://antigravity.google/download).
- A [MrScraper](https://app.mrscraper.com) account.
- Permission to access and process the target content.

## Install

Clone this repository first:

```bash
git clone --depth 1 https://github.com/mrscraper-com/mrscraper-antigravity-plugin.git
```

### Antigravity CLI

```bash
agy plugin install ./mrscraper-antigravity-plugin/plugins/mrscraper
agy plugin list
```

The CLI copies the plugin to `~/.gemini/config/plugins/mrscraper/`, the shared
configuration directory that Antigravity 2.0 and the Antigravity IDE also read.

### Antigravity 2.0 and Antigravity IDE

Copy the plugin folder to the global plugin directory to use it in every
workspace:

```bash
mkdir -p ~/.gemini/config/plugins
cp -R mrscraper-antigravity-plugin/plugins/mrscraper ~/.gemini/config/plugins/
```

To enable it for one project only, copy the folder to
`.agents/plugins/mrscraper/` in that workspace instead. Restart Antigravity,
then confirm that MrScraper appears under **Customizations**.

## Sign in

Antigravity must authorize the hosted MCP server once before the agent can use
its tools. MrScraper supports dynamic client registration, so no client ID or
secret is required.

- **Antigravity 2.0 and Antigravity IDE:** open Agent settings with `Cmd` + `,`
  (macOS) or `Ctrl` + `,` (Windows and Linux), go to **Customizations**, and
  select **Authenticate** next to the MrScraper server.
- **Antigravity CLI:** run `/mcp`, select the MrScraper server, and choose
  **Authenticate**.

Approve access on the MrScraper consent page in your browser, copy the
authorization code that the browser then shows, paste it back into
Antigravity, and submit it. Antigravity stores and refreshes the resulting
tokens. Never paste OAuth tokens or API keys into the chat.

## Try it

```text
Fetch https://www.scrapethissite.com/pages/simple/ and summarize the page.
```

The connection should expose these MCP tools:

| Tool | Purpose |
| --- | --- |
| `fetch` | Retrieve and preserve a known page's raw response. |
| `scrape` | Run managed structured extraction or bounded site mapping. |
| `serp` | Discover public pages through Google. |
| `rerun` | Reuse a saved AI or manual scraper configuration. |
| `results` | Browse and filter stored result records. |
| `result` | Retrieve one stored result or poll an asynchronous run. |
| `status` | Inspect subscription usage and request outcomes. |

Antigravity asks for approval before running MCP tools unless your permission
policy allows them. In the CLI, the skills are also available as slash
commands, such as `/mrscraper:mrscraper-fetch`.

## Fetch-first routing

When a public URL is already known, the skills direct the agent to fetch it
first and treat the raw response as the source of truth. The agent can read,
summarize, compare, or derive structured output locally without losing details
to an early extraction prompt.

This preference can still be faster for large same-layout sets. For roughly
100 known pages, the agent can safely fetch pages concurrently, retain every
raw response, and apply one reusable local extractor instead of requesting 100
separate backend-LLM extractions. Use `scrape` when managed extraction is
explicitly requested or has a clear benefit after the page structure and
desired schema are understood.

## Connect the MCP server without the plugin

To add only the MCP server, put this entry in `~/.gemini/config/mcp_config.json`
(all workspaces) or `.agents/mcp_config.json` (one workspace). In the
Antigravity IDE, open it from **…** > **MCP Servers** > **Manage MCP Servers** >
**View raw config**.

```json
{
  "mcpServers": {
    "mrscraper": {
      "serverUrl": "https://mcp.mrscraper.com/mcp"
    }
  }
}
```

From the CLI, the same entry can be written with:

```bash
agy mcp add mrscraper https://mcp.mrscraper.com/mcp
```

Antigravity requires `serverUrl` for remote servers. Then sign in as described
above.

### API key fallback

Use OAuth whenever possible. If Antigravity cannot complete OAuth, create an
[API key](https://app.mrscraper.com/api-tokens) and send it as a bearer token.
An API key carries full account authority, and Antigravity stores this header
in plain text in `mcp_config.json`, so keep it in your user-level file, never in
a workspace file that is committed.

With the key exported as `MRSCRAPER_API_KEY` in your shell:

```bash
agy mcp add --header "Authorization: Bearer $MRSCRAPER_API_KEY" \
  mrscraper https://mcp.mrscraper.com/mcp
```

Or edit `~/.gemini/config/mcp_config.json` directly:

```json
{
  "mcpServers": {
    "mrscraper": {
      "serverUrl": "https://mcp.mrscraper.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_MRSCRAPER_API_KEY"
      }
    }
  }
}
```

If you use the API key fallback, skip the plugin, whose server uses OAuth, and
copy only its skills to `~/.gemini/config/skills/`, which Antigravity 2.0, the
IDE, and the CLI all read, or to `.agents/skills/` in one workspace:

```bash
mkdir -p ~/.gemini/config/skills
cp -R mrscraper-antigravity-plugin/plugins/mrscraper/skills/* ~/.gemini/config/skills/
```

## Data and permissions

The plugin sends MCP tool inputs—including target URLs and extraction
instructions—to MrScraper's hosted service. Page responses and tool results are
then available to the agent for the requested task. Use it only with public or
otherwise authorized content, and follow the target site's requirements.

Review MrScraper's [MCP documentation](https://docs.mrscraper.com/docs/getting-started/mcp-server),
[Privacy Policy](https://mrscraper.com/privacy-policy), and
[Acceptable Use Policy](https://mrscraper.com/acceptable-use-policy) before use.

## Update or remove

Pull the latest version and reinstall the plugin:

```bash
git -C mrscraper-antigravity-plugin pull
agy plugin install ./mrscraper-antigravity-plugin/plugins/mrscraper
```

Disable or remove it with `agy plugin disable mrscraper` or
`agy plugin uninstall mrscraper`, or use the toggle and **Uninstall** action in
**Customizations** > **Installed**.

## Support and security

- Product help: [MrScraper MCP documentation](https://docs.mrscraper.com/docs/getting-started/mcp-server)
- Bugs and feature requests: [GitHub Issues](https://github.com/mrscraper-com/mrscraper-antigravity-plugin/issues)
- Account help: [support@mrscraper.com](mailto:support@mrscraper.com)
- Security reports: see [SECURITY.md](SECURITY.md)

## Development

```text
plugins/mrscraper/
├── plugin.json
├── mcp_config.json
└── skills/
```

Validate the plugin before a release:

```bash
agy plugin validate plugins/mrscraper
```

The skills are copied from the canonical MrScraper MCP skills. Record
user-visible changes in [CHANGELOG.md](CHANGELOG.md) and use
[PUBLISHING.md](PUBLISHING.md) for the release and Antigravity Marketplace
submission checklist.

## License

[MIT](LICENSE)
