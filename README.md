# AstroDiffraction — PixInsight 发布仓库 / Release Repository

© Fluorine Zhu 2026

## 中文

这里提供 AstroDiffraction 原生 PixInsight Process 的已签名安装包，适用于 PixInsight 1.9.5。**macOS 最新版为 V1.6.3**（模块内部版本 `1.6.3.0001`）；**Windows 暂时保留 V1.6.0**，V1.6.3 待编译后发布。

### macOS V1.6.3 更新

- 取消执行时固定的 1 亿像素限制，并检查像素计数和卷积尺寸溢出。大图仍需足够的内存与 PixInsight 交换空间。
- 修复极亮星核心在 PixInsight 图像窗口中出现黑点的问题：输出统一限制在 0–1，不再显示“保留线性输出范围”选项；不会重新缩放整幅图像。
- 在左侧星表中选星后，预览自动放大到 100%、将该星居中并开启星点标记，支持鼠标和键盘选行。
- 改进未饱和星核的测光和云气背景下的局部噪声估计，减少误判饱和与星芒被背景结构压弱的情况。
- 调整编辑按钮的启用逻辑，修正星表可见状态刷新，并简化鼠标悬停说明。

| 平台 | 版本 | 安装包 |
| --- | --- | --- |
| macOS 14 及以上，Apple Silicon | V1.6.3 | [下载 macOS 版](AstroDiffraction-1.6.3.0001-macos-arm64.zip) |
| Windows x64 | V1.6.0（V1.6.3 待发布） | [下载 Windows 版](AstroDiffraction-1.6.0.0001-windows-x64.zip) |

推荐在 PixInsight 中通过更新仓库安装：

1. 打开 **Resources → Updates → Manage Repositories**。
2. 添加以下地址，保留末尾的 `/`：

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. 运行 **Resources → Updates → Check for Updates**，安装更新并重启 PixInsight。
4. 在 **Process → Convolution → AstroDiffraction** 中打开。

每个安装包包含预设包、模块二进制文件和匹配的 Fluorine7 开发者签名 `.xsgn`；仓库索引 `updates.xri` 也已签名。请将模块与签名文件一起使用。目前没有 Linux 或 Intel Mac 安装包。使用已解析坐标的星表检测需要联网。

**验证范围：**macOS V1.6.3 已通过编译、开发者签名验证，以及大图尺寸、输出范围、写回和渲染回归测试；12348×8202 图像已通过尺寸检查，尚未完成该尺寸的整图渲染基准测试。Windows V1.6.3 的编译与实机验证待执行。

**预设随包安装：**ZIP 中的 `bin/` 同时包含模块、签名及 `AstroDiffraction-presets.adpresets`。请一起解压或通过更新仓库安装，模块会按自身所在目录读取预设。现有光学预设下拉框提供“普通设置（内置）”“JWST 蜂窝盖板（内置）”和“quattro150（随包）”，选择后点击“应用”即可。内置预设不能覆盖，修改后请换一个名称保存。

用户自行保存的光学和渲染预设使用 `AstroDiffraction-user.adpresets`，存放在 Windows 的 `%LOCALAPPDATA%\AstroDiffraction` 或 macOS 的 `~/Library/Application Support/AstroDiffraction`。旧版保存在 PixInsight 设置中的预设会自动迁移。模块更新不会覆盖用户文件，保存路径会显示在 Process Console 中。迁移到另一台电脑时，可将用户预设文件复制到对应用户目录，重新打开界面后即可读取；替换前请备份目标电脑已有的同名文件。

## English

This repository distributes signed binaries of the native AstroDiffraction PixInsight Process for PixInsight 1.9.5. **The latest macOS release is V1.6.3** (internal module version `1.6.3.0001`). **Windows remains at V1.6.0** until the V1.6.3 Windows build is ready.

### macOS V1.6.3 changes

- Removes the fixed 100-million-pixel execution limit and checks pixel counts and convolution dimensions for overflow. Large images still need sufficient RAM and PixInsight swap space.
- Fixes dark dots in very bright stellar cores in PixInsight image windows. Output is limited to 0–1; the unbounded-output checkbox has been removed. No whole-image rescaling is applied.
- Selecting a star-table row centres that star at 100% preview scale and enables star markers. Mouse and keyboard selection are supported.
- Improves intact-core photometry and local noise estimation on nebula backgrounds, reducing false saturation recovery and spike suppression by background structure.
- Refines editing-control availability, visible-star status refresh and tooltips.

| Platform | Version | Package |
| --- | --- | --- |
| macOS 14 or later, Apple Silicon | V1.6.3 | [Download for macOS](AstroDiffraction-1.6.3.0001-macos-arm64.zip) |
| Windows x64 | V1.6.0 (V1.6.3 pending) | [Download for Windows](AstroDiffraction-1.6.0.0001-windows-x64.zip) |

The recommended installation method is the PixInsight update repository:

1. Open **Resources → Updates → Manage Repositories**.
2. Add the following URL, including the trailing `/`:

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. Run **Resources → Updates → Check for Updates**, install the update, and restart PixInsight.
4. Open **Process → Convolution → AstroDiffraction**.

Each package contains the preset pack, module binary, and matching Fluorine7 developer signature (`.xsgn`). The `updates.xri` index is also signed. Keep the module and signature together. Linux and Intel Mac packages are not available yet. Catalog-assisted detection of solved images requires internet access.

**Validation scope:** macOS V1.6.3 passes compilation, developer-signature verification, and geometry, output-range, writeback and rendering regression tests. The 12348×8202 geometry passes preflight; a full-frame rendering benchmark at that size has not been completed. Windows V1.6.3 compilation and hardware validation remain pending.

**Bundled presets:** Each ZIP places the module, its signature, and `AstroDiffraction-presets.adpresets` together under `bin/`. Keep them together when extracting, or install through the update repository. The module reads presets next to its own binary. The existing optics preset list offers ordinary optics, `JWST 蜂窝盖板（内置）`, and `quattro150（随包）`. Select a preset and click Apply; to save changes to a supplied preset, use a new name.

User optics and render presets are saved in `AstroDiffraction-user.adpresets` under `%LOCALAPPDATA%\AstroDiffraction` on Windows or `~/Library/Application Support/AstroDiffraction` on macOS. Legacy module-settings presets migrate automatically. Updates preserve the user file, and the Process Console reports its saved location. To move presets to another computer, copy the user file to that computer's corresponding user directory and reopen the interface. Back up an existing destination file before replacing it.
