# AI Search for Agents - EN / ZH / GitHub Field Report (2026-11)

> **Status:** archival snapshot. Created **2026-11-02**. Safe to delete after **2027-02-02**.
> **状态：** 资料快照，创建于 2026-11-02，三个月后（2027-02-02）可删除。
> **License:** CC BY 4.0 - reuse with attribution. See [LICENSE](LICENSE).

## TL;DR

| Region | De-facto standard | Why it wins |
|---|---|---|
| **English web** | Tavily, Exa, Brave, Firecrawl, SearXNG | Native tools in LangChain/LlamaIndex, MCP distribution, independent benchmarks [E-07][E-09][E-19] |
| **Chinese web** | Bocha, Zhipu, Baidu Qianfan, Aliyun IQS, DeepSeek | FastGPT ranks Bocha #1 in its provider list; DeepSeek undercuts at CNY 5/1k [E-33][E-39] |
| **GitHub** | GitHub code search + GitHub MCP, grep.app, Sourcegraph, repomix/gitingest | 630M repos on GitHub; grep.app indexes 1M+ public repos and speaks MCP [E-23][E-24][E-25] |

**中文摘要：** 英文区默认组合是 Tavily/Exa 做搜索 + Firecrawl/Jina 读正文；中文区默认是博查（生态最全）或 DeepSeek（最便宜）；GitHub 区默认是 GitHub MCP + grep.app。三个区的分发渠道、计价单位、内容覆盖都不同，不能混着选。

## 0. Prerequisites / 先决条件

**Question.** 给 LLM / AI Agent 用的搜索工具，在中文互联网、英文互联网、GitHub 代码库三个场景里分别是什么？哪些是"很多人真的在用"，证据是什么？

**In scope.** Web search APIs, MCP search servers, code-search tools, repo-context tools, and the platforms that distribute them (LangChain, LlamaIndex, Dify, FastGPT, MaxKB, MCP registries).

**Out of scope.** 模型内置搜索的完整评测（OpenAI / Anthropic 内置工具只做定价提及）；搜索引擎排序质量的主观评测；无公开定价的私有部署；非搜索类 RAG 组件。

**Evidence standard.**

| Grade | Meaning | Examples |
|---|---|---|
| **A** | 一手、可复现 | Official pricing/docs, `gh api` measurements, Microsoft/Google announcements, open benchmark repos |
| **B** | 强二手 | Mainstream funding reports, framework repo integration lists, marketplace install counts |
| **C** | 弱 / 营销 | Vendor-run benchmarks, SEO comparison posts - used as leads only |

**Snapshot date.** 2026-11-02 (Asia/Shanghai). All star counts measured that day with `gh api repos/{owner}/{repo} --jq .stargazers_count`.

**Known limitations.** Some pricing pages render dynamically and were not captured verbatim; vendor self-reported numbers are labelled; one TinyFish research output contradicted a primary source and is flagged in section 7. Prices change fast - re-verify before procurement.

## 1. Method / 方法与检索路径

**Search matrix** (multi-engine, EN and ZH run separately):

- EN: `best web search API for AI agents 2026`, `Tavily vs Exa vs Brave comparison`, `MCP web search server`, `Exa funding Series C`, `code search tool for AI agents`
- ZH: `AI 搜索 API 对比 博查 智谱 百度`, `博查 DeepSeek 联网搜索 合作伙伴`, `Dify 搜索插件 安装量`, `秘塔 API 开放平台`, `阿里云 IQS 百度千帆 AI搜索`
- GitHub: `grep.app code search`, `GitHub MCP server code search`, `gitingest repomix deepwiki`, then verified every candidate with `gh api`

**Tooling.** Web search (Exa/Tavily/Parallel/Bing routing), direct page fetches for official docs, `gh api` for star/fork/activity, and one TinyFish Research API run (`mode=deep`, ~20 min, 48 citations) as a lead generator. Full command log in [METHOD.md](METHOD.md).

**Rule applied.** A tool is "widely used" only if it appears in at least two independent distribution layers (framework-native tool + MCP/marketplace, or framework + independent benchmark). Star count alone is never sufficient.

## 2. English Web / 英文区

