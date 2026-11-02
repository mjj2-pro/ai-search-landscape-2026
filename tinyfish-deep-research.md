# TinyFish Deep Research - Raw Output (archived)

> **Archival note.** This is the unedited output of one TinyFish Research API run (`mode=deep`, 2026-11-02, ~20 minutes, 48 citations). It is included as raw material, **not** as verified fact. Where it contradicts a primary source, [README.md](README.md) section 7 flags it. Treat every number here as a lead to verify against the cited URL.
>
> Why archive it: it surfaced leads the manual search missed - Vals AI independent benchmark, Keenable, Perplexity's Sonar-to-Agent-API migration, Jina's acquisition by Elastic, and the Reddit/Google lawsuits. Those leads were then checked separately; see EVIDENCE.md grades.

---

# Web Search APIs for AI Agent Developers: A Decision-Maker's Research Report
## As of Late 2026

---

## Executive Summary

The market for web search APIs serving AI agent developers has consolidated around a clear tier structure. **Exa** and **Firecrawl** have the strongest combination of verified adoption signals (funding, framework integrations, GitHub traction, and independent benchmark performance). **Brave Search API** leads on independent benchmark scores but has a thinner integration footprint. **Tavily** remains the most deeply embedded in the LangChain/LlamaIndex tutorial ecosystem and reports the largest developer user base, but has faced acquisition uncertainty and benchmarks below the top tier. **Parallel Web Systems** has the most impressive venture backing for its age ($230M total) and strong latency numbers. **Perplexity** pivoted away from Sonar to an Agent API in September 2026. **Jina AI** was acquired by Elastic in late 2025 and now occupies a niche URL-to-markdown role. **Linkup** is a credible but early-stage seed entrant. **Keenable** just emerged from stealth in August 2026 with $26M and topped the Vals AI benchmark with GPT-5.6 Sol, but has almost no public customer evidence. **Valyu** ran its own benchmark (self-reported, not independent) and claims strong accuracy on paywalled/academic sources. **Firecrawl** stands out with ~197K GitHub stars and $75M Series B.

The most important methodological warning for decision-makers: **every benchmark in this space is either vendor-funded, benchmarked at a single point in time, or uses a different test harness**. No single "ground truth" ranking exists. Treat all performance claims with appropriate skepticism.

---

## Section 1: Market Context

Several macro shifts define the current landscape:

- **Microsoft retired all Bing Search APIs on August 11, 2025**, forcing a large cohort of developers to find alternatives [10][18]. This accelerated growth for nearly every provider covered here.
- **Google's Custom Search JSON API is closed to new customers** and sunsets for existing customers on January 1, 2027 [18].
- **Cloudflare began blocking AI crawlers by default starting July 1, 2025**, complicating web-scale indexing for newer entrants [20].
- **US v. Google** (final judgment December 5, 2025) requires Google to share index data with qualified competitors, but as of late August 2026 no competitor had yet received access [20].
- **Reddit sued Perplexity, SerpApi, Oxylabs, and AWMProxy** in October 2025 for alleged industrial-scale scraping [20].
- **Google sued SerpApi** under DMCA §1201 in December 2025; SerpApi filed a motion to dismiss in February 2026 [20].

These legal and infrastructure shifts make API selection a **strategic risk decision**, not just a performance decision. Providers with independent indexes (Brave, Exa, Parallel, Keenable) carry less legal exposure than meta-search wrappers. Tavily's privacy policy explicitly states query data may be passed to Google when its own index cannot retrieve content [35], which is a compliance consideration for enterprise teams.

---

## Section 2: Provider-by-Provider Analysis

### 2.1 Tavily

**Verified evidence summary:**

