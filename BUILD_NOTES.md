# Pikafish 构建与发布说明

本仓库主要收录 Pikafish 在各平台的预编译二进制文件，旨在方便用户快速部署，无需自行配置复杂的编译环境。

## 构建流程概述

本次发布包含两个阶段的云编译产物，均在 GitHub Actions 环境中完成：

### 第一阶段：全平台基础构建

我们执行了标准的多平台编译工作流，生成了以下通用架构版本：

1. **Windows**: `Pikafish-Windows-x86-64-universal.exe`
2. **Linux**: `Pikafish-Linux-x86-64-universal`
3. **macOS**: `Pikafish-MacOS-universal`
4. **Android (Legacy)**: `Pikafish-Android-arm64v8a-8byte-legacy-Android13Only`

此阶段启用了 `OPTIMIZE=yes` 以确保各平台获得最佳性能表现。

### 第二阶段：Android 平台专项适配

鉴于 Android 系统底层的持续演进，我们针对 Android 平台进行了二次精细化构建。
此次构建在沿用标准优化参数的基础上，调整了链接器配置以适应最新的系统要求，生成了新版 Android 引擎：

* **Android (Current)**: `Pikafish-Android-arm64v8a-64kb-aligned`

---

## Android 版本兼容性对照表

为了帮助 Android 用户选择正确的版本，请参考下表：

| 文件名                                                    | 适用系统版本                        | 构建特性            | 推荐度           |
|:------------------------------------------------------ |:----------------------------- |:--------------- |:------------- |
| **`Pikafish-Android-arm64v8a-64kb-aligned`**           | **Android 10 ~ Latest (14+)** | 64KB 页面对齐，兼容新内核 | ⭐⭐⭐⭐⭐ (新设备必选) |
| `Pikafish-Android-arm64v8a-8byte-legacy-Android13Only` | Android 13 及更低版本              | 传统 8-byte 对齐    | ⭐⭐⭐ (旧设备备用)   |

> **技术注释**：较新的 Android 内核（对应 Android 14+）对 ELF 加载机制进行了调整。新版引擎通过调整 `max-page-size` 参数确保了在华为及其他新款设备上的稳定运行。

---

## NNUE 权重文件

`pikafish.nnue` 为本引擎配套的神经网络权重文件。

* 引擎通常已内置对应版本的权重。
* 若未来官方发布了更新的 `.nnue` 文件，可直接下载并放置于引擎同级目录以手动更新。

---

*遵循 Pikafish 项目 GPLv3 协议分发。*