### 2.1 Landscape table

| Tool | Type | USD / 1k | GH stars (measured) | Native integration evidence | Adoption / capital |
|---|---|---|---|---|---|
| **Tavily** | AI-native search + extract | 8 basic / 16 advanced | tavily-python 1,427; tavily-mcp 2,471 | LangChain `langchain-tavily` [E-07] | Acquired by Nebius, reported $275M [E-02] |
| **Exa** | Own index + neural search | 7 auto / 4 instant / 12-15 deep | exa-py 237; exa-mcp 5,208 | LangChain partners; Claude connector | $250M Series C at $2.2B [E-03] |
| **Brave Search API** | Independent index SERP | 5 | brave-search-mcp 1,553 | LangChain `brave_search`; Dify plugin | Claude search backend; 700k OpenClaw users [E-13] |
| **Firecrawl** | Crawl + `/search` | ~0.75-3.80 / 1k pages | 197,814; firecrawl-mcp 7,751 | LangChain / LlamaIndex / n8n / MCP | $75M Series B, 1.5M devs self-reported [E-06] |
| **SearXNG** | Self-host metasearch | free | 39,116 | LangChain `searx_search` [E-19] | Zero-cost default |
| **Serper.dev** | Google SERP resale | 1.00 -> 0.30 | no official SDK repo | LangChain `google_serper` | Large legacy base, weakest LLM fit |
| **SerpApi** | Multi-engine SERP | 25 | serpapi-python 179 | LangChain built-in | Sued by Google, 2025-12 [E-18] |
| **Parallel** | Agent search suite | 1 turbo / 5 basic | parallel-sdk-python 31 | LangChain [E-08] | $100M Series B at $2B [E-05] |
| **Perplexity** | Answer engine | 2.50 (Agent API) | ppl MCP 2,603 | OpenAI SDK compatible | Sonar retired 2026-09, moved to Agent API [E-22] |
| **Jina Reader** | URL -> Markdown | token-based | jina-ai/reader 12,226 | LangChain loaders [E-20] | Acquired by Elastic, 2025-10 |
| **Kagi** | Paid quality search | 12 | kagimcp 557 | MCP [E-21] | Small, loyal paid base |
| **Bing Web Search API** | - | **retired** | - | - | Retired 2025-08-11 [E-01] |

### 2.2 Three hard pieces of evidence

**1) Framework-native tool lists beat star counts.**
LangChain's classic tools directory ships search tools for: `tavily_search`, `brave_search`, `bing_search`, `google_search`, `google_serper`, `searx_search`, `ddg_search`, `searchapi`, `dataforseo`, `reddit_search`, `metaphor_search` (Exa's former name). Linkup, Valyu, Parallel, Keenable and Firecrawl are **not** in it. LlamaIndex is more open (Tavily/Exa/Brave/Jina/Linkup/Parallel/Valyu all have official packages), but "has a package" is not "default". [E-07][E-08]

**2) Independent benchmarks now exist, and they disagree with vendor marketing.**
[OpenBenchmarks](https://openbenchmarks.com/web-search/exa-vs-tavily-vs-brave-vs-serper) ran 300 company-news questions with one answering model, updated 2026-10-21, code and dataset public [E-09]:

| Config | Accuracy | Median latency | USD / 1k |
|---|---|---|---|
| Exa fast | **99.3%** | 569 ms | 7 |
| Brave llm-context | 94.0% | 590 ms | 5 |
| Tavily advanced | 93.0% | 4.2 s | 16 |
| Tavily basic | 87.7% | 1.7 s | 8 |

On the coding-agent documentation board the gap widens: **Exa deep 83% vs Tavily advanced 60%** task completion [E-10]. A separate 2025-12 snapshot (AIMultiple, 100 queries) had Brave first and Tavily fifth - ranking is task-dependent, so never trust a single board [E-12].

**3) MCP is the real distribution channel, and its popularity does not match funding.**
Measured stars: `firecrawl-mcp-server` **7,751** > `exa-mcp-server` **5,208** > Perplexity MCP **2,603** > `tavily-mcp` **2,471** > `brave-search-mcp-server` **1,553** > Jina MCP **899** > `kagimcp` **557**. Firecrawl leads because "turn a page into clean context" is a higher-frequency agent need than "return ten links" [E-06][E-29].