| Dimension | Evidence | Source Quality |
|---|---|---|
| Funding | $25M total: ~$5M seed (mid-2024) + $20M Series A (Insight Partners, Alpha Wave Global, August 2025) | Primary [36][45] |
| Acquisition | Nebius acquired 100% on February 19, 2026; Nebius recorded $189.4M in acquisition consideration | Primary [43] |
| Reported deal size | SiliconANGLE/Calcalist reported $275M initial payment, potentially rising to $400M on milestones | Secondary [35] |
| Developer count | "Over 2 million developers" and "300 million monthly requests" (August 2026, self-reported) | Primary [43] |
| Earlier self-reported metrics | "Over 700,000 users," "over a million monthly installs," "100,000 GitHub mentions" (at Series A) | Primary [45] |
| GitHub stars (langchain-tavily repo) | 25 stars, 17 forks, 201 commits | Primary [2] |
| Framework integrations confirmed | LangChain (default in LangSmith Agent Builder), LlamaIndex, MCP (mcp.tavily.com), AWS/Azure/Snowflake/Databricks marketplaces | Secondary/Primary [12][6] |

**Pricing (verified):**
- Free: 1,000 credits/month, no card required [31]
- Pay-as-you-go: $0.008/credit -> **$8 per 1,000 basic searches** (1 credit each), **$16 per 1,000 advanced searches** (2 credits each) [31][18]
- Monthly plans: $30/mo (4,000 credits, $0.0075/credit) through $500/mo (100,000 credits, $0.005/credit) [31]
- At the Growth plan rate: **$5 per 1,000 basic searches**

**Performance benchmarks:**
- AIMultiple agentic search benchmark (100 queries, December 2025 snapshot): Tavily scored 13.67, ranked fifth of eight, at 998ms average latency. Brave's lead over Tavily was the only statistically meaningful gap in the test [19][10].
- Parallel's BrowseComp (September 2026): Tavily scored 66% at the frontier tier for $935 per 1,000 questions - notably expensive versus Perplexity at 74% for $275 [13].
- OpenBenchmarks (September 2026): Tavily basic measured at 1.88s mean latency on factual lookup, among the slower engines [13].

**Key risks and qualifications:**
- Tavily does not publish a reproducible public accuracy benchmark [23].
- Privacy policy allows query data to pass to Google as fallback [35].
- Post-acquisition integration into Nebius introduces operational uncertainty.
- Tavily's LangChain integration repo has only 25 GitHub stars [2], suggesting the integration is distributed via the main LangChain package rather than through this repo - but this also means it is harder to independently measure community engagement.
- One GitHub user report cited issues with JS-rendered pages and cached results [5].

**Assessment:** Tavily's value is primarily **ecosystem embeddedness** - it is the default tool in countless LangChain tutorials and agent starter kits, and the 2M developer figure, even if self-reported, reflects genuine mindshare. Its benchmark performance trails the top tier, and its post-acquisition trajectory is uncertain. Best suited for prototyping and LangChain-heavy stacks where switching costs are low.

### 2.2 Exa AI

**Verified evidence summary:**

| Dimension | Evidence | Source Quality |
|---|---|---|
| Funding | $357M+ total: ~$22M Series A (July 2024, Lightspeed) -> $85M Series B (~$700M valuation, September 2025, Benchmark) -> $250M Series C ($2.2B valuation, May 2026, a16z) | Primary [29][20][27] |
| Revenue estimate | Sacra estimates $100M annualized revenue in September 2026, up from $14M at end of 2025 | Low [27] |
| Developer/company count | Self-reported: 400,000+ developers, 5,000+ companies (at Series C announcement, May 2026) | Primary [29][20] |
| Named customers | Cursor, Cognition, HubSpot, OpenRouter, Monday.com | Primary [29] |
| Framework integrations | LangChain, LlamaIndex, MCP (mcp.exa.ai/mcp, works anonymously), OpenAI SDK compatibility | Primary/Secondary [6][12] |
| Index | Crawlers track 500B+ URLs, own neural search index | Primary [29][20] |

**Pricing (verified):**
- Standard/Auto search: $7/1,000 requests [35][18]
- Instant/Lite: $4/1,000 [35][18]
- Deep search: $12-15/1,000 [27][18]
- Page contents: $1/1,000 pages [35]
- Free tier: $10 monthly credit + $10 onboarding bonus [18]
- **Effective cost per 1,000 standard searches: $7** (pay-as-you-go)

