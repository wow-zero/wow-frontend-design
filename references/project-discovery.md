# Project Discovery

## 目录

- 启动检查
- 技术栈识别
- 渲染模式识别
- 目录和架构识别
- 代码阅读范围
- 架构决策优先级

## 启动检查

开始分析、设计或编码前，先识别项目实际情况。优先查看：

```text
package.json
pnpm-workspace.yaml
yarn.lock
package-lock.json
turbo.json
nx.json
tsconfig.json
vite.config.*
webpack.config.*
rollup.config.*
rspack.config.*
eslint.config.*
tailwind.config.*
postcss.config.*
nuxt.config.*
next.config.*
astro.config.*
svelte.config.*
```

不要默认使用 React、Vue 或某个个人熟悉的目录结构。

## 技术栈识别

确认项目是否属于以下类型，或是否为混合架构：

- Vue / Nuxt
- React / Next.js / Remix
- Angular
- Svelte / SvelteKit
- Astro
- Electron / Tauri
- 小程序
- 微前端
- 其他框架

同时识别：

- 状态管理：Pinia、Vuex、Redux、Zustand、MobX、Recoil、Jotai、Context、RxJS 或内置方案。
- 请求方案：axios、fetch 封装、ky、ofetch、GraphQL Client、tRPC、service、repository、server actions。
- UI 框架：Element Plus、Ant Design、Arco、Naive UI、Vuetify、MUI、Chakra、Radix、Headless UI、自研组件库。
- 样式方案：CSS、SCSS、Less、Tailwind、UnoCSS、CSS Modules、CSS-in-JS、scoped style、design token。
- 国际化：vue-i18n、react-i18next、next-intl、nuxt-i18n 或自研 i18n。
- 权限：路由、页面、按钮、菜单、接口、角色、feature flag。

已有方案必须复用，禁止并行引入第二套。

## 渲染模式识别

判断当前模块属于：

- SSR
- CSR
- SSG
- ISR
- Hybrid Rendering

分析是否影响：

- SEO 和首屏可索引内容
- Hydration 一致性
- 服务端运行兼容性
- 首屏性能和缓存策略
- 浏览器 API 使用边界

## 目录和架构识别

根据项目实际目录判断，不强行套模板。

常见 Vue 项目：

```text
views/
components/
composables/
stores/
router/
services/
utils/
```

常见 Nuxt 项目：

```text
pages/
components/
composables/
layouts/
middleware/
plugins/
server/
```

常见 React 项目：

```text
pages/
components/
hooks/
services/
stores/
utils/
```

常见 Next.js App Router：

```text
app/
components/
lib/
hooks/
actions/
```

常见 Angular 项目：

```text
modules/
components/
services/
guards/
pipes/
directives/
```

## 代码阅读范围

根据任务范围，尽可能阅读：

- 当前要修改的文件
- 父级页面、布局或入口
- 关联组件
- 关联 Hook / Composable
- 关联 Store
- 关联 Service / API
- 关联类型定义
- 同类型页面、组件、表单、弹窗、列表、详情页
- 相似权限判断、埋点事件和请求流程

新增能力前先查找相似实现，优先复用或轻量扩展。

## 架构决策优先级

所有设计决策遵循：

```text
项目现有架构
> 项目现有技术栈
> 框架最佳实践
> 通用最佳实践
> 个人偏好
> AI 个人习惯
```
