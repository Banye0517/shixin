---
name: shixin
description: 当用户要构建类似 PayDance 的实时工资或收入追踪器时使用：实现月薪/日薪/时薪换算、工作日、午休、通勤、实时入账、进度和预计收入，并采用科技风界面、macOS 菜单栏金额入口与 iOS 状态栏或 Live Activity 设计。
metadata:
  short-description: 科技风实时工资追踪器产品 Skill
---

# Shixin · 实时工资追踪器

`shixin` 是一个产品型 Skill，不是通用的前端开发教程。它指导实现一个功能接近 [PayDance](https://github.com/MrBaoboer/PayDance) 的本地优先实时工资追踪器：用户配置薪资和工作安排后，应用持续计算当前已经赚到的钱，并在桌面与移动端提供一眼可读的入口。

## 产品目标

让用户随时知道：今天已经赚了多少、当前工作进度、距离下班多久、今天预计收入是多少。计算结果必须由一套 canonical salary schedule 驱动，主看板、macOS 菜单栏和 iOS 快捷视图不能各算一遍。

## 先读取对应规范

- 需要实现或修改功能：读取 [references/product-spec.md](references/product-spec.md)。
- 需要设计科技风界面：读取 [references/visual-system.md](references/visual-system.md)。
- 需要 macOS 菜单栏或 iOS 状态栏/Live Activity：读取 [references/platform-surfaces.md](references/platform-surfaces.md)。
- 需要测试、打包或发布：读取 [references/qa-release.md](references/qa-release.md)。

## 不可偏离的产品边界

- 这是实时工资产品，不要把结果改写成泛化的 KPI dashboard、待办工具或抽象设计案例。
- 功能参考 PayDance 的公开产品说明，但独立实现品牌、文案、视觉和代码，不复制源码、商标或页面结构。[PayDance](https://github.com/MrBaoboer/PayDance)
- 默认本地优先：不添加账号、云同步、遥测或后端，除非用户另行要求。
- 当前桌面范围是 macOS：顶部菜单栏只显示金额，点击后打开或聚焦完整看板；不使用大悬浮窗，不显示蓝色 `¥` 图标。
- iOS 设计优先做状态栏、安全区、Widget/Live Activity 的产品界面；不要声称普通 App 可以随意替换系统状态栏。

## 核心功能

实现时至少覆盖：

1. 月薪、日薪、时薪模式及清晰的换算规则。
2. 周一到周日工作日选择、上下班时间和跨零点夜班。
3. 可选午休，并从有效计薪时长中扣除。
4. 可选通勤，分别填写上班前和下班后的分钟数，并计入有效工作时长。
5. 实时今日入账，至少显示到小数点后两位。
6. 工作进度、已工作时长、距离下班、时薪和今日预计收入。
7. 未选工作日显示休息状态，不产生当日收入。
8. 设置校验、保存、恢复默认值和本地持久化。

## 实现规则

- 先用固定数据做静态界面，再接入实时计时和持久化。
- 所有金额、进度、有效起止时间和倒计时都从同一份 salary schedule 派生。
- 表单先编辑 draft，通过校验后再替换 committed settings；非法输入不能污染已保存配置。
- 浏览器预览和原生壳共享核心计算逻辑；原生 command 在浏览器模式中安全 no-op。
- 先复现真实问题再修根因；构建成功不等于视觉、点击或系统 UI 验收成功。

## 视觉方向

使用科技风蓝色毛玻璃：深海军蓝背景、蓝色能量光、半透明面板、细边框、冷白数字、高亮进度环和清晰的数字层级。视觉服务于“实时收入可读”，不要用过度发光、装饰性粒子或复杂图表遮住金额和状态。

## 交付标准

- 核心计算有单元测试，至少覆盖工作日、午休、通勤、跨零点、休息日和边界时间。
- 浏览器中真实检查设置保存、金额变化、窄窗口、文字截断、主要点击区域和控制台错误。
- macOS 单独检查菜单栏金额、点击聚焦和退出行为；没有系统 UI 证据时明确标记未验证。
- iOS 设计区分安全区顶部栏、Widget 和 Live Activity；如果要真正实现 Live Activity，使用 ActivityKit + WidgetKit/SwiftUI，而不是模拟一条系统状态栏。
- 最终报告区分“功能已实现”“视觉已验证”“原生系统已验证”和“仍受环境限制”。

## 可协作的已有 Skill

按需使用 `brainstorming`、`product-design`、`design-taste-frontend`、`frontend-design`、`test-driven-development`、`systematic-debugging`、浏览器控制和 `github`。它们负责方法或工具，`shixin` 负责本产品的功能边界、数据规则和平台表面；不要用通用 Skill 覆盖本文件的产品约束。