**Performance benchmarks:**
- AIMultiple (December 2025): Exa ranked third at 14.39, statistically tied with top tier (Brave 14.89, Firecrawl 14.58) [19].
- Vals AI Web Search Index (late 2026): Claude Fable 5 + Exa ranked second at 48.45% overall (finance + legal); GPT-5.6 Sol + Exa ranked third at 45.24% but was the **most expensive option at $18.97/task** [42].
- OpenBenchmarks (September 2026): Exa Instant at 398ms mean latency on factual lookup, second only to Parallel Turbo at 348ms [13].

**Assessment:** Exa has the strongest VC validation of any pure-play search API (a16z at $2.2B valuation, Sacra-estimated $100M ARR), named enterprise customers, and strong benchmark performance. Its neural/semantic search differentiator is real and documented. The main concern is **cost** - Exa is consistently among the most expensive per task in multi-hop agentic workflows once content retrieval is factored in. Best suited for semantic similarity tasks, research agents, and cases where result quality justifies premium pricing.

### 2.3 Brave Search API

**Verified evidence summary:**

| Dimension | Evidence | Source Quality |
|---|---|---|
| Index size | Self-reported: 30-40B+ pages, 100M+ daily updates, independent index (no Google/Bing dependency) | Official [6][8][10] |
| Backing | Division of Brave Software; no separate funding disclosed; reported 50x API growth since Q1 2024 | Reported [8] |
| Disclosed usage | Backend for Anthropic Claude web search (listed as subprocessor, March 2025, confirmed July 2026); backend for Mistral Le Chat | Reported [10][20] |
| SOC 2 | Type 2 certified, GDPR compliant, Zero Data Retention available for enterprise | Official [7][8] |
| Framework integrations | Dify (official plugin in Dify Marketplace) [39]; LangChain (community); MCP (official @brave/brave-search-mcp-server) [46] | Official |

**Pricing:**
- Web Search: **$5 per 1,000 requests** [35][10]
- Free: $5 monthly credit (card required); free tier eliminated February 2026 [12][20]
- LLM Context endpoint: ~$5/1,000 (same tier) [17]
- Answers plan: $4/1,000 + $5/million tokens [19]

**Performance benchmarks:**
- AIMultiple (December 2025): Brave ranked first at 14.89 and lowest latency at 669ms. However, the top four (Brave, Firecrawl, Exa, Parallel) are described as statistically indistinguishable [19][35].
- Artificial Analysis Search Index (September 2026): Brave LLM Context mode scored 75, level with Parallel Advanced, behind Perplexity Search medium (80) [13].
- OpenBenchmarks: Brave ranked last of 14 configurations at 38.0% task completion - a striking reversal from AIMultiple [35].

**Assessment:** Brave's independent index is a genuine differentiator and its role as Anthropic Claude's disclosed search backend is strong independent validation of production-scale reliability. The contradictory benchmark results (first in AIMultiple, last in OpenBenchmarks) indicate that its performance is **query-type dependent** - strong on fresh factual lookup, weaker on complex multi-hop tasks.

### 2.4 Firecrawl

**Verified evidence summary:**

| Dimension | Evidence | Source Quality |
|---|---|---|
| GitHub stars | ~197,700 (confirmed from GitHub repo page, November 2026) | Primary [3][47] |
| Funding | $14.5M Series A (Nexus, August 2025) + $75M Series B (Smash Capital, 2026) | Primary [33] |
| Developer count | 1.5M+ developers, 150,000+ companies (self-reported) | Primary [33][24] |
| Named customers | Shopify, Apple, Lovable, Canva, DoorDash | Secondary [20][24] |
| Framework integrations | LangChain, LlamaIndex, CrewAI, n8n, Zapier, MCP (13-tool remote-hosted server), CLI | Primary [3][34] |
| License | AGPL-3.0 open source with hosted cloud service | Primary [3] |

**Pricing:**
- Free: 1,000 credits/month [10]
- Search: 2 credits per 10 results -> effectively **$0.75-$3.80 per 1,000 pages** on monthly plans [18]
- Hobby: $19/mo (5,000 credits) or $16/mo billed annually [10]
- Standard: ~$83/mo for 100K credits [34]
- Scale: ~$599-$749/mo for 1M credits [20]

**Assessment:** Firecrawl is fundamentally a **context API** - it combines search, full-page scraping, crawling, document parsing, and browser interaction in one pipeline. The 197K GitHub stars vastly exceed all other providers and reflect its popularity as a scraping/extraction tool for AI workflows, not just a search API. Excellent for agents needing full-page content extraction alongside search.

