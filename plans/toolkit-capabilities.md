# Composio Toolkit 能力清单

> 共 **1000 个 Toolkit，40,000+ 工具**，覆盖 50+ 场景类别。  
> 通过 `composio.toolkits.get()` 查询全部，`composio.tools.getRawComposioTools({ toolkits: ['<slug>'] })` 获取具体工具。

---

## 目录

1. [邮件与通讯](#1-邮件与通讯)
2. [文件存储与文档](#2-文件存储与文档)
3. [代码与开发](#3-代码与开发)
4. [项目管理](#4-项目管理)
5. [CRM 与销售](#5-crm-与销售)
6. [客户支持](#6-客户支持)
7. [数据库](#7-数据库)
8. [数据分析与 BI](#8-数据分析与-bi)
9. [AI 与搜索](#9-ai-与搜索)
10. [网页爬取](#10-网页爬取)
11. [营销](#11-营销)
12. [电商](#12-电商)
13. [财务与支付](#13-财务与支付)
14. [图像与设计](#14-图像与设计)
15. [视频与音频](#15-视频与音频)
16. [社交媒体](#16-社交媒体)
17. [日历与会议](#17-日历与会议)
18. [教育](#18-教育)
19. [HR 与招聘](#19-hr-与招聘)
20. [其他实用工具](#20-其他实用工具)

---

## 1. 邮件与通讯

### 邮件收发

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `gmail` | Gmail | 60 | 读写邮件、创建草稿、添加标签、管理过滤器、搜索邮件 |
| `outlook` | Outlook | 301 | 收发邮件、管理日历事件、联系人管理、邮件规则创建 |
| `yandex` | Yandex Mail | 21 | Yandex 邮件的读写与管理 |
| `zoho_mail` | Zoho Mail | 15 | Zoho 邮件收发、文件夹管理 |
| `resend` | Resend | 62 | 通过 API 发送事务性邮件 |
| `missive` | Missive | 41 | 团队协作邮件、共享收件箱管理 |

### 即时通讯

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `slack` | Slack | 151 | 发送消息、管理频道、上传文件、添加表情、管理用户 |
| `slackbot` | Slackbot | 87 | Slack Bot 自动化：发消息、管理提醒、处理 DM |
| `microsoft_teams` | Microsoft Teams | 164 | 发消息、管理团队/频道、会议管理、文件共享 |
| `discord` | Discord | 16 | 获取服务器信息、频道管理、消息操作 |
| `discordbot` | Discord Bot | 165 | Discord Bot 全功能：发消息、管理角色、管理成员 |
| `whatsapp` | WhatsApp | 17 | WhatsApp Business API：发消息、管理消息模板 |
| `dialpad` | Dialpad | 192 | 云电话、联系中心：通话记录、短信、联系人管理 |
| `sendbird` | Sendbird | 37 | 应用内聊天 API、消息管理 |

---

## 2. 文件存储与文档

### 云存储

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `googledrive` | Google Drive | 89 | 上传/下载文件、共享、搜索、复制、移动 |
| `one_drive` | OneDrive | 61 | 文件上传/下载、共享权限管理、版本历史 |
| `dropbox` | Dropbox | 177 | 文件同步、共享、版本回滚、团队文件夹管理 |
| `share_point` | SharePoint | 90 | 企业文档管理、内容发布、页面创建 |
| `box` | Box | 32 | 企业云存储、文件协作、安全共享 |

### 文档编辑

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `googledocs` | Google Docs | 35 | 创建/编辑文档、插入内容、导出、协作评论 |
| `googlesheets` | Google Sheets | 46 | 读写表格数据、批量操作、数据聚合、创建图表 |
| `notion` | Notion | 47 | 创建/编辑页面、管理 Database、追加内容块 |
| `confluence` | Confluence | 62 | 创建博客/页面、搜索内容、管理标签 |
| `text_to_pdf` | Text to PDF | 6 | 将文本/HTML 转换为 PDF 文件 |
| `pdf_co` | PDF.co | 35 | PDF 提取、合并、分割、转换、填充表单 |
| `docusign` | DocuSign | 339 | 电子签名：创建/发送/跟踪签署合同 |

---

## 3. 代码与开发

### 代码托管与版本控制

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `github` | GitHub | 867 | 仓库管理、Issue/PR 操作、分支管理、Actions、代码搜索 |
| `bitbucket` | Bitbucket | 104 | 仓库管理、PR 审核、Issue 跟踪、分支操作 |
| `gitlab` | GitLab | — | CI/CD、仓库管理、Issue/MR 操作 |

### 项目跟踪与 Bug 管理

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `jira` | Jira | 97 | Issue 创建/更新、Sprint 管理、用户分配、看板操作 |
| `sentry` | Sentry | 208 | 错误跟踪、监控告警、Issue 分配、性能监控 |
| `linear` | Linear | 31 | Issue 创建、评论、状态变更、工作流管理 |

### 基础设施与云服务

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `supabase` | Supabase | 121 | 数据库操作、认证管理、存储管理、API 密钥管理 |
| `vercel` | Vercel | 147 | 项目/部署管理、域名配置、环境变量操作 |
| `neon` | Neon | 110 | Serverless Postgres：数据库/分支/端点管理 |
| `snowflake` | Snowflake | 15 | 执行 SQL 查询、数据仓库管理 |
| `databricks` | Databricks | 423 | 数据湖、机器学习、SQL 查询、作业管理 |
| `pagerduty` | PagerDuty | 368 | 告警管理、On-Call 排班、事件响应自动化 |

### 开发工具

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `codeinterpreter` | Code Interpreter | 5 | 创建沙盒、执行 Python 代码、运行终端命令 |
| `browserbase_tool` | Browserbase | 19 | 无头浏览器管理：运行/监控浏览器会话 |
| `postman` | Postman | 135 | API 测试集合管理、Mock 服务器 |
| `algolia` | Algolia | 134 | 搜索服务管理：索引、配置、查询 |
| `launch_darkly` | LaunchDarkly | 248 | Feature Flag 管理、AB 测试、渐进发布 |
| `crowdin` | Crowdin | 232 | 本地化翻译管理、多语言资源文件处理 |

---

## 4. 项目管理

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `asana` | Asana | 153 | 任务创建/更新、项目管理、成员分配、进度跟踪 |
| `clickup` | ClickUp | 163 | 任务管理、文档、目标、多视图（列表/看板/甘特） |
| `monday` | Monday.com | 125 | 工作看板、自动化工作流、报告生成 |
| `wrike` | Wrike | 144 | 项目计划、Gantt 图、资源管理、工作流定制 |
| `airtable` | Airtable | 25 | 数据库式表格：记录增删改查、视图管理 |
| `coda` | Coda | 110 | 文档与数据库结合：页面/表格/自动化管理 |
| `shortcut` | Shortcut | 142 | 敏捷开发 Story/Epic 管理、Sprint 规划 |
| `trello` | Trello | — | 看板式任务卡片管理 |
| `baserow` | Baserow | 14 | 开源数据库工具：表格/字段/行管理 |

---

## 5. CRM 与销售

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `hubspot` | HubSpot | 229 | 联系人/公司/交易管理、邮件营销、CRM 自动化 |
| `salesforce` | Salesforce | 225 | Account/Contact/Lead/Opportunity 完整 CRM 管理 |
| `pipedrive` | Pipedrive | 402 | 销售管道管理、Deal 跟踪、活动记录 |
| `attio` | Attio | 111 | 关系管理 CRM：联系人/公司/工作流 |
| `zoho` | Zoho CRM | 12 | Zoho CRM 记录创建、Lead 转换、标签管理 |
| `dynamics365` | Dynamics 365 | 16 | 微软 CRM：Account/Contact/Case 管理 |
| `affinity` | Affinity | 20 | 投资人关系管理：企业/人员/交易 List 管理 |
| `apollo` | Apollo.io | — | 销售线索发现、联系人数据丰富 |
| `linkedin` | LinkedIn | 22 | 发布帖子、评论、创建分享内容 |
| `freshdesk` | Freshdesk | 179 | CRM + 客服 Ticket 管理、知识库、自动化 |

---

## 6. 客户支持

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `zendesk` | Zendesk | 19 | 工单创建/更新、组织管理、知识库操作 |
| `intercom` | Intercom | 133 | 实时聊天、消息自动化、用户分段 |
| `help_scout` | Help Scout | 137 | 共享收件箱、知识库、用户对话管理 |
| `servicenow` | ServiceNow | 5 | ITSM：创建/更新/删除服务记录 |
| `gleap` | Gleap | 179 | 应用内用户反馈、Bug 报告、功能请求管理 |
| `freshservice` | Freshservice | 9 | IT 服务管理：工单、变更、资产管理 |

---

## 7. 数据库

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `neon` | Neon | 110 | Serverless Postgres 管理：库/分支/端点/查询 |
| `googlebigquery` | Google BigQuery | 63 | 云数据仓库：执行查询、管理 Dataset/Table/Job |
| `snowflake` | Snowflake | 15 | 执行 SQL 查询、检查执行状态 |
| `elasticsearch` | Elasticsearch | 4 | 全文搜索、索引管理 |
| `clickhouse` | ClickHouse | 6 | 列式数据库查询、集群管理 |
| `influxdb_cloud` | InfluxDB Cloud | 9 | 时序数据库：写入/查询时序数据 |
| `nocodb` | NocoDB | 27 | 开源 Airtable 替代：表格/记录 CRUD |

---

## 8. 数据分析与 BI

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `posthog` | PostHog | 506 | 产品分析：事件跟踪、用户行为分析、漏斗/队列 |
| `mixpanel` | Mixpanel | 50 | 事件分析、用户画像、留存分析、报告导出 |
| `amplitude` | Amplitude | 54 | 用户行为分析、Cohort 管理、A/B 测试 |
| `google_analytics` | Google Analytics | 69 | 网站流量分析、用户行为报告、转化跟踪 |
| `metabase` | Metabase | 225 | 开源 BI：创建/管理查询、仪表盘、图表 |
| `semrush` | Semrush | 37 | SEO 分析：关键词研究、竞争对手分析、排名跟踪 |
| `ahrefs` | Ahrefs | 40 | SEO：外链分析、域名权重、内容分析 |

---

## 9. AI 与搜索

### AI 模型调用

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `perplexityai` | Perplexity AI | 6 | 对话式 AI 搜索、异步任务、嵌入向量 |
| `openai` | OpenAI | 126 | 管理 Assistants/Thread/File；调用 API |
| `mistral_ai` | Mistral AI | 54 | 调用 Mistral 模型：对话、嵌入、批处理 |
| `groqcloud` | GroqCloud | 7 | 高性能推理 API，超低延迟 LLM 调用 |
| `ollama` | Ollama | 8 | 本地/云端大模型运行管理 |
| `deepseek` | DeepSeek | 4 | DeepSeek 模型 API 调用 |
| `pinecone` | Pinecone | 48 | 向量数据库：Index/Upsert/Query 操作 |
| `mem0` | Mem0 | 47 | LLM 应用记忆层：存储/检索/管理长期记忆 |
| `hugging_face` | Hugging Face | 135 | 模型推理、数据集管理、Space 管理 |

### 搜索工具

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `tavily` | Tavily | 5 | AI 优化搜索、网页抓取、内容提取 |
| `serpapi` | SerpApi | 48 | Google/Bing/百度等搜索结果 API |
| `exa` | Exa | 18 | 语义搜索、网页内容提取、研究助手 |
| `composio_search` | Composio Search | 23 | 综合搜索：旅行/电商/新闻/学术等 |
| `hackernews` | Hacker News | 16 | 获取热门文章、用户信息、最佳故事 |
| `semanticscholar` | Semantic Scholar | 21 | 学术论文搜索、作者信息查询 |
| `yousearch` | You.com | 1 | You.com 搜索引擎查询 |
| `linkup` | Linkup | 5 | 网页搜索、问答提取 |

---

## 10. 网页爬取

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `firecrawl` | Firecrawl | 30 | 批量网页爬取、结构化数据提取、站点地图 |
| `zenrows` | ZenRows | 14 | 绕过反爬机制的网页抓取 API |
| `browser_tool` | Browser Tool | 5 | AI Agent 控制浏览器：自动化网页交互 |
| `browserbase_tool` | Browserbase | 19 | 无头浏览器平台：管理/监控浏览器会话 |
| `apify` | Apify | 113 | 网页爬取与自动化：Actor 管理、任务调度 |
| `phantombuster` | PhantomBuster | 53 | 社交媒体数据提取（LinkedIn/Twitter 等） |
| `scrapegraph_ai` | ScrapeGraph AI | 27 | AI 驱动网页爬取，LLM 解析网页内容 |

---

## 11. 营销

### 邮件营销

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `mailchimp` | Mailchimp | 275 | 邮件活动管理、受众分组、自动化流程、模板 |
| `sendgrid` | SendGrid | 364 | 事务性邮件/营销邮件发送、模板/联系人管理 |
| `brevo` | Brevo | 21 | 邮件+SMS 营销：创建联系人/列表/活动 |
| `klaviyo` | Klaviyo | 225 | 电商邮件营销：用户分群、个性化自动化 |
| `instantly` | Instantly | 118 | 冷邮件自动化：活动管理、邮件序列 |

### 广告

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `metaads` | Meta Ads | 53 | Facebook/Instagram 广告：创建/管理广告系列 |
| `googleads` | Google Ads | 5 | 搜索广告：受众列表、活动查询 |

---

## 12. 电商

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `shopify` | Shopify | 432 | 商品/订单/库存/客户/支付完整管理 |
| `stripe` | Stripe | 560 | 支付/订阅/发票/退款/欺诈检测完整 API |
| `junglescout` | Jungle Scout | 6 | Amazon 商品研究、关键词分析 |
| `lemon_squeezy` | Lemon Squeezy | 32 | 数字产品销售、订阅管理、税务处理 |
| `shippo` | Shippo | 95 | 电商物流：创建标签、跟踪包裹、比价 |

---

## 13. 财务与支付

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `stripe` | Stripe | 560 | 在线支付、订阅、发票、退款、Connect 平台 |
| `quickbooks` | QuickBooks | 105 | 财务管理：发票、费用跟踪、报表生成 |
| `zoho_books` | Zoho Books | 264 | 会计、开具发票、费用追踪、银行对账 |
| `netsuite` | NetSuite | 89 | ERP：会计、CRM、电商一体化管理 |
| `coinbase` | Coinbase | 28 | 加密货币：资产详情、汇率、交易查询 |
| `finage` | Finage | 40 | 金融数据 API：股票/外汇/加密货币实时行情 |
| `ramp` | Ramp | 89 | 企业支出管理：卡片、报销、供应商支付 |
| `brex` | Brex | 85 | 初创公司企业卡：支出管理、财务工具 |

---

## 14. 图像与设计

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `figma` | Figma | 53 | 读取设计文件、评论、管理团队库、Webhook |
| `googlephotos` | Google Photos | 14 | 照片上传/下载、相册管理、内容搜索 |
| `canva` | Canva | — | 在线设计：模板创建、图片编辑 |
| `heygen` | HeyGen | 72 | AI 视频生成：创建 Avatar、生成视频 |

---

## 15. 视频与音频

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `youtube` | YouTube | 51 | 上传视频、管理播放列表、频道管理、评论 |
| `elevenlabs` | ElevenLabs | 155 | AI 语音合成：创建声音、文字转语音、克隆声音 |
| `lmnt` | LMNT | 8 | AI 语音生成、声音管理 |
| `heygen` | HeyGen | 72 | AI Avatar 视频生成、数字人创建 |
| `retellai` | Retell AI | 67 | AI 电话座席：通话录音/转录/分析 |
| `fireflies` | Fireflies | 21 | 会议录音/转录/总结/搜索 |
| `zoom` | Zoom | 73 | 会议创建、注册、网络研讨会管理 |

---

## 16. 社交媒体

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `twitter` | Twitter/X | 80 | 发推、回复、书签、列表管理、关注/粉丝 |
| `linkedin` | LinkedIn | 22 | 发帖、评论、删除内容 |
| `reddit` | Reddit | 23 | 发帖、评论、删除、编辑 Reddit 内容 |
| `discord` | Discord | 16 | 服务器/频道信息查询 |
| `discordbot` | Discord Bot | 165 | 频道管理、角色分配、消息发送完整功能 |

---

## 17. 日历与会议

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `googlecalendar` | Google Calendar | 46 | 事件创建/更新/删除、可用时间查询 |
| `googletasks` | Google Tasks | 18 | 任务列表管理、任务增删改查 |
| `googlemeet` | Google Meet | 17 | 创建会议空间、管理会议、结束会议 |
| `cal` | Cal.com | 175 | 排期/预约管理：预约链接、日历同步 |
| `zoom` | Zoom | 73 | 创建会议、注册管理、Webinar |
| `fireflies` | Fireflies | 21 | 会议转录、摘要生成、搜索 |

---

## 18. 教育

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `canvas` | Canvas LMS | 566 | 课程/作业/成绩/测验/讨论完整 LMS 管理 |
| `blackboard` | Blackboard | 314 | 在线教学平台用户分析与交互数据 |
| `google_classroom` | Google Classroom | 62 | 班级/作业/成绩/公告管理 |
| `d2lbrightspace` | D2L Brightspace | 45 | 学习管理：课程内容/评估/成绩 |

---

## 19. HR 与招聘

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `bamboohr` | BambooHR | 41 | 员工信息管理、招聘 ATS、假期申请 |
| `lever` | Lever | — | 招聘管道：候选人跟踪、面试安排 |
| `workday` | Workday | — | HR ERP：薪酬、绩效、人才管理 |

---

## 20. 其他实用工具

### 搜索 & 情报

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `google_maps` | Google Maps | 22 | 地理编码、路线规划、地点搜索、距离矩阵 |
| `weathermap` | OpenWeatherMap | 2 | 城市天气查询、天气预报 |
| `peopledatalabs` | People Data Labs | 24 | B2B 数据丰富：公司/人员/位置信息查询 |

### 问卷与表单

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `survey_monkey` | SurveyMonkey | — | 调研问卷创建、收集、分析 |
| `typeform` | Typeform | — | 交互式表单/调查创建与响应管理 |

### 活动管理

| Toolkit Slug | 名称 | 工具数 | 能做什么 |
|---|---|---|---|
| `eventbrite` | Eventbrite | — | 活动创建、票务管理、参与者管理 |

---

## 常见使用场景示例

```
# 代码审查 Agent
toolkits: github + slack + jira

# 邮件助手 Agent
toolkits: gmail + googlecalendar + googledrive

# 销售助手 Agent
toolkits: hubspot + salesforce + linkedin + gmail

# 客服 Agent
toolkits: zendesk + slack + notion + gmail

# 数据分析 Agent
toolkits: googlebigquery + googlesheets + googledrive + slack

# 内容营销 Agent
toolkits: twitter + linkedin + notion + mailchimp

# 开发运维 Agent
toolkits: github + jira + sentry + pagerduty + slack

# 招聘 Agent
toolkits: bamboohr + linkedin + calendar + gmail
```

---

## 快速查询 API

```typescript
// 列出所有 toolkit
const all = await composio.toolkits.get();

// 获取某 toolkit 下的全部工具
const tools = await composio.tools.getRawComposioTools({
  toolkits: ['github'],
  important: false,  // false = 返回全部，默认 true 只返回重要工具
});

// 搜索工具
const results = await composio.tools.getRawComposioTools({
  search: 'send email',
});

// 获取工具详情（含参数定义）
const tool = await composio.tools.getRawComposioToolBySlug('GITHUB_CREATE_ISSUE');
console.log(tool.inputParameters);
```
