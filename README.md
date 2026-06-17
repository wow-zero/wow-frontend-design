# WOW Frontend Design Skill

这是一个面向多智能体环境的前端工程 Skill，用于在 Vue、Nuxt、React、Next.js、Angular、Svelte、Astro 等前端项目中处理页面、组件、UI、CSS、接口、状态、路由、SSR、SEO、性能、构建、测试、Review、重构和 Bug 修复任务。

本项目的重点不是提供一套新的前端架构，而是让支持 `SKILL.md` 或类似 Agent Skills 机制的 AI 编程智能体在进入任意前端项目时，优先遵循项目现有约定，复用已有实现，并以最小改动完成用户需求。

## 适用场景

- 前端页面、组件、样式和交互实现。
- 前端 Bug 修复、重构和代码审查。
- API 调用、状态管理、表单、列表、弹窗、权限、埋点等业务前端工作。
- SSR、SSG、SEO、JSON-LD、Lighthouse、Hydration 和首屏性能相关判断。
- 移动端、响应式、可访问性、国际化和文本溢出检查。
- 构建、测试、lint、typecheck 和发布前自检。

如果与 `frontend-craft`、`frontend-design` 等通用前端 Skill 重叠，本 Skill 更强调项目一致性、代码阅读、复用优先和低风险最小改动。

## 工作原则

智能体使用本 Skill 时应遵循以下优先级：

1. 先识别项目技术栈、渲染模式、目录结构和已有工程约定。
2. 先阅读相关代码和同类实现，再设计方案。
3. 优先复用项目已有组件、Hook、Composable、Service、Store、类型、工具函数和样式体系。
4. 只在当前需求确实需要时新增抽象、依赖或公共能力。
5. 修改后尽可能运行项目已有的 typecheck、lint、test、build 或局部验证命令。
6. 最终说明必须交代修改内容、关键判断、验证结果和剩余风险。

## 目录结构

```text
.
├── README.md
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── implementation-patterns.md
    ├── project-discovery.md
    ├── rendering-performance-seo.md
    ├── safety-observability.md
    ├── ui-accessibility-i18n.md
    └── validation-output.md
```

## 多智能体兼容

本 Skill 的核心入口是 `SKILL.md`，目录结构遵循常见 Agent Skills 约定，因此不限定只能用于 Codex。

| 工具 | 建议放置位置 | 说明 |
| --- | --- | --- |
| Codex | `$CODEX_HOME/skills/wow-frontend-design/` | 可保留 `agents/openai.yaml` 作为 Codex / OpenAI 侧展示元数据。 |
| Claude Code | `~/.claude/skills/wow-frontend-design/` 或项目内 `.claude/skills/wow-frontend-design/` | Claude Code 会读取 `SKILL.md`；`agents/openai.yaml` 通常可忽略。 |
| 其他支持 Agent Skills 的工具 | 对应工具的自定义 skills 目录 | 只要支持 `SKILL.md` frontmatter 和按需读取辅助文件，通常可以复用。 |

跨工具使用时需要注意：

- 以当前宿主智能体的系统指令、工具权限和沙箱规则为准。
- 不同工具的自动触发、显式调用、权限预批准和子智能体机制可能不同。
- `references/` 是通用参考资料，建议保留。
- `agents/openai.yaml` 是工具专属 UI 元数据，不影响 Skill 的核心行为。

## 文件说明

| 文件 | 作用 |
| --- | --- |
| `SKILL.md` | Skill 的主入口，包含触发描述、核心原则、工作流程和按需读取 reference 的导航。 |
| `agents/openai.yaml` | Codex / OpenAI 侧 UI 展示元数据，包括展示名称、简短描述和默认提示语；其他智能体可忽略。 |
| `references/project-discovery.md` | 技术栈、渲染模式、目录结构和代码阅读范围识别指南。 |
| `references/implementation-patterns.md` | 组件、代码组织、Vue / Nuxt、React / Next.js、TypeScript、状态和接口请求规则。 |
| `references/rendering-performance-seo.md` | SSR、Hydration、SEO、JSON-LD、Lighthouse、图片优化和渲染性能检查项。 |
| `references/ui-accessibility-i18n.md` | UI 复用、响应式、文本溢出、移动端交互、可访问性和国际化规则。 |
| `references/safety-observability.md` | XSS、权限、敏感信息、外链、表单安全、错误监控、性能监控和埋点规则。 |
| `references/validation-output.md` | 验证命令、测试策略、Review 输出、完成说明和 PR 自检规则。 |

## 维护指南

- 保持 `SKILL.md` 精简，只放核心工作流和 reference 导航。
- 详细规则优先放入 `references/`，并在 `SKILL.md` 中说明什么时候读取。
- 避免在多个文件中重复维护同一条规则；如果需要补充细节，优先扩展对应 reference。
- 如果修改了 Skill 名称、描述或面向用户的定位，同步检查 `agents/openai.yaml` 是否仍然准确。
- 不要为了单个项目的临时偏好污染通用规则；本 Skill 应服务多种前端项目。
- 新增规则时优先写成可执行的判断标准，例如“先查看 package.json scripts”，而不是抽象口号。

## 使用提示

支持 Skills 的智能体通常会通过 `SKILL.md` 的 frontmatter 判断是否启用本 Skill。用户也可以在前端工程任务中明确提到该 Skill，让智能体按这里定义的前端工程流程工作。

这个 README 主要面向维护者。真正影响智能体执行行为的是 `SKILL.md` 以及按需读取的 `references/` 文件。
