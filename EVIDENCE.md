# Evidence Ledger / 证据清单

Every claim in [README.md](README.md) maps to an ID below. Captured **2026-11-02** unless stated. Grades follow README section 0: **A** = primary/reproducible, **B** = strong secondary, **C** = weak/marketing.

## English web

| ID | Claim | Source | Grade |
|---|---|---|---|
| E-01 | Bing Web Search API retired 2025-08-11; no new deployments | [Microsoft Learn lifecycle announcement](https://learn.microsoft.com/en-us/lifecycle/announcements/bing-search-api-retirement) | A |
| E-02 | Tavily acquired by Nebius; reported $275M | [Nebius newsroom](https://nebius.com/newsroom/nebius-announces-agreement-to-acquire-tavily-to-add-agentic-search-to-its-ai-cloud-platform) | A |
| E-03 | Exa raised $250M Series C at $2.2B valuation (2026-05) | [Exa blog](https://exa.ai/blog/announcing-series-c) + [Bloomberg](https://www.bloomberg.com/news/articles/2026-05-20/andreessen-backed-ai-search-startup-exa-valued-at-2-2-billion) | A/B |
| E-04 | Exa raised $85M Series B (2025-09), Benchmark led, Nvidia participated | [SiliconANGLE](https://siliconangle.com/2025/09/03/nvidia-backs-85m-round-ai-search-startup-exa/) | B |
| E-05 | Parallel raised $100M Series B at $2B (2026-04), Sequoia led | [Parallel blog](https://parallel.ai/blog/series-b) + [TechCrunch](https://techcrunch.com/2026/04/29/parallel-web-systems-hits-2b-valuation-five-months-after-its-last-big-raise/) | A/B |
| E-06 | Firecrawl raised $75M Series B; ~197K stars; 1.5M devs self-reported | [Firecrawl blog](https://www.firecrawl.dev/blog/introducing-alexandria-series-b) + [repo](https://github.com/firecrawl/firecrawl) | A/B |
| E-07 | LangChain ships `langchain-tavily` with `TavilySearch`; 1,000 free searches/month | [LangChain docs](https://docs.langchain.com/oss/python/integrations/tools/tavily_search) | A |
| E-08 | LangChain ships a Parallel search integration | [LangChain docs](https://docs.langchain.com/oss/python/integrations/tools/parallel_search) | A |
| E-09 | OpenBenchmarks 300-question company-news board (2026-10-21), code + dataset public | [OpenBenchmarks](https://openbenchmarks.com/web-search/exa-vs-tavily-vs-brave-vs-serper) | A |
| E-10 | OpenBenchmarks coding-agent board: Exa deep 83% vs Tavily advanced 60% | same page, section "Coding-agent documentation tickets" | A |
| E-11 | Vals AI Web Search Index: Keenable 49.08%, Exa 48.45%, cost per task differs 2.5x | [Vals AI](https://www.vals.ai/benchmarks/web_search) (via TinyFish, not re-run) | B |
| E-12 | AIMultiple agentic search snapshot (2025-12): Brave 14.89 first, Tavily 13.67 fifth | [AIMultiple](https://aimultiple.com/agentic-search) (via TinyFish, not re-run) | B |
| E-13 | Brave Search API approaches 700,000 OpenClaw users (2026-04-01) | [Brave blog](https://brave.com/blog/openclaw/) | B (vendor) |
| E-14 | Brave's own "best search API 2026" roundup | [Brave](https://brave.com/learn/best-search-api-2026) | C (vendor) |
| E-15 | Firecrawl pricing: Hobby $19/mo 5k credits; Search 2 credits/10 results | [Firecrawl pricing](https://www.firecrawl.dev/pricing) | A |
| E-16 | Tavily pricing: $8/1k basic, $16/1k advanced, 1,000 free credits | [Tavily pricing](https://www.tavily.com/pricing) | A |
| E-17 | Exa pricing: $7 auto, $4 instant, $12-15 deep, $1/1k pages | [Exa pricing](https://exa.ai/pricing) | A |
| E-18 | SerpApi $25/1k starter; Google sued SerpApi under DMCA (2025-12) | [SerpApi pricing](https://serpapi.com/pricing) + [Reuters/coverage via TinyFish] | A/B |
| E-19 | SearXNG: 39,116 stars; LangChain `searx_search` built-in | [repo](https://github.com/searxng/searxng) | A |
| E-20 | Jina Reader: 12,226 stars; URL-to-markdown; acquired by Elastic 2025-10 | [repo](https://github.com/jina-ai/reader) | A/B |
| E-21 | Kagi API $12/1k queries | [Kagi docs](https://help.kagi.com/kagi/api/api-portal.html) | A |
| E-22 | Perplexity retired Sonar chat API 2026-09-27, moved to Agent API | [migration doc](https://docs.perplexity.ai/docs/agent-api/migrate-from-sonar/overview) | A |

## Chinese web

| ID | Claim | Source | Grade |
|---|---|---|---|
| E-30 | Zhipu Web Search tiers: std 0.01, pro 0.03, sogou/quark 0.05 CNY per call; sogou covers Zhihu | [Zhipu docs](https://docs.bigmodel.cn/cn/guide/tools/web-search) | A |
| E-31 | Bocha: 30M daily calls, ~60% domestic share, DeepSeek supplier (2025-03) | [Bocha open platform](https://open.bochaai.com/) + [product PDF](https://netmarket.oss-cn-hangzhou.aliyuncs.com/fcc655779c6843a1b1a454da28b641b1.%E5%8D%9A%E6%9F%A5%E6%90%9C%E7%B4%A2api%E4%BA%A7%E5%93%81%E6%9C%8D%E5%8A%A1%E6%96%87%E6%A1%A3v1.0.2.pdf) | B (vendor) |
| E-32 | National Business Daily interview repeats Bocha's 30M/day and DeepSeek support | [NBD](https://www.nbd.com.cn/articles/2025-03-07/3779901.html) | B |
| E-33 | FastGPT PR #7022 hard-codes provider order `bocha -> metaso -> brave -> serper -> tavily -> exa -> searxng` | [PR #7022](https://github.com/labring/FastGPT/pull/7022) | A |
| E-34 | MaxKB v1.10.3 ships Bocha search as a built-in function | [MaxKB blog](https://blog.fit2cloud.com/?p=4c5d521c-7fc9-417a-8d8c-95f62b479ead) | B |
| E-35 | Dify Marketplace install counts: Tavily 303,340; Bocha 19,108 | [Dify verify page](https://marketplace.dify.ai/verify) (dynamic; counts from page snippets) | B |
| E-36 | Aliyun IQS tiers: Lite 8 / Auto 18 / Generic 42 / Global 56 CNY per 1k | [IQS pricing](https://www.aliyun.com/product/iqs/pricing) | A |
| E-37 | Baidu Qianfan AI search: 1,500 free calls/month, pay-as-you-go | [Baidu docs](https://cloud.baidu.com/doc/qianfan-api/s/Wmbq4z7e5) | A |
| E-38 | Tencent Yuanbao search WSA: 14/20/26 CNY per 1k | [Tencent Cloud WSA](https://cloud.tencent.com/product/wsa) | A |
| E-39 | DeepSeek Search API: CNY 5 per 1k, own engine, billing from 2026-11-01 | [DeepSeek docs](https://api-docs.deepseek.com/zh-cn/guides/search/) | A |
| E-40 | Metaso API ~CNY 30/1k, official MCP on ModelScope | [Metaso API](https://metaso.cn/search-api) + [OSCHINA](https://www.oschina.net/news/362265) | B |
| E-41 | Baidu search API connected by 625 vendors (Li Yanhong, 2025) | [AASTOCKS via Yahoo](https://hk.finance.yahoo.com/news/%E6%9D%8E%E5%BD%A5%E5%AE%8F-%E7%99%BE%E5%BA%A6-09888-hk-%E6%98%AF%E5%85%A8%E7%90%83%E6%9C%80%E6%BF%80%E9%80%B2ai%E5%8C%96%E6%94%B9%E9%80%A0%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E-024320887.html) | B |
| E-43 | Chinese cross-vendor comparison (Tavily/Bocha/Baidu/IQS), C-grade context | [lllyyb](https://www.lllyyb.com/archives/gsWnWneO) | C |
| E-44 | `bocha-search-mcp` 187 stars vs `firecrawl-mcp` 7,751; Bocha MCP last push 2025-04-14 | [repo](https://github.com/bocha-ai/bocha-search-mcp) | A |

## GitHub

| ID | Claim | Source | Grade |
|---|---|---|---|
| E-23 | GitHub hosts 630M repos, 395M public (Octoverse 2025) | [GitHub Blog](https://github.blog/news-insights/octoverse/octoverse-a-new-developer-joins-github-every-second-as-ai-leads-typescript-to-1/) | A |
| E-24 | Vercel acquired grep.app; 500k+ public repos at acquisition, later 1M+ | [Vercel blog](https://vercel.com/blog/vercel-acquires-grep) + [grep.app](https://grep.app/) | A/B |
| E-25 | grep.app exposes MCP endpoint (2025-07) | [Vercel changelog](https://vercel.com/blog/grep-a-million-github-repositories-via-mcp) | A |
| E-26 | 2026 code-search decision rule: Sourcegraph vs GitHub code search vs agentic grep | [Unblocked](https://getunblocked.com/blog/ai-code-search-tools-compared/) | B |
| E-27 | Sourcegraph lists grep.app as first choice for non-Sourcegraph companies | [Sourcegraph blog](https://sourcegraph.com/blog/tools-for-companies-that-dont-need-sourcegraph) | B |
| E-28 | github/github-mcp-server: 34,156 stars, official MCP, repos/issues/PR toolsets | [repo](https://github.com/github/github-mcp-server) | A |
| E-29 | gitingest 16,063; repomix 29,118; deepwiki-open 18,349; ast-grep 16,416 | repos: [gitingest](https://github.com/cyclotruc/gitingest), [repomix](https://github.com/yamadashy/repomix), [deepwiki](https://github.com/AsyncFuncAI/deepwiki-open), [ast-grep](https://github.com/ast-grep/ast-grep) | A |

## Research-tool evidence (for section 7 of README)

| ID | Claim | Source | Grade |
|---|---|---|---|
| E-42 | TinyFish Research API: `POST /v1/automation/run-research`, X-API-Key, modes deep/max, 2 free runs/UTC day, then $2/$3 per run | [Research API docs](https://docs.tinyfish.ai/research-api) + [reference](https://docs.tinyfish.ai/research-api/reference) | A |
| E-45 | TinyFish run completed in ~20 min, returned 48 citations (this session) | raw output: [tinyfish-deep-research.md](tinyfish-deep-research.md) | A (observed) |

## Primary quotes / 关键原文摘录

**Bing retirement (E-01).** Microsoft: the Bing Search APIs are retired; new deployments are no longer possible and existing instances are decommissioned. This removed the decade-old default "buy a web index for $3-7/1k" option.

**Bocha product doc (E-31).** "截至 2025 年 3 月，博查搜索 API 日均调用量已突破 3000 万次，承接了国内 AI 应用 60%的联网搜索请求……博查是 DeepSeek 联网搜索的供应商。" Note the date: March 2025, before DeepSeek/Kimi/Zhipu shipped standalone search APIs.

**FastGPT PR #7022 (E-33).** Provider priority in code:

```
bocha -> metaso -> brave -> serper -> tavily -> exa -> searxng
```

**Zhipu pricing table (E-30).** `search_std` 0.01 CNY/call; `search_pro` 0.03; `search_pro_sogou` 0.05; `search_pro_quark` 0.05. The sogou tier is documented as covering Tencent ecosystem and Zhihu.

**OpenBenchmarks method (E-09).** Same 300 natural-language company-news questions, one search per question, up to 10 results, one answering model, accuracy = whether results let the model extract the pinned value. Runner and dataset public.

## Grading notes

- **Vendor self-reports** (Bocha 60%, Tavily 2M devs, Firecrawl 1.5M devs, Brave 700k OpenClaw users) are marked B and must not be treated as audited.
- **TinyFish-derived** figures (Vals AI, AIMultiple, SerpApi lawsuit) are B because we did not re-run them; the URLs are provided for independent verification.
- **C-grade** items are listed for completeness and were not used as decision inputs.