### 2.5 Linkup

- Funding: $10M seed led by Gradient, February 2026 [10][20]
- Named customers: KPMG, Artisan (self-reported) [10]
- GitHub (langchain-linkup): 6 stars - very limited [41]
- Pricing: standard search **$5 per 1,000 requests**; deep search $50 per 1,000; $20 monthly credit [18][10]
- Benchmark: claims 92-94% F-score on Verified SimpleQA, 61% on SealQA-0; open-source eval harness [23]

**Assessment:** Legitimate seed-stage entrant with transparent benchmarking methodology and a real LangChain integration. However, the lack of independent adoption evidence beyond the integration repo makes this a **watch-and-wait** position for most buyers.

### 2.6 Valyu

- Benchmark: ran own benchmark (FreshQA 79%, SimpleQA 94%, Finance 73%, Economics 73%, MedAgent 48%) - self-published, October 2025 [11]
- Coverage focus: web search + SEC filings, clinical trials, patents, PubMed, financial data via single API [20]
- **Critical caveat:** entirely self-reported and self-designed [11]. The Vals AI benchmark does not include Valyu [42].

**Assessment:** Differentiation proposition (paywalled academic and financial sources) is potentially valuable for research-heavy agents, but there is **insufficient independent evidence**. Treat as unproven until it appears in an independent benchmark.

### 2.7 Parallel Web Systems

- Founders: Parag Agrawal (ex-Twitter CEO), Travers Nisbet; founded 2023 [22]
- Funding: $30M seed + $100M Series A ($740M valuation, Nov 2025) + $100M Series B ($2B valuation, April 2026, Sequoia) = $230M [22]
- Developer count: 100,000+ (self-reported) [22]
- Named customers: Harvey, Notion, Opendoor, Granola, Dropbox, Clay, Kepler [22][20]
- Commercial launch: August 2025 [22]
- Framework integrations: LangChain (confirmed) [40], MCP (search.parallel.ai/mcp, no key required), OpenAI-compatible Responses API [40][12][28]
- Pricing: Turbo/Fast **$1 per 1,000**; Basic/Advanced **$5 per 1,000**; $5 monthly credit; Extract $1/1,000 URLs [12][10][18]
- Benchmarks: AIMultiple fourth at 14.21 but 13.6s latency [19]; Artificial Analysis 75 [13]; OpenBenchmarks Turbo first on latency at 348ms [13]

**Assessment:** Most impressive institutional VC backing in this cohort, credible founding team, lowest Turbo latency. Product is young (commercial launch August 2025) and the SDK ecosystem is still maturing. Strong choice for enterprises willing to work with a newer vendor.

### 2.8 Keenable

- Stealth exit: August 25, 2026 [14][32]
- Funding: $26M seed led by Accel, with Conviction Partners [14][32]
- Team: Andrey Styskin (ex-Yandex search/AI/cloud lead), Matthias Petri (ex-Amazon AGI) [32][14]
- Index size: self-reported 100B+ documents [14][32]
- Customers: "a handful of AI labs" in production (unnamed) [14][32]
- Pricing: **$1 per 1,000 API requests** [32]
- Vals AI ranking: GPT-5.6 Sol + Keenable **49.08% overall (first)**; 53.9% finance, 44.2% legal [42][38]

**Assessment:** Only weeks old as of late 2026 and its customer list is entirely undisclosed. However, the Vals AI benchmark is the strongest independently verified evidence for any provider in this comparison. At $1/1,000 requests, pricing is competitive. Main risks: extreme youth, no public customers.

### 2.9 Perplexity Sonar -> Agent API

- Platform pivot: Sonar Chat Completions API ended September 27, 2026; replaced by Agent API [15][18]
- Current pricing (Agent API): web_search standard **$2.50 per 1,000 invocations**; Fast Search **$1.00 per 1,000** [26]
- MCP: supports MCP server connections via Agent API [15]
- Benchmark: AIMultiple 12.96 seventh of eight [19]; Artificial Analysis Search medium 80 ranked first [12]; OpenBenchmarks first at 77.3% task completion [35]

