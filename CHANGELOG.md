# Changelog

All notable changes to the MrScraper Antigravity plugin are documented here.
The project follows [Semantic Versioning](https://semver.org/); each release is
a Git tag because Antigravity's `plugin.json` has no version field.

## 0.5.0 - 2026-11-24

- Updated the skills for MrScraper MCP server 0.6.0, whose tools take exactly
  the inputs on MrScraper's API documentation pages. The `mrscraper-fetch`
  skill lists each page tool's inputs with the documented descriptions. An
  input left out is not sent, so MrScraper's own default applies; left out,
  `browserRendering` lets MrScraper switch to a browser when a request is
  blocked. The `mrscraper-serp` skill says the same for `country` and
  `numResults`.
- New inputs: `maxAge` on the four page tools reuses a cached result (0, a
  fresh scrape, is sent when it is left out); `screenshot` on `scrapeHtml`
  adds a screenshot; `getScreenshot` also takes a viewport size such as
  `1280x800`; and `scrapeJson` takes `waitForSelector`, `warmStart`, and
  `blockResources` and returns the page HTML unless `html` is false. `timeout`
  goes up to 330 seconds.
- `scrapeMarkdown` returns only Markdown and `getScreenshot` only the
  screenshot: their `html` and `markdown` inputs are gone, and
  `getScreenshot` no longer takes `blockResources`. Every other input that
  the API documentation doesn't list is gone too. `saveResult` is no longer
  an input: the four page tools always save their result to the MrScraper
  dashboard.
- The retry guidance uses `browserRendering`, `waitForSelector`, `timeout`,
  `warmStart`, `geoCode`, `maxRetries`, and `maxAge`.
- The README shows the MCP 0.6.0 tool descriptions.
- Skills are identical to the MrScraper Claude 0.5.0, Cursor 0.6.0, Grok
  0.5.0, and OpenCode 0.6.0 plugins.

## 0.4.0 - 2026-11-20

- Updated the skills, README, and publishing notes for MrScraper MCP server
  0.5.0, which follows the MrScraper Integrations Standard. The server has
  seven tools with the standard descriptions: `status`, `scrapeHtml`,
  `scrapeMarkdown`, `getScreenshot`, `scrapeBrand`, `scrapeJson`, and
  `webSearch`. `scraperAPI` is gone; use `scrapeHtml`, `scrapeMarkdown`, or
  `getScreenshot`, and `scrapeBrand` or `scrapeJson` for brand data and JSON
  extraction. `webSearch` now takes `query`, `country`, and `numResults`
  instead of `url`, `region`, `num_results`, and `timeout`, and all tool
  inputs are camelCase. Skills are identical to the MrScraper Claude 0.4.0,
  Cursor 0.5.0, Grok 0.4.0, and OpenCode 0.5.0 plugins.
- The hosted server now uses two OAuth scopes: `scrape:read` for the six
  scraping and search tools and `account:read` for `status`. Connections that
  already hold `scrape:read` keep working; `scrape:write` is no longer needed.

## 0.3.0 - 2026-11-02

- Updated the `mrscraper-serp` skill for MrScraper MCP server 0.3.0, which
  moved `webSearch` to MrScraper's new web search endpoint. Results are a
  ranked list (rank, title, url, description, source); `region` sets the
  results' country and the new `num_results` asks for 10 to 100 results. The
  `raw`, `format`, `language`, `page`, and `render_js` options are gone, and
  so is the search results URL example. Skills are identical to the MrScraper
  Claude plugin 0.3.0.

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
