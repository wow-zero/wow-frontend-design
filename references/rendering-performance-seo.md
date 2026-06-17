# Rendering, Performance, SEO

## 目录

- SSR 兼容性
- Hydration 风险
- SEO 基础项
- JSON-LD
- Lighthouse 和性能
- React / Vue 性能注意点

## SSR 兼容性

SSR、SSG、ISR 或 Hybrid 项目中，避免在服务端执行：

```js
window
document
localStorage
sessionStorage
navigator
location
```

必须使用时，放入客户端生命周期、client-only 组件或明确的运行环境判断。不要让 SSR 输出依赖客户端独有状态。

## Hydration 风险

注意服务端和客户端渲染内容不一致，常见来源包括：

- 随机数
- 当前时间
- 浏览器本地存储
- 用户客户端状态
- 客户端专属数据
- 不稳定 key
- 根据视口或设备即时改变首屏结构

需要首屏稳定时，优先使用服务端可获得的数据或延迟到客户端挂载后再渲染差异部分。

## SEO 基础项

页面需要 SEO 时检查：

- title
- description
- canonical
- robots
- sitemap
- Open Graph
- Twitter Card
- H1-H6 结构
- 图片 alt
- 内链结构
- 面包屑
- 首屏内容是否可被服务端渲染

不要用客户端渲染隐藏关键可索引内容，除非业务明确不需要搜索收录。

## JSON-LD

适用时优先使用 JSON-LD：

- WebPage
- Article
- Product
- FAQPage
- BreadcrumbList
- Organization
- LocalBusiness
- WebSite
- SearchAction

JSON-LD 必须与页面真实内容一致。禁止伪造评分、评论、库存、价格、作者、发布时间或公司信息。

## Lighthouse 和性能

SSR / SSG 页面尽可能达到：

```text
Performance >= 90
Accessibility >= 90
Best Practices >= 90
SEO >= 90
```

无法达到时，说明原因和可优化方向。

优先考虑：

- Tree Shaking
- Code Splitting
- Dynamic Import
- 减少不必要依赖
- 避免重复依赖
- 减少客户端 JS
- 避免大组件全量加载
- 首屏数据请求数量
- 缓存策略
- 组件懒加载
- 不必要的 hydration

## 图片优化

优先使用 WebP、AVIF、响应式图片、Lazy Load、合理压缩和 CDN 图片参数。

尽可能设置：

```html
width
height
alt
```

避免图片导致 CLS。

## 渲染性能

注意：

- 避免无意义重渲染。
- 避免在模板或渲染函数中执行重计算。
- 长列表使用分页或虚拟滚动。
- 避免一次性渲染大量 DOM。
- 避免频繁 layout thrashing。

React 中，`memo`、`useMemo`、`useCallback` 仅在必要时使用，注意依赖数组，避免 Context 大范围更新，Next.js 中避免不必要 client boundary。

Vue 中，合理使用 `computed`，避免模板复杂计算、不必要深层 `watch` 和过大的响应式对象；Nuxt 中注意 client-only 组件对首屏和 SEO 的影响。