**Assessment:** Best performance on complex reasoning-plus-search tasks according to Artificial Analysis and OpenBenchmarks, at a competitive $2.50-$5/1,000. The platform pivot introduces integration risk. Not ideal for raw SERP use cases.

### 2.10 Jina AI

- Acquisition: acquired by Elastic (NYSE: ESTC), completed October 9, 2025 [20]
- Reader GitHub stars: ~12,200 [21]
- Product: r.jina.ai URL-to-markdown; s.jina.ai search -> visits top 5 results -> LLM-ready markdown [21]
- License: Apache-2.0 [21]
- Pricing: $0.05 per million response tokens [18][34]

**Assessment:** Fills a narrow niche: free or near-free URL-to-markdown conversion for RAG pipelines where you already know which URLs to fetch. Not competitive as a general-purpose web search API. Its future as part of Elastic is uncertain from a developer API perspective.

---

## Section 3: Third-Party Benchmarks - What to Trust

### 3.1 Vals AI Web Search Index (Most Independent)

- 450 finance analysis questions (FAB v2) + 208 expert-authored legal research tasks; agent harness and model held constant [42][38]
- Providers tested: Native (no external search), Exa, Keenable [42]

| Rank | Model | Search Tool | Score | Cost/Task |
|---|---|---|---|---|
| 1 | GPT-5.6 Sol | Keenable | 49.08% | $8.84 |
| 2 | Claude Fable 5 | Exa | 48.45% | $3.48 |
| 3 | GPT-5.6 Sol | Exa | 45.24% | $18.97 |

**Limitation:** Only three configurations tested; Brave, Tavily, Perplexity, Parallel, Firecrawl, Linkup, Valyu are **not evaluated** [42].

### 3.2 AIMultiple Agentic Search Benchmark (December 2025 Snapshot)

100 AI/LLM queries, 4,000 retrieved results, scored by GPT-5.2 with 10% human verification [19].

| Rank | Provider | Agent Score | Avg Latency |
|---|---|---|---|
| 1 | Brave Search | 14.89 | 669ms |
| 2 | Firecrawl | 14.58 | 1,335ms |
| 3 | Exa | 14.39 | ~1,200ms |
| 4 | Parallel Pro | 14.21 | 13,600ms |
| 5 | Tavily | 13.67 | 998ms |
| 6 | Parallel Base | 13.50 | ~2,900ms |
| 7 | Perplexity | 12.96 | 11,000ms+ |
| 8 | SerpAPI | 12.28 | - |

**Caveat:** top four statistically indistinguishable; 10% human verification only [19].

### 3.3 Artificial Analysis Search Index (September 2026)

25 search API products [12]: Perplexity Search medium 80; Octen Search 77; Parallel Search advanced 75; Brave LLM Context 75.

### 3.4 OpenBenchmarks (September 2026)

Task completion: Perplexity 77.3% -> Exa Fast 66.3% -> Tavily Basic 51.0% -> Brave last at 38.0% [35]. Latency leaders: Parallel Turbo 348ms -> Exa Instant 398ms -> Brave 601-630ms -> Tavily Basic 1,880ms [13].