### 2.3 English verdict

- **Tavily = ecosystem embedment champion.** LangChain tutorials default, 1,000 free credits/month, acquired by Nebius. Benchmarks put it second tier, and its privacy policy allows query fallback to Google.
- **Exa = quality + capital champion.** $2.2B valuation, Cursor/HubSpot customers, top independent scores. Expensive on multi-hop tasks ($0.13/task in one benchmark).
- **Brave = compliance / independent-index default.** The only large vendor still selling its own index after Bing's retirement; disclosed as Claude's search backend. Performance swings by task type.
- **Firecrawl = the context layer you cannot avoid.** 197K stars, but it is a scraping/context API first and a search API second.
- **Parallel / Linkup / Valyu / Keenable = pilot candidates, not defaults.** Parallel's capital ($2B) far exceeds its developer footprint (SDK 31 stars); Keenable topped one independent board but is ~10 weeks old with undisclosed customers.

## 3. Chinese Web / 中文区

### 3.1 Landscape table

| Tool | Vendor | CNY / 1k | Integration evidence | Notes |
|---|---|---|---|---|
| **Bocha 博查** | Hangzhou Bocha (independent) | Web 36 / AI Search 60 | FastGPT PR #7022 ranks it **first**; MaxKB v1.10.3 built-in; Dify plugin 19,108 installs [E-33][E-34][E-35] | Only pure-play search vendor; pricing lives in a Feishu wiki |
| **Zhipu 智谱** | Zhipu AI | std 10 / pro 30 / sogou 50 / quark 50 | Official MCP broker; Dify plugin 2.2k installs [E-30] | Most transparent pricing; `search_pro_sogou` is the only tier that names Zhihu coverage |
| **Baidu Qianfan** | Baidu | 4.9 promo; 1,500 free/month | Qianfan AppBuilder component, MCP [E-37] | Best Chinese index; three overlapping product lines |
| **Aliyun IQS** | Alibaba Cloud | Lite 8 / Auto 18 / Generic 42 / Global 56 | Aliyun ecosystem [E-36] | Strongest compliance story; heavy jargon, little community discussion |
| **Tencent Yuanbao WSA** | Tencent Cloud | 14 / 20 / 26 | Tencent Cloud MCP plaza [E-38] | Exclusive Tencent content (news, Sogou Baike, Penguin accounts) |
| **DeepSeek Search** | DeepSeek | **5** (0.005/call) | DSH / Claude Code / Codex server-side tools [E-39] | Cheapest in the table; billing from 2026-11-01; near-zero ecosystem |
| **Metaso 秘塔** | Metaso | 30 | ModelScope official MCP [E-40] | Positioned as the Bing-retirement replacement; minimal API |
| **Kimi Web Search** | Moonshot | per-call (unit unverified) | Standalone REST `/v1/tools/search` | Pro tier returns content chunks |
| **360 Zhisou** | 360 | no public price list | Official MCP | Most engineering-heavy docs (site_weight, exclude_aigc) |

### 3.2 Three hard pieces of evidence

**1) FastGPT's provider priority is harder evidence than any review post.**
Merged [PR #7022](https://github.com/labring/FastGPT/pull/7022) (2026-05) hard-codes the search-provider order as:

```
bocha -> metaso -> brave -> serper -> tavily -> exa -> searxng
```

A Chinese open-source agent platform ranks two Chinese search vendors **ahead of** Brave, Serper, Tavily and Exa. In the same period MaxKB v1.10.3 shipped "Bocha search" as a built-in function [E-33][E-34]. That is adoption evidence, not marketing.

**2) Bocha's "60% share" must be read with its timestamp.**
Bocha's own product document (2025-03) claims 30M daily API calls, ~60% of domestic AI-app web-search requests, and being DeepSeek's search supplier; a [National Business Daily interview](https://www.nbd.com.cn/articles/2025-03-07/3779901.html) repeats it [E-31][E-32]. But this is **vendor self-report**, the denominator is undefined, and at that time DeepSeek/Kimi/Zhipu had no standalone search APIs. By 2026 DeepSeek ships its own search at CNY 5/1k - the integrated supplier became a competitor.

**3) The real gap is distribution, not price.**
English vendors distribute through two public layers (MCP + LangChain/LlamaIndex). Chinese vendors distribute through platform-specific built-ins (Dify, FastGPT, Coze, MaxKB), so the same Bocha key is configured three times. Open-source collaboration differs 26-40x: `firecrawl-mcp` 7,751 vs `bocha-search-mcp` **187**, and Bocha's official MCP has not been pushed since 2025-04 [E-44].

