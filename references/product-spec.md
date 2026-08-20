# 实时工资追踪器产品规格

## 产品定义

这是一个本地优先的实时工资追踪器。用户输入薪资模式和工作安排，系统按当前时间计算“今天已经赚到的钱”，并显示进度、剩余工作时间和今日预计收入。

功能参考 [PayDance](https://github.com/MrBaoboer/PayDance) 的公开说明：实时金额、月薪/日薪/时薪换算、工作日、午休剔除、跨零点夜班、桌面快捷入口和本地保存。实现必须保持独立品牌和界面。

## 配置模型

```text
salaryMode: "monthly" | "daily" | "hourly"
salaryAmount: number
workdays: [1..7]                 # Monday-Sunday
workStart: "09:00"
workEnd: "17:30"
lunchEnabled: boolean
lunchStart: "12:00"
lunchEnd: "13:30"
commuteEnabled: boolean
commuteBeforeMinutes: number
commuteAfterMinutes: number
currency: "CNY"
```

保存时生成一份 canonical schedule。主看板、macOS 菜单栏、iOS 快捷视图和测试都只消费它的派生结果。

## 计算规则

派生结果至少包括：

```text
effectiveStart
effectiveEnd
paidMinutes
elapsedPaidMinutes
progress
currentEarning
projectedEarning
remainingSeconds
dayState: "working" | "before-start" | "after-end" | "rest"
```

- 月薪先按配置的月度工作日或月度计薪规则换算；日薪按当日工作日规则换算；时薪直接按有效计薪分钟计算。不要在 UI 组件里重复换算。
- 未选中的工作日返回 `rest`、零进度和零当前收入。
- 午休开启时，从有效工作区间中扣除午休重叠部分；关闭时不扣除。
- 通勤开启时，有效开始时间向前扩展 `commuteBeforeMinutes`，有效结束时间向后扩展 `commuteAfterMinutes`，并计入 `paidMinutes`。
- 跨零点时，结束时间属于次日；比较时间不能只依赖同一天的 `HH:mm` 字符串。
- 当前收入按已完成的有效计薪分钟增长，实时显示保留两位小数；处于工作区间外时根据产品文案显示未开始、已下班或今日预计。

## 主界面状态

主看板至少包含：今日入账、工作进度、已工作时长、距离下班、时薪、今日预计收入，以及可编辑的薪资和时间设置。设置提交采用 draft → validate → committed 流程。

## 平台表面

- macOS 菜单栏：只显示格式化后的金额，例如 `¥459.10`；点击打开或聚焦完整看板。
- iOS 快捷视图：显示金额、进度和剩余时间，优先考虑顶部栏、Widget 和 Live Activity 的不同尺寸，而不是把完整表单塞进状态栏。
- 桌面和移动快捷入口只负责扫读和跳转，完整编辑放在主看板/App 内。

## 非目标

当前不默认实现 Windows、账号、云同步、遥测、工资单导出、支付、通知和自动启动。用户另行提出时再扩展数据模型和权限边界。
