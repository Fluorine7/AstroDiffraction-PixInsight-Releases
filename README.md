# AstroDiffraction — PixInsight 发布仓库 / Release Repository

© Fluorine Zhu 2026

## 中文

这里提供 AstroDiffraction 原生 PixInsight Process 的已签名安装包，适用于 PixInsight 1.9.5。**macOS 最新版为 V1.6.4**（模块内部版本 `1.6.4.0001`）；**Windows 暂时保留 V1.6.0**，V1.6.4 待编译后发布。

### macOS V1.6.4 更新

- 修复打开工作台时，已从 FILTER 识别出的 Ha、SII、OIII、Hb 中心波长被默认参数覆盖回 550 nm 的问题。保留手动修改和已保存的非默认波长，FWHM 仍按实际滤镜带宽填写。
- 将普通设置、JWST 蜂窝盖板和 quattro150 预设内嵌模块，升级后无需旁置预设资源。
- 补充联网、隐私与文件保存说明，以及 PCL 致谢和第三方许可文本。
- 加强 HTTPS 和星表响应校验，拒绝错误页、异常数值及截断响应；正式构建关闭开发诊断文件读写入口。
- 包含 V1.6.3 的大图执行限制修复、极亮星核心黑点修复和星表选星后 100% 居中等改进。

| 平台 | 版本 | 安装包 |
| --- | --- | --- |
| macOS 14 及以上，Apple Silicon | V1.6.4 | [下载 macOS 版](AstroDiffraction-1.6.4.0001-macos-arm64.zip) |
| Windows x64 | V1.6.0（V1.6.4 待发布） | [下载 Windows 版](AstroDiffraction-1.6.0.0001-windows-x64.zip) |

### 安装

推荐在 PixInsight 中通过更新仓库安装：

1. 打开 **Resources → Updates → Manage Repositories**。
2. 添加以下地址，保留末尾的 `/`：

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. 运行 **Resources → Updates → Check for Updates**，安装更新并重启 PixInsight。
4. 在 **Process → Convolution → AstroDiffraction** 中打开。

macOS V1.6.4 的 ZIP 将模块和匹配的 Fluorine7 开发者签名 `.xsgn` 放在 `bin/`，用户说明与许可放在 `doc/tools/AstroDiffraction/`。手动安装请遵循 PixInsight 的标准模块安装流程，并保留这些文档。`updates.xri` 仓库索引也已签名。目前没有 Linux 或 Intel Mac 安装包。

Windows V1.6.0 的 ZIP 仍包含旁置的 `AstroDiffraction-presets.adpresets`，请将它与模块、签名一起保留。

### 联网、隐私与本地数据（macOS V1.6.4）

“使用已解析的坐标（需要联网）”默认勾选。执行检测，或在尚未检测时生成星芒，会按需通过 HTTPS 向 `vizier.cds.unistra.fr` 的 CDS/VizieR 服务查询 Bright Star、Tycho-2 及补充 Gaia DR3 星表；打开界面本身不查询。请求包含天区中心坐标、搜索半径、字段、返回数量上限和星等条件。天区坐标可能反映拍摄对象。**不上传图像像素、文件名、本机路径、账号或设备序列号，也没有开发者遥测或使用跟踪。**取消勾选后使用本地图像检测。

下载的星表文本仅在内存中处理，不保存到磁盘；补充 Gaia 结果在同一天区最多复用十分钟。服务及用户配置的代理会看到来源 IP 等常规连接信息，服务日志由 CDS 自行管理。连接验证服务器证书和主机名；响应有大小、星表身份、列顺序、单位、数值和结束标记等检查。详见安装包内的 `doc/tools/AstroDiffraction/AstroDiffraction.html`。

用户自己的光学和渲染预设使用 `AstroDiffraction-user.adpresets`，存放在 Windows 的 `%LOCALAPPDATA%\AstroDiffraction` 或 macOS 的 `~/Library/Application Support/AstroDiffraction`。保存时在同一目录写入临时文件，再替换自己的预设文件。旧版 PCL Settings 预设可迁移，模块更新不覆盖用户文件。光谱数据库只读访问；图像结果通过 PixInsight 的保存功能写入文件。模块不启动外部程序，不请求管理员权限。

