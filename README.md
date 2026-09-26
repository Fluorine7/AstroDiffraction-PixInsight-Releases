# AstroDiffraction — PixInsight 发布仓库 / Release Repository

© Fluorine Zhu 2026

## 中文

这里提供 AstroDiffraction 原生 PixInsight Process 的已签名安装包。当前版本为 V1.3（模块内部版本 `1.3.0.0018`），适用于 PixInsight 1.9.5。V1.3 改进了手动添加星点的亮度测量与极亮星的检测和渲染，并保持加宽星芒的核心清晰。

| 平台 | 安装包 |
| --- | --- |
| macOS 14 及以上，Apple Silicon | [下载 macOS 版](AstroDiffraction-1.3.0.0018-macos-arm64.zip) |
| Windows x64 | [下载 Windows 版](AstroDiffraction-1.3.0.0018-windows-x64.zip) |

推荐在 PixInsight 中通过更新仓库安装：

1. 打开 **Resources → Updates → Manage Repositories**。
2. 添加以下地址，保留末尾的 `/`：

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. 运行 **Resources → Updates → Check for Updates**，安装更新并重启 PixInsight。
4. 在 **Process → Convolution → AstroDiffraction** 中打开。

每个安装包都包含模块二进制文件和与其匹配的 Fluorine7 开发者签名 `.xsgn`；仓库索引 `updates.xri` 也已签名。请勿将模块与签名文件分开使用。目前没有 Linux 或 Intel Mac 安装包。

## English

This repository distributes signed binaries of the native AstroDiffraction PixInsight Process. The current release is V1.3 (internal module version `1.3.0.0018`) for PixInsight 1.9.5. V1.3 improves brightness measurement for manually added stars, detection and rendering of very bright stars, and core sharpness when spikes are broadened.

| Platform | Package |
| --- | --- |
| macOS 14 or later, Apple Silicon | [Download for macOS](AstroDiffraction-1.3.0.0018-macos-arm64.zip) |
| Windows x64 | [Download for Windows](AstroDiffraction-1.3.0.0018-windows-x64.zip) |

The recommended installation method is the PixInsight update repository:

1. Open **Resources → Updates → Manage Repositories**.
2. Add the following URL, including the trailing `/`:

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. Run **Resources → Updates → Check for Updates**, install the update, and restart PixInsight.
4. Open **Process → Convolution → AstroDiffraction**.

Each package contains the module binary and its matching Fluorine7 developer signature (`.xsgn`). The `updates.xri` repository index is also signed. Keep each module and signature together. Linux and Intel Mac packages are not available yet.
