# Validation and Output

## 目录

- 验证命令
- Type Check
- Lint
- Unit Test
- E2E Test
- 手动验证
- Review 输出
- 完成说明
- PR 自检

## 验证命令

修改后尽可能执行项目已有命令。先查看 `package.json` scripts，不要臆造不存在的命令。

常见命令：

```bash
pnpm typecheck
pnpm lint
pnpm test
pnpm build
```

也可能是 `npm`、`yarn`、`bun` 或 monorepo 子包命令，以项目实际为准。

无法运行时说明原因，例如依赖缺失、命令不存在、环境限制或测试耗时过长。

## Type Check

如果项目使用 TypeScript，尽可能通过类型检查。常见工具包括：

```bash
tsc
vue-tsc
```

以项目 scripts 为准。

## Lint

尽可能通过 lint。常见工具包括：

- ESLint
- Biome
- oxlint
- Stylelint

不要为了通过 lint 大范围改无关文件。

## Unit Test

核心逻辑变更时考虑单元测试。常见工具：

- Vitest
- Jest
- Testing Library

测试应覆盖真实风险，而不是只测试实现细节。

## E2E Test

关键流程变更时考虑 E2E。常见工具：

- Playwright
- Cypress

表单提交、权限、支付、登录、核心转化流程尤其需要关注。

## 手动验证

### 开发环境服务

功能验收、浏览器手动验证或 E2E 前，先确认是否已经有可用的开发环境服务：

- 如果用户提供了本地 URL、当前会话已有 dev server，或常用端口已有对应项目服务，优先复用该服务。
- 不要在已有可用服务时重复执行 `npm run dev`、`pnpm dev`、`yarn dev`、`bun dev` 等启动命令。
- 只有没有可复用服务时，才自动启动新服务；启动后记录进程、端口和 URL。
- 验收完成后，如果服务是本次自动启动的，必须停止该服务，避免长期占用端口。
- 不要停止用户原本已经启动的服务；最终说明中交代复用了已有服务，或自动启动并已停止新服务。

UI 修改至少考虑：

- 正常状态
- loading 状态
- empty 状态
- error 状态
- 移动端
- 桌面端
- 长文本和文本溢出
- 权限不足
- 接口失败

## Review 输出

用户要求 Review 时采用代码审查口径：

- 发现问题优先，摘要靠后。
- 按严重程度排序。
- 每条问题给出文件和行号。
- 聚焦 bug、回归、安全、测试缺口和可维护性风险。
- 没发现问题时明确说明，并指出剩余测试风险。

## 完成说明

完成修改后说明：

- 改了哪些文件。
- 每个文件为什么改。
- 是否复用了现有实现。
- 是否新增公共能力。
- 是否影响 SSR、SEO、Lighthouse。
- 是否验证响应式。
- 存在什么剩余风险。
- 已运行或建议运行哪些检查命令。

保持简洁，不要把内部思考完整铺开。

## PR 自检

提交前确认：

- 已识别技术栈和渲染模式。
- 已阅读相关代码和同类实现。
- 已复用现有组件、Hook / Composable、Service / API 和类型定义。
- 没有引入不必要依赖、第二套 UI 框架、第二套状态管理或第二套请求库。
- 没有无关重构、调试代码和无意义 `console.log`。
- 已处理 loading、empty、error。
- 已检查响应式、长文本、移动端交互。
- 已检查 SSR、SEO、JSON-LD、Lighthouse 影响。
- 已检查权限、XSS、敏感信息。
- 已通过可运行的 typecheck、lint、测试或构建。