### 3.3 Chinese verdict

- **Coverage + ready ecosystem -> Bocha** (expensive, but works in FastGPT/MaxKB/Dify/Coze out of the box).
- **Cheap + transparent -> Zhipu `search_pro` (CNY 30/1k) or DeepSeek (CNY 5/1k, ecosystem near zero).**
- **Zhihu / Tencent content -> Zhipu `search_pro_sogou` or Tencent Yuanbao.**
- **Compliance + volume -> Aliyun IQS** (8 -> 30 CNY/1k tiering).
- **Structural content gap:** Zhihu is locked behind the Sogou ecosystem; **no vendor in the table officially claims WeChat official-account or Xiaohongshu coverage**. That is a licensing problem, not an engineering one.

## 4. GitHub / 代码区

### 4.1 Landscape table

| Tool | Type | Scale / price | GH stars (measured) | Best for |
|---|---|---|---|---|
| **GitHub code search** | Platform-native | 630M repos (395M public) [E-23] | - | Code already on GitHub, free |
| **github/github-mcp-server** | Official MCP | Free, token required | **34,156** [E-28] | Agents reading repos/files/issues/PRs |
| **grep.app (Vercel)** | Public regex code search | 1M+ repos, free, MCP [E-24][E-25] | - | "Has anyone ever written this?" |
| **Sourcegraph** | Enterprise cross-repo search | Commercial | - | Large orgs, many branches/hosts |
| **gitingest** | Repo -> prompt text | Free | 16,063 [E-29] | Feed a whole repo to an LLM |
| **repomix** | Repo packing | Free | 29,118 [E-29] | Same, broader ecosystem |
| **DeepWiki (OSS)** | Repo -> AI wiki | Free | 18,349 [E-29] | Understanding an unfamiliar repo |
| **ast-grep** | Structural code search | Free | 16,416 [E-29] | Search/rewrite by syntax tree |

### 4.2 Key judgments

**1) Scale is the moat.** 630M repos, 395M public [E-23]. No third-party index covers that. grep.app covers 1M+ public repos; Sourcegraph covers your org's private repos. They solve different problems.

**2) There is a ready-made decision rule.** [Unblocked's 2026 comparison](https://getunblocked.com/blog/ai-code-search-tools-compared/) [E-26]: more than a few dozen repos and a budget -> Sourcegraph; code already on GitHub and free -> GitHub code search; **if the consumer is a coding agent -> agentic grep** (let the agent run ripgrep/grep instead of pre-building an index).

**3) grep.app changed role after the Vercel acquisition.** Vercel's announcement says 500k+ public repos at acquisition, later "a million" [E-24]; since 2025-07 it exposes an MCP endpoint so AI apps can query that index over HTTP [E-25]. Sourcegraph's own blog lists grep.app as the first choice for companies that do not need Sourcegraph [E-27].

**4) GitHub MCP is "read", not "search".** The official 34K-star server exposes repos/issues/PRs/code_security toolsets for reading specific repos and files. Cross-repo discovery still needs code search or grep.app. Complementary, not substitutes.

### 4.3 GitHub verdict

- Agent reads a known repo -> **GitHub MCP Server**.
- Agent looks for prior art -> **grep.app**.
- Enterprise multi-repo/multi-host -> **Sourcegraph**.
- Pack a repo into context -> **repomix / gitingest**.
- Understand an unfamiliar repo -> **DeepWiki**.

## 5. Cross-region comparison / 三区对比

