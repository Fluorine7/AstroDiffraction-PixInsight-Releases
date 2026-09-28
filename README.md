# AstroDiffraction — PixInsight 发布仓库 / Release Repository

© Fluorine Zhu 2026

## 中文

这里提供 AstroDiffraction 原生 PixInsight Process 的已签名安装包。当前版本为 **V1.5.2**（模块内部版本 `1.5.2.0001`），适用于 PixInsight 1.9.5。自 V1.3 起新增已解析坐标的在线星表辅助检测、JWST 蜂窝盖板内置光学预设，并改进内存占用和明亮尖锐星点的星芒可见性。

| 平台 | 安装包 |
| --- | --- |
| macOS 14 及以上，Apple Silicon | [下载 macOS 版](AstroDiffraction-1.5.2.0001-macos-arm64.zip) |
| Windows x64 | [下载 Windows 版](AstroDiffraction-1.5.2.0001-windows-x64.zip) |

推荐在 PixInsight 中通过更新仓库安装：

1. 打开 **Resources → Updates → Manage Repositories**。
2. 添加以下地址，保留末尾的 `/`：

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. 运行 **Resources → Updates → Check for Updates**，安装更新并重启 PixInsight。
4. 在 **Process → Convolution → AstroDiffraction** 中打开。

每个安装包包含模块二进制文件和匹配的 Fluorine7 开发者签名 `.xsgn`；仓库索引 `updates.xri` 也已签名。请将模块与签名文件一起使用。目前没有 Linux 或 Intel Mac 安装包。使用已解析坐标的星表检测需要联网。

**已知限制：**一项合成星云背景回归测试显示，与平坦背景相比，结构化背景下的外侧星芒可能被过度抑制。此现象在 V1.5.1 已存在，V1.5.2 尚未修复。

**预设：**模块自带 JWST 光学预设。用户自行保存的光学和渲染预设存于本机 PixInsight 设置；目前没有从 GitHub 下载、导入或自动发现预设文件的功能。将预设文件上传到本仓库不会使现有模块自动识别。

## English

This repository distributes signed binaries of the native AstroDiffraction PixInsight Process. The current release is **V1.5.2** (internal module version `1.5.2.0001`) for PixInsight 1.9.5. Since V1.3 it adds online catalog-assisted detection for solved images and a built-in JWST reticle optical preset, and improves peak memory use and spike visibility for bright, sharp stars.

| Platform | Package |
| --- | --- |
| macOS 14 or later, Apple Silicon | [Download for macOS](AstroDiffraction-1.5.2.0001-macos-arm64.zip) |
| Windows x64 | [Download for Windows](AstroDiffraction-1.5.2.0001-windows-x64.zip) |

The recommended installation method is the PixInsight update repository:

1. Open **Resources → Updates → Manage Repositories**.
2. Add the following URL, including the trailing `/`:

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. Run **Resources → Updates → Check for Updates**, install the update, and restart PixInsight.
4. Open **Process → Convolution → AstroDiffraction**.

Each package contains the module binary and matching Fluorine7 developer signature (`.xsgn`). The `updates.xri` index is also signed. Keep the module and signature together. Linux and Intel Mac packages are not available yet. Catalog-assisted detection of solved images requires internet access.

**Known limitation:** A synthetic structured-nebula regression test shows that outer spikes can be suppressed more strongly than on a flat background. This was already present in V1.5.1 and remains unresolved in V1.5.2.

**Presets:** The module includes a built-in JWST optics preset. User-created optics and render presets live in local PixInsight settings. The module currently has no GitHub download, import, or automatic discovery for preset files. Uploading a preset file here alone will not make the existing module recognize it.
