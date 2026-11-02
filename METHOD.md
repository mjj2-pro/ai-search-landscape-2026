# Method & Reproducibility Log / 方法与复现日志

## Scope

This report answers one question: **which search tools are actually used by LLM / AI-agent developers in three ecosystems - English web, Chinese web, and GitHub - and what is the evidence?**

It deliberately does **not** rank search quality by human preference, does not cover private deployments, and does not attempt a full evaluation of model-native search (OpenAI / Anthropic built-ins are mentioned only for pricing).

## Timeline (2026-11-02, Asia/Shanghai)

| Step | What happened |
|---|---|
| 19:14 | Session start; parallel sub-investigations launched for EN and ZH |
| 19:15-19:25 | Multi-engine web searches (EN + ZH), `gh api` star measurements, official docs fetched |
| 19:25 | ZH investigation returned (pricing tables, FastGPT PR, MaxKB, Dify installs) |
| 19:25 | EN investigation returned (funding, LangChain tool lists, MCP stars, benchmarks) |
| 19:26-19:46 | TinyFish Research API run (`mode=deep`) - completed, 48 citations |
| 19:47-19:55 | Cross-checks: OpenBenchmarks page fetched directly, Brave/OpenClaw blog, Dify marketplace, LangChain docs |
| 20:36 | Report written and published to this repo |

## Search queries

**English (run on Exa / Tavily / Parallel / Bing routing):**

- `best web search API for AI agents 2026 Tavily Exa Brave comparison`
- `web search API for LLM agents Tavily Exa Brave Serper comparison`
- `Exa AI search funding Series B valuation 2026`
- `Parallel Web Systems search API pricing Parag Agrawal`
- `Perplexity Sonar API pricing per search`
- `code search tool for AI agents GitHub grep.app Sourcegraph gitingest comparison`
- `grep.app number of repositories indexed code search`
- `GitHub Octoverse 2025 repositories total number code search`
- `Brave Search API 700,000 OpenClaw users`
- `Dify marketplace search plugin Bocha Tavily installs`

**Chinese (run on Exa fallback, because Baidu key was unavailable):**

- `AI 搜索 API 对比 博查 智谱 百度 给大模型用`
- `博查 DeepSeek 联网搜索 官方合作伙伴`
- `秘塔 AI 搜索 API 开放平台 价格`
- `阿里云 IQS 信息查询服务 AI 搜索 API 百度千帆 AI搜索`
- `博查 AI 搜索 API 定价 文档 bocha`

**GitHub:** `grep.app code search`, `GitHub MCP server code search`, `gitingest repomix deepwiki` - used only to discover candidates; every number was then verified with `gh api`.

## Commands used (examples)

```bash
# star counts, all 2026-11-02
gh api repos/github/github-mcp-server --jq .stargazers_count
gh api repos/firecrawl/firecrawl --jq .stargazers_count
gh api repos/searxng/searxng --jq .stargazers_count
gh api repos/ItzCrazyKns/Perplexica --jq .stargazers_count
gh api repos/bocha-ai/bocha-search-mcp --jq .stargazers_count
gh api repos/gitingest/gitingest --jq .stargazers_count   # 404 -> correct repo is cyclotruc/gitingest

# independent benchmark, machine-readable
curl -s https://openbenchmarks.com/web-search/exa-vs-tavily-vs-brave-vs-serper.md
```

Full star table measured during the session:

| Repo | Stars | Pushed |
|---|---|---|
| firecrawl/firecrawl | 197,814 | 2026-11-02 |
| langgenius/dify | 160,223 | 2026-11-02 |
| n8n-io/n8n | 209,345 | 2026-11-02 |
| open-webui/open-webui | 157,527 | 2026-11-02 |
| searxng/searxng | 39,116 | 2026-11-01 |
| ItzCrazyKns/Perplexica | 37,962 | 2026-09-01 |
| github/github-mcp-server | 34,156 | 2026-11-02 |
| assafelovic/gpt-researcher | 30,428 | 2026-10-10 |
| yamadashy/repomix | 29,118 | 2026-11-01 |
| AsyncFuncAI/deepwiki-open | 18,349 | 2026-10-28 |
| ast-grep/ast-grep | 16,416 | 2026-11-02 |
| cyclotruc/gitingest | 16,063 | 2026-11-02 |
| jina-ai/reader | 12,226 | 2026-05-22 |
| miurla/morphic | 9,251 | 2026-11-01 |
| modelcontextprotocol/servers | 91,744 | 2026-10-29 |

## TinyFish run parameters

- Endpoint: `POST https://agent.tinyfish.ai/v1/automation/run-research`
- Auth: `X-API-Key`
- Body: `{"query": "...", "mode": "deep"}`
- Observed duration: ~20 minutes; 48 citations returned
- Free allowance: first 2 completed runs per UTC day; afterwards `deep` = $2/run, `max` = $3/run
- Full output archived in [tinyfish-deep-research.md](tinyfish-deep-research.md)

## What was NOT done (honest gaps)

1. **No primary re-run of Vals AI or AIMultiple benchmarks.** They are cited as B-grade via TinyFish; URLs are in EVIDENCE.md for independent verification.
2. **Baidu search engine was unavailable** during the session (no key configured), so Chinese queries fell back to Exa. This biases Chinese results toward English-indexed Chinese content.
3. **No procurement-level price verification** for Kimi, 360, Valyu, Keenable.
4. **No hands-on latency testing.** All latency figures are vendor- or benchmark-reported.
5. **No Chinese-language independent benchmark exists** to our knowledge - that absence is itself a finding (README section 3.3).

## Reproducing this report

1. Re-run the `gh api` star commands above (numbers drift daily).
2. Fetch the OpenBenchmarks page and check the date stamp.
3. Fetch each vendor pricing page - several are JS-rendered and may need a browser.
4. Optionally run one TinyFish `deep` research to discover new entrants; verify every number it returns against a primary source.