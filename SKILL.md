---
name: shixin
description: 将设计参考、录屏或产品想法收敛为可运行、可验证、可发布的网页或 macOS 桌面原型；适用于需要真实交互、业务计算、视觉还原和交付证据的个人产品。
metadata:
  short-description: 从设计参考到可验证产品原型
---

# Shixin

把设计师的视觉目标和实际使用场景，转成一个能运行、能检查、能交付的本地产品原型。适合 React/Vite 网页原型和 macOS/Tauri 菜单栏应用；不把一张漂亮截图当成完成证明。

## 先固定边界

- 先区分事实、推测和待确认项：参考图只证明视觉方向，录屏只证明可见行为，不能臆测未展示的产品规则。
- 先写清完成标准、平台、主要数据状态和验证方式；如果缺少关键上下文，采用最小安全假设并记录。
- 保留用户已确认的范围。个人本地工具默认不添加账号、云同步、遥测、自动启动、通知或公发布能力。
- 视觉来源只有一份：选定的参考图、录屏或设计稿作为布局、密度、层级、色彩和文案的事实来源。

## 工作路由

根据当前请求只加载相关参考文档，不要默认读取全部内容：

1. 需求和业务规则：读取 [references/product-flow.md](references/product-flow.md)。
2. 从截图、录屏或生成图实现 UI：读取 [references/visual-implementation.md](references/visual-implementation.md)。
3. 需要 macOS 菜单栏、Tauri 或原生窗口：读取 [references/macos-tauri.md](references/macos-tauri.md)。
4. 需要测试、浏览器验收、打包或 GitHub 交付：读取 [references/qa-release.md](references/qa-release.md)。

## 必须保持的工作节奏

1. 先做轻量需求拆解和风险判断，再写等价的 PRD、Tech Spec 或项目说明；复杂改动未定义验收标准前不动代码。
2. 先用固定数据完成静态视觉保真，再接入实时数据、持久化和原生桥接。
3. 业务计算放在纯函数或单一状态模型里；UI、浏览器模式和原生壳都消费同一份派生结果。
4. 修复录屏或测试暴露的问题时，先复现并定位根因，再做最小修改；不把“构建成功”当作交互或视觉验收。
5. 交付时分开报告：代码通过的证据、浏览器看到的证据、原生系统看到的证据，以及仍然受环境限制的部分。

## 可复用 Skill 的协作

在目标环境可用时按需调用，不复制它们的通用内容：

- `brainstorming`：需求不清或需要做创意方向选择时。
- `writing-plans`：多文件、架构、数据模型或发布任务开始前。
- `product-design`：需要从参考图推导页面结构、状态和交互时。
- `design-taste-frontend` 或 `frontend-design`：需要高质量、非模板化前端视觉时。
- `教程美化方案`：产出 VitePress/教程型交互说明时。
- `artifact-template-nova-fit-blue-energy`：用户明确选用 NOVA Fit Blue Energy 视觉模板时。
- `test-driven-development`：新增计算逻辑或修复可复现缺陷时。
- `systematic-debugging`：遇到构建失败、交互异常或运行时错误时。
- `browser` / `ego-browser`：需要真实浏览器交互和页面证据时。
- `github`：用户明确授权提交、推送或创建 GitHub 仓库时。

如果某个 Skill 不可用，保留同样的边界和验收要求，使用当前环境的等价能力；不要假装调用成功。

## 交付底线

- 本地应用必须有可重复的启动、测试和构建命令。
- 视觉任务必须检查文字截断、遮挡、响应式布局、主要点击区域和关键状态。
- 原生 macOS 行为必须单独验证；浏览器中的模拟托盘不能替代系统菜单栏验收。
- 任何无法验证的结论都明确标注为“未验证”或“受环境限制”，不把推测写成事实。
- 发布前只提交确认过的 Skill 文件，不携带用户项目源码、录屏、截图、环境变量、Token、登录态或个人路径。
