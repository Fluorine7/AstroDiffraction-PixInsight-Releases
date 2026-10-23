# AstroDiffraction for PixInsight

© Fluorine Zhu 2026

## 中文

AstroDiffraction 用于为 PixInsight 图像添加衍射星芒。当前版本为 **V1.7.4**（`1.7.4.0001`），适用于 **PixInsight 1.9.5**。模块和更新索引均使用 **Fluorine7 CPD 开发者身份**签名。

**请在完成色彩平衡和 BXT 后、拉伸之前使用，图像须保持线性。**

| 平台 | 安装包 |
| --- | --- |
| macOS 14 及以上，Apple Silicon | [下载 macOS 版](AstroDiffraction-1.7.4.0001-macos-arm64.zip) |
| Windows x64 | [下载 Windows 版](AstroDiffraction-1.7.4.0001-windows-x64.zip) |

暂不提供 Linux 或 Intel Mac 安装包。

### 安装

1. 打开 **Resources → Updates → Manage Repositories**，添加以下地址，保留末尾的 `/`：

   ```text
   https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/
   ```

2. 运行 **Resources → Updates → Check for Updates**，安装后重启 PixInsight。
3. 从 **Process → Convolution → AstroDiffraction** 打开模块。

手动安装：完整解压对应平台的 ZIP，在 **Process → Modules → Install Modules** 中搜索解压包的 `bin/`。请保留模块旁的 `.xsgn` 签名文件和 `doc/tools/AstroDiffraction/` 文档目录。内置预设无需另行下载。

### 最近更新

- **V1.7.4**：在界面上增加常驻的使用时机提示。
- **V1.7.3**：修复“撤回星芒”后的历史记录；再次生成时不再累积旧的 AD 步骤。
- **V1.7.2**：提高大核和远场采样精度，加快首次计算。

旧版安装包、模块及签名保存在 [archive/](archive/)，PixInsight 更新不会下载这些归档。

### 联网与隐私

“使用已解析的坐标（需要联网）”默认启用。检测星点时，模块会通过 HTTPS 查询 CDS/VizieR 的 Bright Star、Tycho-2 和补充 Gaia DR3 星表。请求包含天区坐标、范围和星等条件等检索信息，**不上传图像、文件名或本机路径，也没有遥测或使用跟踪**。服务及代理可见来源 IP 等常规连接信息。关闭该选项后使用本地图像检测；打开界面本身不会发起查询。

星表数据仅缓存在内存中，Gaia 缓存最多保留十分钟。用户预设保存在 Windows 的 `%LOCALAPPDATA%\AstroDiffraction` 或 macOS 的 `~/Library/Application Support/AstroDiffraction`。大型 FFT 按需使用系统临时目录，完成或取消后清理。模块不启动外部程序、不自行安装其他软件，也不请求管理员权限。

使用与隐私说明、第三方声明和许可证随安装包提供，位于 `doc/tools/AstroDiffraction/`。打开其中的 `AstroDiffraction.html` 即可离线阅读。

## English

AstroDiffraction adds diffraction spikes to images in PixInsight. The current version is **V1.7.4** (`1.7.4.0001`) for **PixInsight 1.9.5**. Modules and the update index are signed with the **Fluorine7 CPD identity**.

**Use it after color balance and BXT, before stretching, while the image is still linear.**

| Platform | Package |
| --- | --- |
| macOS 14 or later, Apple Silicon | [Download for macOS](AstroDiffraction-1.7.4.0001-macos-arm64.zip) |
| Windows x64 | [Download for Windows](AstroDiffraction-1.7.4.0001-windows-x64.zip) |

Linux and Intel Mac packages are not available.

### Installation

1. Open **Resources → Updates → Manage Repositories** and add this URL, including the final `/`:

   ```text
   https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/
   ```

2. Run **Resources → Updates → Check for Updates**, install, then restart PixInsight.
3. Open **Process → Convolution → AstroDiffraction**.

For manual installation, extract the entire ZIP and search its `bin/` directory under **Process → Modules → Install Modules**. Keep the module's `.xsgn` signature file and the `doc/tools/AstroDiffraction/` directory. Built-in presets need no separate download.

### Recent updates

- **V1.7.4**: adds a permanent reminder of when to use the process.
- **V1.7.3**: fixes history handling when retracting spikes, so generating again does not accumulate old AD steps.
- **V1.7.2**: improves large-kernel and far-field sampling accuracy and speeds up the first calculation.

Older packages, modules and signatures are kept in [archive/](archive/). PixInsight's updater does not download the archive.

### Network and privacy

The solved-coordinate option is enabled by default. During star detection, the module queries the Bright Star, Tycho-2 and supplementary Gaia DR3 catalogs through CDS/VizieR over HTTPS. Requests contain field coordinates, search limits and magnitude filters. **Images, filenames and local paths are not uploaded. There is no telemetry or usage tracking.** The service and any proxy can see ordinary connection metadata, such as the source IP. Disable this option to use local image detection. Opening the interface alone does not make a query.

Catalog data stays in memory; the Gaia cache lasts up to ten minutes. User presets are stored in `%LOCALAPPDATA%\AstroDiffraction` on Windows or `~/Library/Application Support/AstroDiffraction` on macOS. Large FFTs may use the system temporary directory, with cleanup after completion or cancellation. The module launches no external programs, installs no other software and requests no elevated privileges.

User documentation, privacy information, third-party notices and licenses are included under `doc/tools/AstroDiffraction/`. Open `AstroDiffraction.html` there to read them offline.

## Acknowledgments and licenses

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors (https://pixinsight.com/).

Both packages include `THIRD-PARTY-NOTICES.txt` and complete license texts under `doc/tools/AstroDiffraction/`.
A CPD signature identifies the developer and verifies integrity; it is not Pleiades Astrophoto product approval or an endorsement.
