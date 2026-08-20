# macOS 与 iOS 平台表面

## macOS 菜单栏

当前桌面端只支持 macOS，建议使用 Tauri 2 + Rust 原生菜单栏能力：

- 只有一个完整 `main` 看板窗口和一个菜单栏 item。
- 菜单栏标题只显示实时金额，例如 `¥459.10`。
- 左键点击打开或聚焦主看板；菜单项提供“打开完整看板”和“退出”。
- 不保留大悬浮窗、`mini` window、蓝色 `¥` 图标或透明图标资源。
- 菜单栏金额与 React 主看板读取同一份派生收入值。
- 浏览器预览缺少 Tauri runtime 时，调用原生 command 必须安全 no-op。

## iOS 状态栏的正确拆分

“iOS 状态栏”要先区分三种东西：

1. App 内顶部栏：可以自定义科技风玻璃样式，但必须尊重 Safe Area。
2. Widget：用 WidgetKit 提供桌面快捷查看，可显示金额、进度和剩余时间。
3. Live Activity：用 ActivityKit 管理生命周期，用 WidgetKit + SwiftUI 设计锁屏和 Dynamic Island 的布局；它不是任意 App 页面里的系统状态栏替换。

如果用户只要设计稿或网页演示，先实现 App 内顶部栏、Dynamic Island/锁屏信息卡的静态状态。只有用户明确要 iOS 原生运行时，才增加 SwiftUI Widget Extension、ActivityKit 状态模型、启动/更新/结束和深链跳转。

## 共享数据边界

- web/macOS/iOS 都使用相同的 salary schedule 字段和计算语义。
- 平台 UI 只负责展示派生状态，不在 Widget、菜单栏或页面里复制收入算法。
- iOS Live Activity 的状态只传递必要的小型快照；不要把完整设置表单或敏感数据放进快捷表面。

## 验证边界

- macOS 必须在真实系统 UI 中检查标题完整、点击聚焦和退出行为。
- iOS 设计预览只能证明布局和层级；不能证明 ActivityKit 生命周期、系统刷新频率或 Dynamic Island 真机表现。
- 未安装 Xcode、没有 iOS Simulator 或没有 Accessibility 权限时，分别报告对应的未验证项。
