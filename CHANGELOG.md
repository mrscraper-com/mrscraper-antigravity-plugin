# Changelog

All notable changes to the MrScraper Antigravity plugin are documented here.
The project follows [Semantic Versioning](https://semver.org/); each release is
a Git tag because Antigravity's `plugin.json` has no version field.

## 0.2.2 - 2026-10-29

- Reworded search as web search in the plugin
  description, README, publishing notes, and skills.
  The `webSearch` tool is unchanged. The skills now differ from the MrScraper
  Claude plugin 0.2.2 only in this wording.

## 0.2.1 - 2026-10-22

- Updated the `mrscraper` skill and the docs for the hosted server's three
  scopes: `scraperAPI` needs `scrape:write`, `webSearch` needs `scrape:read`,
  and `status` needs `account:read`. If `scraperAPI` returns 403
  `insufficient_scope`, sign in again so Antigravity requests `scrape:write`.
  Skills are identical to the MrScraper Claude plugin 0.2.2.

## 0.2.0 - 2026-10-14

- Updated the skills for the hosted MCP server's new tools: `scraperAPI`
  (pages as HTML, Markdown, or screenshots), `webSearch` (Google), and `status`
  (account usage). The `fetch`, `scrape`, `serp`, `rerun`, `results`, and
  `result` tools no longer exist.
- Removed the `mrscraper-scrape` skill. Skills are identical to MrScraper
  Claude plugin 0.2.0.

## 0.1.0 - 2026-10-05

- Added the initial MrScraper plugin for Antigravity 2.0, the Antigravity CLI,
  and the Antigravity IDE: the hosted MCP server over Streamable HTTP with
  OAuth 2.1, and the `mrscraper`, `mrscraper-fetch`, `mrscraper-scrape`, and
  `mrscraper-serp` skills, identical to MrScraper Claude plugin 0.1.4.
- Added continuous validation with Antigravity CLI 1.2.17.
