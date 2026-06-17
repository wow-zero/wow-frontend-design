# Implementation Patterns

## 目录

- 代码组织
- 组件开发与复用
- Vue / Nuxt 规则
- React / Next.js 规则
- TypeScript 规则
- 状态管理
- 接口请求

## 代码组织

按项目现有结构拆分职责，避免一个文件同时承担：

- 页面 UI
- 业务逻辑
- 状态管理
- 接口请求
- 数据转换
- 工具函数
- 类型定义
- 常量配置

常见职责边界：

- 页面入口：负责页面组合和数据流组织。
- 组件：负责 UI 展示和交互。
- Hook / Composable：负责复用逻辑。
- Store：负责跨组件状态。
- Service / API：负责请求接口。
- Utils：负责纯函数工具。
- Constants：负责常量配置。
- Types：负责类型定义。

出现以下情况时才考虑拆分：文件超过项目常规规模、组件职责混杂、状态逻辑复杂、接口逻辑与 UI 混杂、重复逻辑明显。拆分必须服务当前需求。

## 组件开发与复用

新增组件前按顺序检查：

1. 项目中是否已有相同组件。
2. 项目中是否已有类似业务组件。
3. 当前 UI 框架是否已有适用组件。
4. 是否可以基于已有组件轻量扩展。
5. 是否确实需要自行实现。

组件应单一职责、高内聚、低耦合、可组合、可测试、易理解。

避免：

- 深层 props drilling
- 隐式依赖
- 过多布尔参数
- 组件内部处理过多业务
- 与具体页面强绑定
- 过度通用化

项目已有 UI 框架时，优先使用框架组件、项目二次封装组件、主题变量，以及既有表单、弹窗、表格、分页封装。

## Vue / Nuxt 规则

Vue 项目优先遵循项目现有写法：

- Composition API 或 Options API 以项目主流为准。
- 优先使用已有 composables、Pinia / Vuex 模式和组件命名规则。
- 遵循 scoped style、CSS Modules、Tailwind、UnoCSS 等既有样式方案。
- SSR 场景不要直接使用 `window`、`document`、`localStorage`。
- Nuxt 项目注意 server/client 边界、`useFetch`、`useAsyncData`、plugins 和 middleware 的运行环境。

## React / Next.js 规则

React 项目优先遵循项目已有 Hooks、状态管理和 Router 方案。

Next.js 项目必须区分：

- App Router / Pages Router
- Server Component / Client Component
- Server Actions / API Routes
- 静态渲染、动态渲染和缓存策略

不要无意义扩大 client boundary。`memo`、`useMemo`、`useCallback` 只在有真实收益或避免明显回归时使用。

## TypeScript 规则

禁止滥用 `any`。优先使用已有类型、接口生成类型、公共类型、模块内类型，再新增自定义类型。

类型应：

- 表达真实业务结构。
- 避免过度宽泛。
- 避免重复定义接口响应。
- 避免前后端字段含义不一致。
- 放在项目约定位置，例如当前文件局部类型、`*.types.ts`、`types/`、`interface/`、API generated types。

确需使用 `any` 或类型断言时，说明原因并限制影响范围。

## 状态管理

新增状态前确认：

- 是否已有服务端状态。
- 是否已有缓存。
- 是否已有全局 Store。
- 是否已有页面状态。
- 是否已有 URL Query 状态。
- 是否可以通过 props、emits、context 或组合函数传递。

状态优先级：

```text
服务端状态
> URL 状态
> 全局状态
> 页面状态
> 组件状态
```

接口数据、分页、筛选、详情等优先视为服务端状态。项目使用 TanStack Query、SWR、Apollo、urql、Vue Query、Nuxt `useFetch` / `useAsyncData` 时，优先复用。

全局状态只用于用户信息、权限、主题、国际化、跨页面共享状态或深层多组件共享状态。

## 接口请求

不要在组件中散落新的请求方式。优先使用项目已有：

- services
- api
- request
- repository
- client
- server actions
- composables
- hooks

请求流程必须考虑 loading、success、empty、error。错误处理遵循项目已有 toast、message、notification、error boundary、fallback UI、统一异常拦截或日志上报方式。

列表、搜索、详情、筛选结果必须考虑空状态。根据场景考虑搜索防抖、表单防重复提交、请求取消、请求重试、分页加载、下拉刷新和无限滚动，但不要过度设计。
