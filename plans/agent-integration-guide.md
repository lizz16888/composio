# Composio SDK Agent 集成指南

> 本文档面向自研 Agent 开发者，介绍如何将 Composio SDK 接入自己的 Agent，实现工具查询、工具调用等功能。

---

## 目录

1. [架构说明](#1-架构说明)
2. [安装与初始化](#2-安装与初始化)
3. [用户授权（ConnectedAccounts）](#3-用户授权-connectedaccounts)
4. [查询可用工具](#4-查询可用工具)
5. [执行工具](#5-执行工具)
6. [自定义 Provider（深度集成）](#6-自定义-provider深度集成)
7. [自定义工具（Custom Tools）](#7-自定义工具-custom-tools)
8. [Modifiers（拦截器）](#8-modifiers拦截器)
9. [工具版本控制](#9-工具版本控制)
10. [错误处理](#10-错误处理)
11. [完整示例](#11-完整示例)

---

## 1. 架构说明

```
你的 Agent（本地）
       │
       │ HTTP（工具查询 / 执行参数）
       ▼
  Composio 云端（backend.composio.dev）
       │ 使用托管的用户 OAuth token / API Key
       ▼
  目标服务（GitHub / Gmail / Slack / ...）
       │
       ▼
  执行结果返回给 Agent
```

**关键点：**
- SDK 只是客户端，工具的实际执行在 Composio 云端完成
- 用户的 OAuth token / API Key 由 Composio 云端托管，不需要在 Agent 代码中管理
- 共有 **1000+ Toolkit，40,000+ 工具** 可用

---

## 2. 安装与初始化

### 安装

```bash
# 仅使用核心功能（不接入特定 AI 框架）
npm install @composio/core

# 如果接入 OpenAI
npm install @composio/core @composio/openai

# 如果接入 Anthropic
npm install @composio/core @composio/anthropic

# 如果接入 Vercel AI SDK
npm install @composio/core @composio/vercel

# LangChain
npm install @composio/core @composio/langchain
```

### 初始化

```typescript
import { Composio } from '@composio/core';

// 最简初始化（默认 Provider）
const composio = new Composio({
  apiKey: process.env.COMPOSIO_API_KEY,          // 必填
  baseURL: 'https://backend.composio.dev',        // 可选，自定义 API 地址
  allowTracking: true,                            // 可选，默认 true
  autoUploadDownloadFiles: true,                  // 可选，自动处理文件上传/下载，默认 true
});

// 指定 AI Provider（以 OpenAI 为例）
import { OpenAIProvider } from '@composio/openai';

const composio = new Composio({
  apiKey: process.env.COMPOSIO_API_KEY,
  provider: new OpenAIProvider(),
});

// 锁定工具包版本（生产环境推荐）
const composio = new Composio({
  apiKey: process.env.COMPOSIO_API_KEY,
  toolkitVersions: {
    github: '20250909_00',
    slack:  '20250902_00',
  },
});
```

### 环境变量

```bash
COMPOSIO_API_KEY=sk-xxxx           # 必填，Composio 控制台获取
COMPOSIO_BASE_URL=                 # 可选，自定义 API 地址
COMPOSIO_LOG_LEVEL=info            # 可选：silent/error/warn/info/debug
COMPOSIO_DISABLE_TELEMETRY=true    # 可选，禁用遥测

# 也可通过环境变量锁定工具包版本
COMPOSIO_TOOLKIT_VERSION_GITHUB=20250909_00
COMPOSIO_TOOLKIT_VERSION_SLACK=20250902_00
```

---

## 3. 用户授权（ConnectedAccounts）

工具执行前，用户需要先授权对应的外部服务（如 GitHub OAuth）。

### 3.1 创建认证配置

```typescript
import { AuthConfigTypes } from '@composio/core';

// 使用 Composio 托管的认证（最简单）
const authConfig = await composio.authConfigs.create('github', {
  type: AuthConfigTypes.COMPOSIO_MANAGED,
  name: 'My GitHub Auth',
});

console.log(authConfig.id); // auth_config_xxx
```

### 3.2 引导用户授权

```typescript
// 为用户生成授权链接
const connectionRequest = await composio.connectedAccounts.link(
  'user-123',         // 你系统中的用户 ID
  authConfig.id       // 上一步创建的 authConfig ID
);

console.log(connectionRequest.redirectUrl); // 引导用户打开此链接完成 OAuth 授权

// 轮询等待用户完成授权
const connectedAccount = await connectionRequest.waitForConnection();
console.log(connectedAccount.id); // connected_account_xxx
```

### 3.3 查询已连接的账户

```typescript
// 查询某用户的所有已连接账户
const accounts = await composio.connectedAccounts.list({
  userIds: ['user-123'],
});

// 查询某 toolkit 的已连接账户
const githubAccounts = await composio.connectedAccounts.list({
  toolkitSlugs: ['github'],
});
```

### 3.4 使用 connectedAccountId 执行工具

如果用户有多个同类型连接（如多个 GitHub 账号），执行工具时可指定：

```typescript
const result = await composio.tools.execute('GITHUB_CREATE_ISSUE', {
  userId: 'user-123',
  connectedAccountId: connectedAccount.id,  // 指定使用哪个连接
  arguments: { owner: 'my-org', repo: 'my-repo', title: 'Bug' },
  dangerouslySkipVersionCheck: true,
});
```

---

## 4. 查询可用工具

### 4.1 查询所有可用 Toolkit

```typescript
// 列出所有 toolkit
const toolkits = await composio.toolkits.get();

// 按分类筛选
const toolkits = await composio.toolkits.get({ category: 'productivity' });

// 获取单个 toolkit 详情
const github = await composio.toolkits.get('github');
```

### 4.2 获取工具列表（wrapped 格式，适配 AI 框架）

`composio.tools.get()` 返回经 Provider 包装后的格式，可直接传给对应 AI 框架。

```typescript
// 按 toolkit 获取（默认返回 "重要工具" 子集）
const tools = await composio.tools.get('user-123', {
  toolkits: ['github'],
});

// 获取全部工具（关闭 important 过滤）
const tools = await composio.tools.get('user-123', {
  toolkits: ['github'],
  important: false,
});

// 限制数量
const tools = await composio.tools.get('user-123', {
  toolkits: ['github'],
  limit: 10,
});

// 按工具 slug 精确获取
const tools = await composio.tools.get('user-123', {
  tools: ['GITHUB_CREATE_ISSUE', 'GITHUB_GET_REPOS'],
});

// 获取单个工具（slug 字符串形式）
const tool = await composio.tools.get('user-123', 'GITHUB_CREATE_ISSUE');

// 语义搜索
const tools = await composio.tools.get('user-123', {
  search: 'create issue',
});

// 跨多个 toolkit
const tools = await composio.tools.get('user-123', {
  toolkits: ['github', 'slack'],
});
```

### 4.3 获取工具原始 Schema（不经过 Provider 包装）

适合需要自行处理工具 schema 的场景。

```typescript
// 获取工具列表原始 schema
const rawTools = await composio.tools.getRawComposioTools({
  toolkits: ['github'],
  limit: 5,
});

// rawTools[0] 结构示例：
// {
//   slug: 'GITHUB_CREATE_ISSUE',
//   name: 'Create Issue',
//   description: 'Create a new issue in a GitHub repository',
//   inputParameters: {
//     type: 'object',
//     properties: {
//       owner: { type: 'string', description: '...' },
//       repo: { type: 'string', description: '...' },
//       title: { type: 'string', description: '...' },
//     },
//     required: ['owner', 'repo', 'title'],
//   },
//   toolkit: { slug: 'github', name: 'GitHub' },
//   version: '20250909_00',
//   tags: ['Important'],
// }

// 获取单个工具原始 schema
const rawTool = await composio.tools.getRawComposioToolBySlug('GITHUB_CREATE_ISSUE');
console.log(rawTool.inputParameters);   // 查看参数定义
console.log(rawTool.availableVersions); // 查看所有可用版本
```

---

## 5. 执行工具

### 5.1 直接执行（适合自研 Agent）

```typescript
const result = await composio.tools.execute('GITHUB_CREATE_ISSUE', {
  userId: 'user-123',                   // 使用哪个用户的授权
  arguments: {
    owner: 'my-org',
    repo: 'my-repo',
    title: 'Bug: Something is wrong',
    body: 'Details here...',
  },
  version: '20250909_00',               // 建议生产环境指定版本
  // dangerouslySkipVersionCheck: true, // 或跳过版本检查（开发用）
});

// 返回结构
// {
//   data: { ... },       // 工具执行的实际返回数据
//   error: null,         // 错误信息
//   successful: true,    // 是否成功
//   logId: 'log_xxx',    // 执行日志 ID
// }

if (result.successful) {
  console.log(result.data);
} else {
  console.error(result.error);
}
```

### 5.2 需要 Agent 决策的完整调用循环

Agent 自己解析工具调用（适合自研 LLM 推理框架）：

```typescript
import { Composio } from '@composio/core';

const composio = new Composio({ apiKey: process.env.COMPOSIO_API_KEY });

// 第一步：获取工具 schema，构造给 LLM 的 prompt
const rawTools = await composio.tools.getRawComposioTools({
  toolkits: ['github'],
});

// 构造工具描述（自行格式化给 LLM）
const toolDescriptions = rawTools.map(tool => ({
  name: tool.slug,
  description: tool.description,
  parameters: tool.inputParameters,
}));

// 第二步：调用你的 LLM（伪代码）
const llmResponse = await yourLLM.chat({
  messages: [{ role: 'user', content: '帮我在 my-org/my-repo 创建一个 issue' }],
  tools: toolDescriptions,
});

// 第三步：解析 LLM 决策，执行工具
if (llmResponse.toolCall) {
  const result = await composio.tools.execute(llmResponse.toolCall.name, {
    userId: 'user-123',
    arguments: llmResponse.toolCall.arguments,
    dangerouslySkipVersionCheck: true,
  });
  
  // 第四步：将结果反馈给 LLM 继续推理
  const finalResponse = await yourLLM.chat({
    messages: [
      { role: 'user', content: '...' },
      { role: 'assistant', toolCall: llmResponse.toolCall },
      { role: 'tool', content: JSON.stringify(result.data) },
    ],
  });
}
```

### 5.3 使用已支持的 AI Provider（自动处理调用循环）

以 OpenAI 为例（其他框架类似）：

```typescript
import { Composio } from '@composio/core';
import { OpenAIProvider } from '@composio/openai';
import OpenAI from 'openai';

const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });
const composio = new Composio({
  apiKey: process.env.COMPOSIO_API_KEY,
  provider: new OpenAIProvider(),
});

// 工具自动转换为 OpenAI function calling 格式
const tools = await composio.tools.get('user-123', { toolkits: ['github'] });

const response = await openai.chat.completions.create({
  model: 'gpt-4o',
  messages: [{ role: 'user', content: '帮我创建一个 issue' }],
  tools,           // 直接传入
  tool_choice: 'auto',
});

// 一行处理所有工具调用并返回结果
const result = await composio.provider.handleToolCalls('user-123', response);
```

---

## 6. 自定义 Provider（深度集成）

如果你的 Agent 有自己的工具调用格式，可以实现自定义 Provider：

```typescript
import { BaseNonAgenticProvider } from '@composio/core';
import type { Tool } from '@composio/core';

// 定义你需要的工具格式
interface MyToolFormat {
  tool_name: string;
  description: string;
  parameters: Record<string, unknown>;
}

class MyAgentProvider extends BaseNonAgenticProvider<MyToolFormat[], MyToolFormat> {
  readonly name = 'MyAgent';

  // 将单个 Composio Tool 转换为你的格式
  wrapTool(tool: Tool): MyToolFormat {
    return {
      tool_name: tool.slug,
      description: tool.description ?? '',
      parameters: tool.inputParameters?.properties ?? {},
    };
  }

  // 批量转换
  wrapTools(tools: Tool[]): MyToolFormat[] {
    return tools.map(t => this.wrapTool(t));
  }
}

// 使用自定义 Provider
const composio = new Composio({
  apiKey: process.env.COMPOSIO_API_KEY,
  provider: new MyAgentProvider(),
});

// tools 已经是 MyToolFormat[] 格式
const tools = await composio.tools.get('user-123', { toolkits: ['github'] });
```

---

## 7. 自定义工具（Custom Tools）

可以定义自己的工具，与 Composio 内置工具统一管理和调用：

```typescript
import { z } from 'zod';

const tool = await composio.tools.createCustomTool({
  slug: 'MY_CUSTOM_TOOL',
  name: '我的自定义工具',
  description: '这个工具做了某件事',
  toolkitSlug: 'github',             // 所属 toolkit（可选）
  inputParams: z.object({
    param1: z.string().describe('参数1的描述'),
    param2: z.number().optional().describe('可选参数2'),
  }),
  execute: async (input, connectionConfig, executeToolRequest) => {
    // 可以直接在本地执行逻辑
    const result = doSomething(input.param1);
    
    // 也可以通过 executeToolRequest 转发 HTTP 请求（会使用用户授权的凭据）
    const apiResult = await executeToolRequest({
      endpoint: `/repos/${input.param1}`,
      method: 'GET',
    });
    
    return {
      data: { result },
      error: null,
      successful: true,
    };
  },
});

// 自定义工具可以像内置工具一样调用
const result = await composio.tools.execute('MY_CUSTOM_TOOL', {
  userId: 'user-123',
  arguments: { param1: 'hello' },
  dangerouslySkipVersionCheck: true,
});
```

---

## 8. Modifiers（拦截器）

Modifiers 允许在工具 Schema 获取、执行前、执行后注入自定义逻辑。

### 8.1 modifySchema — 修改工具 Schema

```typescript
const tools = await composio.tools.get('user-123', { toolkits: ['github'] }, {
  modifySchema: ({ toolSlug, toolkitSlug, schema }) => {
    // 例如：为某个工具添加额外参数
    if (toolSlug === 'GITHUB_CREATE_ISSUE') {
      return {
        ...schema,
        inputParameters: {
          ...schema.inputParameters,
          properties: {
            ...schema.inputParameters?.properties,
            extra_label: {
              type: 'string',
              description: '自动添加的标签',
            },
          },
        },
      };
    }
    return schema;
  },
});
```

### 8.2 beforeExecute — 执行前拦截

```typescript
const result = await composio.tools.execute('GITHUB_CREATE_ISSUE', {
  userId: 'user-123',
  arguments: { owner: 'my-org', repo: 'my-repo', title: 'Test' },
  dangerouslySkipVersionCheck: true,
}, {
  beforeExecute: ({ toolSlug, toolkitSlug, params }) => {
    // 可以修改入参，添加日志等
    console.log(`[Before] Executing ${toolSlug}`);
    return params; // 必须返回 params（可修改后返回）
  },
});
```

### 8.3 afterExecute — 执行后拦截

```typescript
const result = await composio.tools.execute('GITHUB_CREATE_ISSUE', {
  userId: 'user-123',
  arguments: { ... },
  dangerouslySkipVersionCheck: true,
}, {
  afterExecute: ({ toolSlug, toolkitSlug, result }) => {
    // 可以修改返回结果，过滤字段等
    console.log(`[After] ${toolSlug} completed`);
    return result; // 必须返回 result（可修改后返回）
  },
});
```

---

## 9. 工具版本控制

Composio 的工具定期更新，生产环境建议锁定版本避免意外变更。

```typescript
// 方式一：初始化时全局指定（推荐生产环境）
const composio = new Composio({
  apiKey: process.env.COMPOSIO_API_KEY,
  toolkitVersions: {
    github: '20250909_00',
    slack:  '20250902_00',
  },
});

// 方式二：执行时指定具体版本
await composio.tools.execute('GITHUB_CREATE_ISSUE', {
  userId: 'user-123',
  version: '20250909_00',
  arguments: { ... },
});

// 方式三：环境变量（与方式一等效）
// COMPOSIO_TOOLKIT_VERSION_GITHUB=20250909_00

// 方式四：开发调试时跳过检查（不推荐生产使用）
await composio.tools.execute('GITHUB_CREATE_ISSUE', {
  userId: 'user-123',
  dangerouslySkipVersionCheck: true,
  arguments: { ... },
});

// 查看某工具的可用版本
const tool = await composio.tools.getRawComposioToolBySlug('GITHUB_CREATE_ISSUE');
console.log(tool.availableVersions); // ['20250909_00', '20250902_00', ...]
```

---

## 10. 错误处理

```typescript
import {
  ComposioToolNotFoundError,
  ComposioToolExecutionError,
  ComposioToolVersionRequiredError,
  ComposioConnectedAccountNotFoundError,
} from '@composio/core';

try {
  const result = await composio.tools.execute('GITHUB_CREATE_ISSUE', {
    userId: 'user-123',
    version: '20250909_00',
    arguments: { owner: 'my-org', repo: 'my-repo', title: 'Test' },
  });

  if (!result.successful) {
    // 工具执行失败（业务层面的错误，比如 API 返回错误）
    console.error('Tool execution failed:', result.error);
  }
} catch (error) {
  if (error instanceof ComposioToolNotFoundError) {
    // 工具 slug 不存在
  } else if (error instanceof ComposioToolVersionRequiredError) {
    // 版本为 latest，需要指定版本或设置 dangerouslySkipVersionCheck
  } else if (error instanceof ComposioConnectedAccountNotFoundError) {
    // 用户未连接该 toolkit，引导用户授权
  } else if (error instanceof ComposioToolExecutionError) {
    // 工具执行异常
  }
}
```

---

## 11. 完整示例

以下是一个完整的自研 Agent 集成示例：

```typescript
import { Composio } from '@composio/core';
import 'dotenv/config';

// 初始化
const composio = new Composio({
  apiKey: process.env.COMPOSIO_API_KEY,
  toolkitVersions: {
    github: '20250909_00',
  },
});

const userId = 'user-123';

async function setupUserConnection() {
  // 检查用户是否已连接 GitHub
  const accounts = await composio.connectedAccounts.list({
    userIds: [userId],
    toolkitSlugs: ['github'],
  });

  if (accounts.items.length === 0) {
    // 引导用户授权
    const authConfig = await composio.authConfigs.create('github', {
      type: 'COMPOSIO_MANAGED',
      name: 'GitHub Auth',
    });
    const request = await composio.connectedAccounts.link(userId, authConfig.id);
    console.log('请访问以下链接完成授权:', request.redirectUrl);
    await request.waitForConnection();
    console.log('授权完成！');
  }
}

async function runAgent(userMessage: string) {
  // 获取工具 schema
  const rawTools = await composio.tools.getRawComposioTools({
    toolkits: ['github'],
    limit: 20,
  });

  // 构造工具描述（传给你的 LLM）
  const toolDescriptions = rawTools.map(tool => ({
    name: tool.slug,
    description: tool.description,
    inputSchema: tool.inputParameters,
  }));

  // === 调用你的 LLM（此处为伪代码）===
  const llmDecision = await yourLLM.reason(userMessage, toolDescriptions);
  // llmDecision = { toolName: 'GITHUB_CREATE_ISSUE', args: { owner: ..., ... } }

  if (!llmDecision.toolName) {
    return llmDecision.text; // 不需要调用工具，直接返回文本
  }

  // 执行工具
  const result = await composio.tools.execute(llmDecision.toolName, {
    userId,
    arguments: llmDecision.args,
  }, {
    beforeExecute: ({ toolSlug, params }) => {
      console.log(`[LOG] 执行工具: ${toolSlug}`, params.arguments);
      return params;
    },
    afterExecute: ({ toolSlug, result }) => {
      console.log(`[LOG] 工具完成: ${toolSlug}`, result.successful);
      return result;
    },
  });

  if (!result.successful) {
    throw new Error(`工具执行失败: ${result.error}`);
  }

  // 将结果反馈给 LLM 生成最终回答（伪代码）
  return await yourLLM.summarize(userMessage, llmDecision.toolName, result.data);
}

// 运行
await setupUserConnection();
const answer = await runAgent('帮我在 my-org/my-repo 创建一个 issue，标题是"测试"');
console.log(answer);
```

---

## 附：常用 Toolkit 清单

| Toolkit Slug | 名称 | 工具数 |
|---|---|---|
| `github` | GitHub | 867 |
| `outlook` | Outlook | 301 |
| `hubspot` | HubSpot | 229 |
| `slack` | Slack | 151 |
| `supabase` | Supabase | 121 |
| `bitbucket` | Bitbucket | 104 |
| `jira` | Jira | 97 |
| `googledrive` | Google Drive | 89 |
| `slackbot` | Slackbot | 87 |
| `twitter` | Twitter | 80 |
| `gmail` | Gmail | 60 |
| `figma` | Figma | 53 |
| `youtube` | YouTube | 51 |
| `notion` | Notion | 47 |
| `googlecalendar` | Google Calendar | 46 |
| `googlesheets` | Google Sheets | 46 |
| `googledocs` | Google Docs | 35 |
| `linear` | Linear | 31 |
| `firecrawl` | Firecrawl | 30 |
| `discord` | Discord | 16 |
| `tavily` | Tavily | 5 |
| `perplexityai` | Perplexity AI | 6 |

完整列表通过 API 查询：
```typescript
const toolkits = await composio.toolkits.get();
```