**Our note (not TinyFish's):** the OpenBenchmarks page we fetched directly on 2026-11-02 shows Brave llm-context at 94.0% (rank 3) on the company-news board, contradicting the "38.0% last" claim above. This is flagged in README section 7.

### 3.5 Vendor-run benchmarks (treat as marketing)

- Parallel BrowseComp: Perplexity 74% at $275/1k; Parallel Advanced 74% at $399; Exa 70% at $971; Tavily 66% at $935 [13]
- Valyu self-benchmark: Valyu first across all categories, self-designed and self-scored [11]
- Keenable NEEDLE: claims superiority over Tavily/Exa/Perplexity, self-reported [32]

---

## Section 4: Framework Integration Matrix

| Provider | LangChain | LlamaIndex | Dify | n8n | MCP Official |
|---|---|---|---|---|---|
| Tavily | Confirmed [2] | Reported [6][12] | Not confirmed | Not confirmed | mcp.tavily.com [6] |
| Exa | Reported [12][6] | Reported [12] | Not confirmed | Not confirmed | mcp.exa.ai/mcp [6] |
| Brave | Community | Not confirmed | Confirmed [39] | Not confirmed | @brave/brave-search-mcp-server [46] |
| Firecrawl | Reported [34] | Reported [34] | Not confirmed | Confirmed [3] | firecrawl-mcp [3] |
| Linkup | Confirmed [41] | Self-claimed [23] | Not confirmed | Self-claimed [23] | Self-claimed [23] |
| Parallel | Confirmed [40] | Not confirmed | Not confirmed | Not confirmed | search.parallel.ai/mcp [6] |
| Perplexity | Not confirmed | Not confirmed | Not confirmed | Not confirmed | via Agent API [15] |
| Jina AI | LangChain loaders [34] | Not confirmed | Not confirmed | Not confirmed | URL extraction MCP [17] |

**Note:** the modelcontextprotocol/servers repo is a reference collection, not a comprehensive registry [46].

---

## Section 5: Pricing Comparison

| Provider | Per 1,000 Basic | Per 1,000 Deep | Free Tier |
|---|---|---|---|
| Tavily | $8 (PAYG) / $5 (Growth) | $16 advanced | 1,000 credits/mo |
| Exa | $7 auto / $4 instant | $12-15 deep | $10/mo + $10 onboarding |
| Brave | $5 flat | $5 (LLM Context) | $5/mo credit |
| Firecrawl | ~$0.75-3.80/1k pages | Scale plan | 1,000 credits/mo |
| Linkup | $5 | $50 | $20/mo eligible |
| Parallel | $1 turbo / $5 basic | $5 advanced | $5/mo credit |
| Keenable | $1 | Not published | Not confirmed |
| Perplexity | $2.50 standard / $1 fast | $5 full | None |
| Jina AI | ~$0.10-0.25/1k pages | same | 10M tokens one-time |
| Valyu | Not confirmed | Not confirmed | Free trial reported |

---

## Section 6: Funding Summary

| Provider | Total | Latest | Backers |
|---|---|---|---|
| Exa | ~$357M | $250M C @ $2.2B | a16z, Benchmark, Lightspeed |
| Parallel | $230M | $100M B @ $2B | Sequoia, Kleiner Perkins, Index |
| Firecrawl | ~$96M | $75M B | Smash Capital, Nexus, YC |
| Tavily | Acquired | Nebius, ~$189M consideration | Insight, Alpha Wave |
| Keenable | $26M | seed | Accel, Conviction |
| Linkup | $10M | seed | Gradient |
| Jina AI | ~$39M | acquired by Elastic | Elastic |
| Perplexity | ~$900M+ | $500M+ in 2025 | Softbank, IVP, NEA |

---

## Section 7: Decision Framework

**Tier 1 (strongest evidence):** Exa, Firecrawl.
**Tier 2 (strong evidence, caveats):** Brave, Tavily, Parallel, Perplexity.
**Tier 3 (watch list):** Keenable, Linkup, Valyu, Jina.

---

## Section 8: Key Risks

1. **Legal/scraping liability** - Reddit and Google lawsuits; independent-index providers carry less exposure.
2. **Benchmark gaming** - every provider except Tavily publishes a benchmark showing itself first.
3. **Platform stability** - Bing retired 2025-08; Perplexity Sonar retired 2026-09; Google CSE sunsets 2027-01.
4. **Cost modeling complexity** - per-request vs per-page vs per-token metrics are not comparable.
5. **Acquisition uncertainty** - Tavily (Nebius) and Jina (Elastic) now have non-search parents.

---

## Citations (48)

1. https://www.confident-ai.com/knowledge-base/compare/best-web-search-apis-grounding-llms-reducing-hallucinations-2026
2. https://github.com/tavily-ai/langchain-tavily
3. https://github.com/firecrawl/firecrawl
4. https://fastcrw.com/blog/search-api-for-ai-agents
5. https://michaellivs.com/blog/web-search-for-agents-2026/
6. https://www.braintrust.dev/articles/best-web-search-apis-mcps-ai-agents-2026
7. https://oxylabs.io/blog/best-web-search-apis
8. https://www.vellum.ai/blog/best-web-search-apis-and-mcps-for-ai-agents
9. https://sfailabs.com/guides/best-ai-search-apis-for-agents-2026
10. https://growthner.com/blog/best-ai-search-apis-for-agents-and-llm-apps/
11. https://www.valyu.ai/blogs/benchmarking-search-apis-for-ai-agents
12. https://parallel.ai/articles/the-honest-2026-comparison-web-search-apis-for-ai-agents
13. https://parallel.ai/articles/most-powerful-search-api-for-ai
14. https://techcrunch.com/2026/08/25/accel-backed-keenable-is-indexing-the-web-for-ai-agents/
15. https://www.perplexity.ai/hub/blog/agent-api-one-place-to-build-with-llms-the-web-and-agents
16. https://www.activepieces.com/blog/perplexity-sonar-api-cost-per-search-2026-guide
17. https://www.nimbleway.com/blog/top-web-search-mcps
18. https://serpex.dev/blog/best-ai-ready-search-apis-for-llms-agents-in-2025-serpexdev-vs-tavily-vs-bright-data
19. https://aimultiple.com/agentic-search
20. https://chierhu.medium.com/ai-search-api-wars-who-will-own-the-web-for-ai-agents-bf90b0663d6f
21. https://github.com/jina-ai/reader
22. https://en.wikipedia.org/wiki/Parallel_Web_Systems
23. https://www.linkup.so/blog/tavily-alternative-web-search-api-comparison
24. https://dealroom.co/news/155341-firecrawl-raises-75m-series-b-to-build-a-knowledge-library-for-ai-agents/
25. https://katteb.com/blog/tavily-ai-agent/
26. https://docs.perplexity.ai/docs/getting-started/pricing
27. https://sacra.com/c/exa/
28. https://sacra.com/c/parallel/
29. https://exa.ai/blog/announcing-series-c
30. https://www.tavily.com/pricing
31. https://docs.tavily.com/documentation/api-credits
32. https://siliconangle.com/2026/08/25/agentic-web-search-infrastructure-startup-keenable-raises-26m/
33. https://www.firecrawl.dev/blog/introducing-alexandria-series-b
34. https://blog.apify.com/jina-ai-vs-firecrawl/
35. https://www.beri.net/article/tavily-vs-exa-vs-brave-vs-perplexity-search-api-agent-cost-2026
36. https://www.insightpartners.com/ideas/tavily-raises-25-million-to-power-the-internet-of-agents/
37. https://keenable.ai/blog/keenable-raised-26m-to-beat-google-in-the-agentic-search-market
38. https://keenable.ai/blog/keenable-vals-web-search-index
39. https://dify.ai/blog/dify-x-brave-search-supercharging-ai-apps-with-real-time-search
40. https://docs.langchain.com/oss/python/integrations/tools/parallel_search
41. https://github.com/LinkupPlatform/langchain-linkup
42. https://www.vals.ai/benchmarks/web_search
43. https://ai.engineer/orgs/tavily
44. https://www.elastic.co/customers/tavily
45. https://www.tavily.com/blog/big-news-from-tavily-announcing-25m-series-a-to-power-the-internet-of-agents
46. https://github.com/modelcontextprotocol/servers
47. https://www.star-history.com/firecrawl/firecrawl
48. https://www.agenthivex.com/agent/jina-ai-reader/

---

## Our assessment of this run

**Usefulness: 4/5.** It surfaced leads our manual search missed: Vals AI, Keenable, Perplexity's Sonar retirement, Jina/Elastic, the Reddit and Google lawsuits, and Tavily's Google-fallback privacy clause. All of these were then checked against primary sources where possible.

**Problems:**
- It contradicts a primary source: it says Brave scored 38.0% and ranked last on OpenBenchmarks; the page we fetched shows 94.0%, rank 3. Do not trust its benchmark synthesis without checking.
- It reports vendor self-reports (Tavily 2M devs, Exa $357M total) without a confidence label.
- It is overconfident on rankings despite acknowledging benchmark variance.

**Recommended use:** lead generator for names, funding, lawsuits and leaderboards. Re-verify every number against the cited URL. Budget: 2 free runs per UTC day, then $2 (deep) / $3 (max) per completed run.