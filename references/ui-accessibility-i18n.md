# UI, Accessibility, I18n

## 目录

- UI 复用
- 响应式布局
- 文本溢出
- 移动端交互
- 可访问性
- 国际化

## UI 复用

涉及 UI 时先确认项目已有：

- UI 框架
- 二次封装组件
- design token
- 主题变量
- 图标体系
- 表单、弹窗、表格、分页、筛选器、上传、空状态封装

不要手写一个与项目 UI 风格不一致的组件，也不要引入第二套 UI 框架。

## 响应式布局

如项目支持响应式，每次 UI 修改都考虑：

```text
Mobile: 320px ~ 767px
Tablet: 768px ~ 1024px
Desktop: 1025px+
Large Desktop: 1440px+
Ultra Wide: 1920px+
```

重点检查：

- Header
- Footer
- Sidebar
- Navigation
- Table
- Form
- Modal
- Drawer
- Card
- Tabs
- Pagination
- Dropdown
- Tooltip
- 图片和视频
- 长文本
- 按钮组

避免无业务依据的固定宽度，例如 `width: 1200px`。优先使用 `max-width`、`min-width`、`flex`、`grid`、`clamp()`、`minmax()` 或 container query。

## 文本溢出

限定高度或宽度的布局中必须考虑文本超出场景。

默认目标：

- 不撑开布局。
- 不遮挡相邻内容。
- 不破坏响应式。
- 根据项目约定使用换行、省略号、tooltip 或展开查看。

按钮、标签、表格列、卡片标题、导航项、弹窗标题和筛选项尤其需要检查。

## 移动端交互

移动端需注意：

- 点击区域足够大。
- 弹窗不超出屏幕。
- 表格可横向滚动或重排。
- 表单输入体验正常。
- 固定底部按钮不遮挡内容。
- 键盘弹出不破坏布局。
- Hover-only 交互有触屏替代方案。

## 可访问性

优先使用语义化 HTML：

```html
<header>
<nav>
<main>
<section>
<article>
<aside>
<footer>
```

表单控件应有 `label`、`aria-label` 或 `aria-describedby`，错误提示应能关联到对应控件。

图片必须考虑 `alt`；装饰性图片可使用空 `alt`。

交互组件应按场景支持 Tab、Enter、Space、Escape 和方向键。Modal、Drawer、Dropdown、Select、Menu、Tooltip、Popover 需要注意焦点管理。

文本和背景需有足够对比度。不要只用颜色表达状态，应结合文字、图标或提示。

## 国际化

如果项目支持国际化，禁止硬编码用户可见文案。新增文案时：

- 放入正确语言文件。
- key 命名符合项目规范。
- 不重复创建相同文案。
- 保持多语言含义一致。
- 避免把变量拼接成难以翻译的句子。

如果项目没有国际化体系，则遵循项目现有文案语言和表达方式。
