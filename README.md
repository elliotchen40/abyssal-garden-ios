# Abyssal Garden — iOS 修复版

基于 [Noniv/abyssal-garden](https://github.com/Noniv/abyssal-garden)（MIT License）的 iOS 修复构建。
原始作者：Noniv。本仓库只做移动端兼容修复，世界内容与原始版本一致。

在线试玩：<https://elliotchen40.github.io/abyssal-garden-ios/>

## 修的问题

| 上游 issue | 现象 | 本仓库的修法 |
|---|---|---|
| [#5](https://github.com/Noniv/abyssal-garden/issues/5) | iPhone 上按住手指不前进（能转视角，游不动） | `identifier` 一律转无符号比较；并新增独立的"手指是否按下"标志，推进力与摇杆转向不再依赖 identifier 符号 |
| [#16](https://github.com/Noniv/abyssal-garden/issues/16) | iOS 26.1 Safari / Chrome 整屏黑屏 | 移除 glint 管线里一个未被使用的常量 `ROWS: 7`（Safari 顶点阶段因此编译失败） |
| [#17](https://github.com/Noniv/abyssal-garden/issues/17) | iPhone 无声、锁屏后不恢复 | `AudioContext` 状态非 running 即 resume 并忽略 rejected resume；隐藏前淡出再 suspend；`navigator.audioSession.type = 'playback'` |

## 触屏操作

按住 = 前进；滑动 = 转向；第二根手指 = 加速。**没有后退手势**（推进力恒为正），后退只有键盘 S 键。

## 诊断

在网址后加 `?debug=1`，左下角会显示实时触屏读数：触点数、手指按下标志、跟踪的 identifier、当前 identifier 列表、推进力、速度、帧率、pointer 类型、maxTouchPoints、是否 standalone。若按住仍不前进，截图该面板即可定位。

## 浏览器要求

WebGPU：Chrome / Edge 113+、Safari 26+（iOS 也需 26+）。iOS 26.0 之前的 Safari 不支持 WebGPU。
