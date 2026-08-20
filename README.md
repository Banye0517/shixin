# shixin

一个面向设计师与初级开发者的 Codex Skill：把参考图、录屏或产品想法收敛成可运行、可验证、可发布的网页或 macOS 桌面原型。

## 它解决什么

`shixin` 把一次真实的 PayDance 产品挑战整理成可复用工作流：

- 先拆解需求、平台和验收标准，再开始实现。
- 从视觉参考构建静态保真页面，再接入业务逻辑和持久化。
- 用单一业务模型处理工作日、午休、通勤、实时金额等派生状态。
- 将 React/Vite 页面与 macOS/Tauri 菜单栏壳分开验证。
- 用测试、浏览器交互、原生打包和证据化 QA 支撑交付。

它整合了 `brainstorming`、`writing-plans`、`product-design`、`design-taste-frontend`、`frontend-design`、`test-driven-development`、`systematic-debugging`、浏览器验收和 `github` 发布能力的协作边界；不复制这些 Skill 的通用说明，也不要求它们全部存在。

## 使用

在 Codex 中显式调用：

```text
使用 $shixin 把这个参考图做成一个可运行的 React/Vite 原型，并验证主要交互。
```

macOS 菜单栏场景：

```text
使用 $shixin，把这个实时数据看板做成只支持 macOS 的菜单栏应用，菜单栏只显示数字，点击后打开完整设置界面。
```

## 目录

```text
shixin/
├── SKILL.md
├── agents/openai.yaml
├── references/
│   ├── product-flow.md
│   ├── visual-implementation.md
│   ├── macos-tauri.md
│   └── qa-release.md
└── README.md
```

## 范围与限制

- 默认优先本地、个人使用和最小可维护实现。
- 不默认增加账号、云同步、遥测、通知、自动启动或跨平台支持。
- 视觉截图和构建结果不能替代真实浏览器或 macOS 系统 UI 验收。
- Skill 本身不携带任何项目源码、截图、录屏、凭据或登录态。

## 安装

将本目录复制到当前 Codex 的 Skills 目录，例如：

```text
<CODEX_HOME>/skills/shixin
```

安装后可使用 `$shixin` 显式调用。具体目录以当前 Codex 环境的 Skills 配置为准。
