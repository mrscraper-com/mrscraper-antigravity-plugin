# Publishing MrScraper for Antigravity

Use this checklist for a public MrScraper Antigravity plugin release.

## Release gate

- [ ] Merge only reviewed changes into `main`.
- [ ] Record user-visible changes in `CHANGELOG.md`. Antigravity's
      `plugin.json` has no version field, so the release version is the Git
      tag.
- [ ] Keep the skills identical to the canonical MrScraper MCP skills in
      `mrscraper-com/mrscraper-claude-plugin` (`plugins/mrscraper/skills/`).
- [ ] Confirm that the repository contains no credentials or private target
      data.
- [ ] Validate the plugin from a clean checkout:

  ```bash
  agy plugin validate plugins/mrscraper
  ```

- [ ] Confirm the GitHub validation workflow passes.
- [ ] Install the plugin from the public repository in a clean Antigravity
      profile, complete OAuth, and confirm all seven MCP tools load.
- [ ] Run the smoke-test prompt below.
- [ ] Create the matching Git tag and GitHub release for an explicit semantic
      version.

## Submission details

Keep these values ready for Google:

| Field | Value |
| --- | --- |
| Plugin name | `mrscraper` |
| Display name | `MrScraper` |
| Repository | `https://github.com/mrscraper-com/mrscraper-antigravity-plugin` |
| Plugin path | `plugins/mrscraper` |
| Documentation | `https://docs.mrscraper.com/docs/getting-started/mcp-server#google-antigravity` |
| Support | `support@mrscraper.com` · `https://mrscraper.com/support` |
| Privacy policy | `https://mrscraper.com/privacy-policy` |
| Acceptable use policy | `https://mrscraper.com/acceptable-use-policy` |
| Terms of use | `https://mrscraper.com/terms-of-use` |
| MCP endpoint | `https://mcp.mrscraper.com/mcp` (Streamable HTTP) |
| Authentication | OAuth 2.1 with dynamic client registration and client ID metadata documents |
| Components | 1 MCP server, 4 skills |

Suggested description:

> Connect your agent to MrScraper for raw page fetching, managed structured
> extraction, Google discovery, and reusable saved scraper workflows. The
> included skills preserve source responses with a fetch-first workflow before
> adding backend extraction when it is explicitly requested or clearly useful.

The hosted service receives target URLs and tool inputs, including extraction
instructions. Results are returned to the agent for the user's requested task.
The OAuth connection can grant `scrape:read`, `scrape:write`, and
`account:read` access. The plugin contains no static credentials.

Smoke-test prompt:

```text
Fetch https://www.scrapethissite.com/pages/simple/ and summarize the page.
```

## Submit to Google

The Antigravity Marketplace is curated. Its documentation directs plugin
authors to the
[Antigravity Plugin Interest Form](https://forms.gle/2EX5RFYPoJe1UgxR9); see
[Marketplace](https://antigravity.google/docs/marketplace).

1. Make this repository public and confirm the validation workflow passes.
2. Submit the interest form with the values above. Google uses the company
   details to verify the organization and sends review status to the primary
   contact.
3. Answer Google's follow-up questions, pointing reviewers to the repository
   and plugin path above.
4. When the listing is live, install it from **Customizations** >
   **Marketplace** in Antigravity 2.0 or with `/plugin install` in the CLI,
   then repeat the OAuth and smoke-test checks.

Antigravity documents no separate submission process for its built-in MCP
Store; ask Google in the same follow-up whether the hosted MCP server can also
be listed there.