**验证范围：**V1.6.4 已通过 macOS 编译及开发者签名验证。15 项相关回归测试覆盖波长初始化、星表校验、预设、打包、诊断隔离、大图尺寸和输出写回；诊断开关未改变测试图像的渲染像素。另使用三种真实 VizieR 响应验证格式兼容性。这些测试不替代完整的 PI 界面实测；Windows V1.6.4 编译和实机验证待执行。

## English

This repository distributes signed binaries of the native AstroDiffraction PixInsight Process for PixInsight 1.9.5. **The latest macOS release is V1.6.4** (internal version `1.6.4.0001`). **Windows remains at V1.6.0** until its V1.6.4 build is ready.

### macOS V1.6.4 changes

- Fixes default process import resetting an inferred Ha/SII/OIII/Hb wavelength to 550 nm when opening the workbench. Manual edits and saved nondefault wavelengths are preserved; enter the actual filter FWHM yourself.
- Embeds supplied ordinary, JWST reticle and quattro150 presets in the module.
- Includes network/privacy documentation, PCL acknowledgments and third-party licenses.
- Strengthens authenticated HTTPS and catalog-response checks. Production builds disable development diagnostic file I/O.
- Includes V1.6.3's large-image execution fix, bright-core display fix and 100% preview centring on star-table selection.

| Platform | Version | Package |
| --- | --- | --- |
| macOS 14 or later, Apple Silicon | V1.6.4 | [Download for macOS](AstroDiffraction-1.6.4.0001-macos-arm64.zip) |
| Windows x64 | V1.6.0 (V1.6.4 pending) | [Download for Windows](AstroDiffraction-1.6.0.0001-windows-x64.zip) |

### Installation

1. Open **Resources → Updates → Manage Repositories**.
2. Add the following URL, including the trailing `/`:

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. Run **Resources → Updates → Check for Updates**, install the update, and restart PixInsight.
4. Open **Process → Convolution → AstroDiffraction**.

The macOS V1.6.4 ZIP places the module and matching Fluorine7 developer signature (`.xsgn`) under `bin/`, and user documentation and licenses under `doc/tools/AstroDiffraction/`. Follow PixInsight's standard module installation procedure for manual installation. Keep the documentation and module signature. The `updates.xri` index is also signed. Linux and Intel Mac packages are not available.

The Windows V1.6.0 package still uses an adjacent `AstroDiffraction-presets.adpresets`; keep it with its module and signature.

### Network, privacy and storage (macOS V1.6.4)

The solved-coordinate option is enabled by default. Detection, or generation that needs detection, queries CDS/VizieR at `https://vizier.cds.unistra.fr/viz-bin/asu-tsv` for Bright Star, Tycho-2 and supplementary Gaia DR3. Opening the interface does not query catalogs. Requests contain the solved field centre, radius, requested fields, row limit and magnitude filters. A field position can reveal the photographed target. **Image pixels, filenames, local paths, account data and device serial numbers are not uploaded. There is no developer telemetry or usage tracking.** Disable the option for local image detection.

Catalog text stays in memory; supplementary Gaia results may be reused for up to ten minutes. The service and any user-configured proxy see ordinary connection information such as the source IP; CDS controls its own service logs. Server certificates and hostnames are verified. Response size, catalog identity, column order, units, numeric ranges and complete table framing are checked. See the installed `doc/tools/AstroDiffraction/AstroDiffraction.html` for details.

User presets and same-directory temporary files use `%LOCALAPPDATA%\AstroDiffraction` on Windows or `~/Library/Application Support/AstroDiffraction` on macOS. The file is `AstroDiffraction-user.adpresets`. Legacy PCL Settings presets migrate without replacing existing file entries. Updates preserve user presets. Spectral databases are read only; image results are saved with PixInsight's Save command. The module launches no external programs and requests no elevated privileges.

**Validation scope:** macOS V1.6.4 passes compilation and developer-signature verification. Fifteen targeted regressions cover wavelength initialization, catalog validation, presets, packaging, diagnostic isolation, large-image geometry and output writeback. Diagnostic isolation preserves the rendered pixels of the test image. Three real VizieR responses pass format validation. Full PI GUI testing and Windows V1.6.4 hardware validation are not claimed.

## Acknowledgments and licenses

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors (https://pixinsight.com/).

The macOS package includes complete license texts and `THIRD-PARTY-NOTICES.txt` under `doc/tools/AstroDiffraction/`. A CPD signature identifies the developer and verifies integrity; it is not Pleiades Astrophoto product approval or an endorsement.