| Dimension | English web | Chinese web | GitHub |
|---|---|---|---|
| **Distribution** | MCP + LangChain/LlamaIndex | Dify/FastGPT/Coze/MaxKB built-ins | Platform API + MCP |
| **Pricing unit** | per request (USD 1-16/1k) | per request (CNY 5-60/1k) | free / enterprise |
| **Strongest evidence** | independent benchmarks + framework tool lists | open-source platform PR priority | repo scale + acquisitions |
| **Biggest weakness** | price; vendor benchmark spam | no independent third-party benchmark; weak UGC coverage | cross-repo discovery still needs third parties |
| **Default combo** | Tavily/Exa + Firecrawl/Jina | Bocha (ecosystem) or DeepSeek (cheap) | GitHub MCP + grep.app |

One counter-intuitive observation: Hacker News discussion of this category is unusually quiet (the Nebius/Tavily acquisition thread had ~2 points), while Reddit r/Rag and r/AI_Agents are active. Judging adoption by HN heat would badly underrate the category.

## 6. Selection guide / 选型建议（可直接复制）

| Scenario | Recommendation | Reason |
|---|---|---|
| English agent prototype | **Tavily** | LangChain default, 1,000 free/month, lowest switching cost |
| English production, quality first | **Exa** | Top independent scores, $2.2B backing, Cursor uses it |
| English, compliance / own index | **Brave** | Claude backend, $5/1k, no Google dependency |
| English, need page content not links | **Firecrawl or Jina** | 197K / 12K stars, extraction is the real need |
| Zero budget, self-host | **SearXNG** | 39K stars, LangChain built-in |
| Chinese, ready ecosystem | **Bocha** | FastGPT #1 priority, MaxKB/Dify/Coze all wired |
| Chinese, cheapest | **DeepSeek (CNY 5/1k) or Zhipu (CNY 30/1k)** | 6x price gap; DeepSeek ecosystem near zero |
| Chinese, Zhihu/Tencent content | **Zhipu `search_pro_sogou` or Tencent Yuanbao** | Only tiers that name Zhihu coverage |
| Agent reads a GitHub repo | **GitHub MCP Server** | Official, free, 34K stars |
| Agent searches across repos | **grep.app** | Free, MCP, 1M+ repos |
| Enterprise code search | **Sourcegraph** | All branches, all hosts, but budget |

## 7. Caveats / 存疑与未核实

| Item | Status |
|---|---|
| Brave's rank on OpenBenchmarks | TinyFish claimed "last of 14 at 38.0%"; the page we fetched shows Brave llm-context at 94.0%, rank 3. Treat 38% as unverified (possibly a different board). |
| Google Custom Search API sunset on 2027-01-01 | Mentioned by TinyFish, not confirmed on Google's own page. |
| Kimi search API unit price | Pricing page renders dynamically; no number captured. |
| 360 Zhisou per-tier price | No public price list. |
| Valyu pricing tiers | Only fragments on the site. |
| WeChat official-account / Xiaohongshu official API | No vendor in the table claims coverage; assumed none. |
| RAGFlow / QAnything official integration | Not found; assumed none. |
| Vendor self-reported numbers | Tavily 2M devs, Firecrawl 1.5M devs, Bocha 60% share - all self-reported. |

## 8. Reproduce / 复现

```bash
# star counts (all measured 2026-11-02)
gh api repos/github/github-mcp-server --jq .stargazers_count
gh api repos/firecrawl/firecrawl --jq .stargazers_count
gh api repos/searxng/searxng --jq .stargazers_count
gh api repos/bocha-ai/bocha-search-mcp --jq .stargazers_count

# the independent benchmark
curl -s https://openbenchmarks.com/web-search/exa-vs-tavily-vs-brave-vs-serper.md | head -80
```

Full command log: [METHOD.md](METHOD.md). Full source list: [EVIDENCE.md](EVIDENCE.md). TinyFish raw output: [tinyfish-deep-research.md](tinyfish-deep-research.md).

## 9. Citation

```
mjj2-pro. "AI Search for Agents - EN / ZH / GitHub Field Report (2026-11)."
GitHub, 2026-11-02. https://github.com/mjj2-pro/ai-search-landscape-2026
```

Corrections welcome via issues. This snapshot is intentionally frozen; newer data belongs in a new report.