# AstroDiffraction — PixInsight 发布仓库 / Release Repository

© Fluorine Zhu 2026

## 中文

这里提供 AstroDiffraction 原生 PixInsight Process 的安装包，适用于 PixInsight 1.9.5。
**macOS 与 Windows 最新版均为 V1.7.4，模块内部版本 `1.7.4.0001`。**
模块及更新索引使用 **Fluorine7 CPD 开发者身份**签名。

**Windows V1.7.4：** 已在 Windows 构建机编译，拉回 Mac 后单独使用 Fluorine7 签名并验签。旧 Windows V1.7.3 安装包、原 DLL 和匹配签名已按版本归档。

旧版模块、匹配签名及原安装包保存在 [archive/](archive/)。更新索引只引用当前版本，PixInsight 更新不会下载归档；完整 Git 克隆仍包含它们。

| 平台 | 安装包 |
| --- | --- |
| macOS 14 及以上，Apple Silicon | [下载 macOS 版](AstroDiffraction-1.7.4.0001-macos-arm64.zip) |
| Windows x64 | [下载 Windows 版](AstroDiffraction-1.7.4.0001-windows-x64.zip) |

### V1.7.4 — macOS 与 Windows

顶部操作栏下方新增带边框的常驻提示，关键条件加粗，并支持自动换行；切换参数页或滚动参数时仍然可见：

> **使用时机：** 完成**色彩平衡和 BXT** 后，在**拉伸之前**、图像仍为**线性状态**时使用本程序。

本次仅增加界面提示并更新版本和文档，处理算法与历史行为保持 V1.7.3 的实现。

### 沿用 V1.7.3 的历史修复

- 修复“撤回星芒”只还原像素、却保留已应用 AD 历史的问题；现在同时恢复 PixInsight 的历史位置。
- 撤回后仍可通过 PI“重做”恢复结果；再次生成会替换旧分支，已应用历史中只保留新的 AD 步骤，之前的其他处理不受影响。
- 生成后若又修改了图像或历史，要求按顺序使用 PI 撤销，避免撤掉其他处理。
- 避免反复调整时累积旧 AD 历史和暂存数据；首次计算的峰值内存没有因此下降。

### 沿用 V1.7.2 的采样与速度改进

- 修复大核与远场的采样精度：所有物理远场层采用 2 倍强度采样、Lanczos-16 像元积分，并提前衔接标准场与远场，改善远端星芒轮廓及能量分布。
- 用最多八个、受硬件和任务规模限制的工作线程加速首次光学计算，保持修正后的采样精度、双精度运算和计算范围。
- 此前 Mac 配对原生基准中，大核首次构建耗时减少约 36%，扩展远场探针首次渲染减少约 23%。基线是已修复精度的版本；这些数据不是相对 V1.7.1 的对比，也不代表 Windows、所有机器或完整 PI 工作流的速度。
- 修复星表下载取消后继续请求的问题，加入请求时限，并加固测光数值边界。
- 大型 FFT 继续使用系统临时目录控制内存。32768 入瞳网格采用 2 倍采样时，频谱暂存约需 16.1 GiB；若强度也写入磁盘则约需 24.1 GiB，另预留 512 MiB。
- 保留此前的 SDK 安全回补、预设 I/O 加固及完整中英用户文档和第三方许可。

Windows 现已补齐 V1.7.4 的常驻提示；本次 macOS 安装包保持原字节和签名。两个平台的旧 V1.7.3 包、模块及匹配签名均已归档。

### 安装

1. 在 PixInsight 打开 **Resources → Updates → Manage Repositories**。
2. 添加以下地址，保留末尾的 `/`：

   `https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

3. 运行 **Resources → Updates → Check for Updates**，按标准流程安装并在方便时重启 PixInsight。
4. 在 **Process → Convolution → AstroDiffraction** 打开模块。

手动安装请完整解压对应平台 ZIP，在 **Process → Modules → Install Modules** 中搜索解压包的 `bin/`。
保留模块旁的 `.xsgn`，以及完整的 `doc/tools/AstroDiffraction/` 文档目录；可直接打开其中的
`AstroDiffraction.html` 离线阅读帮助和许可。不要关闭签名检查。更新磁盘文件不会替换当前会话已经加载的模块。
目前没有 Linux 或 Intel Mac 安装包。内置预设已经嵌入模块，无需旁置预设文件。

### 联网、隐私与文件

“使用已解析的坐标（需要联网）”默认启用。执行检测，或在尚未检测时生成星芒，会按需通过 HTTPS 查询
CDS/VizieR 的 Bright Star、Tycho-2 及补充 Gaia DR3；打开界面本身不查询。请求包含天区中心坐标、
半径、字段、返回数量上限和星等条件。**不上传图像像素、文件名、本机路径、账号或设备序列号；没有开发者遥测或使用跟踪。**
取消该选项后使用本地图像检测。服务及代理可见来源 IP 等常规连接信息，服务日志由 CDS 管理。

星表文本只在内存中处理，Gaia 缓存最多十分钟。HTTPS 验证服务器证书和主机名，响应有大小与结构/数值检查。
用户预设文件 `AstroDiffraction-user.adpresets` 存放于 Windows 的 `%LOCALAPPDATA%\AstroDiffraction`
或 macOS 的 `~/Library/Application Support/AstroDiffraction`，保存时在同一目录创建临时文件。
低内存 FFT 暂存使用系统临时目录，完成、取消或异常时释放。光谱数据库只读；图像结果由用户通过 PixInsight 保存。
模块不启动外部程序、不安装可执行代码、不请求管理员权限。详见包内用户说明。

### 验证范围

macOS V1.7.4 已完成原生模块编译。未改动的打包／签名助手、历史处理及光学算法复用之前通过的验证结果。新模块使用 Fluorine7 CPD 签名，通过 SHA-512/Ed25519 密码学验证；安装包检查覆盖内部版本、正式构建标记、准确的模块／签名字节和全部 16 份文档许可。PI 官方接口对新模块和更新索引均返回有效签名。用户已确认 macOS 界面能看到新提示。先前的历史处理验证包括原生回归、PJSR 接口检查，以及现有 PI 中独立 32 位灰度和 64 位 RGBA 图像的撤销／重做；完整工作台 GUI 验证仍未完成。
Windows V1.7.4 已在 VS 2022 x64 Release 下编译通过。本次仅增加提示、版本和文档，复用 V1.7.3 已通过的 39 项常规原生回归；本次重新构建的安全修补库通过 SDK CRC/LUT CVE 探针。DLL 拉回 Mac 后单独签名，通过 SHA-512/Ed25519 验签，PI 官方接口对 DLL 和此次 XRI 均返回有效的 Fluorine7 签名。安装包包含匹配签名及全部 16 份用户文档／许可文件。Windows PI 内实际加载、界面显示及完整用户图像验收仍未完成；未重复测量 Windows 速度或峰值内存，最高 32768 入瞳档完整渲染仍未完成。

## English

AstroDiffraction is a native PixInsight Process for PixInsight 1.9.5.
**macOS and Windows are both V1.7.4, internal version `1.7.4.0001`.**
The modules and update index are signed with the **Fluorine7 CPD identity**.

**Windows V1.7.4:** compiled on the Windows build host, transferred to the Mac, and separately signed with the Fluorine7 identity. The signature is verified before packaging. The superseded Windows V1.7.3 package, original DLL and matching signature are archived by version.

Superseded modules, matching signatures and original packages are kept in [archive/](archive/).
PixInsight's updater downloads only the current packages listed in the update index; full Git clones include the archive.

| Platform | Package |
| --- | --- |
| macOS 14 or later, Apple Silicon | [Download for macOS](AstroDiffraction-1.7.4.0001-macos-arm64.zip) |
| Windows x64 | [Download for Windows](AstroDiffraction-1.7.4.0001-windows-x64.zip) |

### V1.7.4 for macOS and Windows

A permanent framed reminder appears below the top command bar. Key conditions are bold; the text
wraps and remains visible when switching or scrolling parameter pages:

> Use AstroDiffraction after **color balance and BXT**, **before stretching**, while the image is **still linear**.

This update adds the interface reminder, version and documentation changes. Processing algorithms
and history behavior retain the V1.7.3 implementation.

### History fixes retained from V1.7.3

Fixes **撤回星芒** restoring pixels while leaving the AD step applied in PixInsight history.
Retraction now restores the native history position. Redo remains available until new processing
replaces the undone branch. Generating again leaves one new applied AD step, preserving earlier
processing. Intervening image or history edits are guarded. This avoids obsolete AD history/swap
accumulation during repeated adjustments; it does not reduce peak generation RAM.

### Sampling and speed improvements retained from V1.7.2

Large kernels and every physical far-field tier now use factor-2 intensity sampling and Lanczos-16
detector integration. An earlier blend between standard and far fields improves outer-wing accuracy.
Up to eight bounded workers accelerate cold optical builds without changing the corrected sampling,
double-precision arithmetic or field coverage. Paired native benchmarks on one Mac reduced large-kernel
build time by about 36% and expanded far-field rendering time by about 23%, relative to the preceding
high-accuracy source revision. These are Mac results, not Windows timings, comparisons with V1.7.1, or full PixInsight workflow timings.
Catalog downloads now stop on cancellation and have total time limits; photometry bounds are hardened.

With factor-2 sampling, a 32768 pupil grid requires about 16.1 GiB of spectrum scratch space,
or 24.1 GiB if intensity also spills to disk, plus a 512 MiB reserve. SDK security backports,
hardened preset I/O, complete user documentation and third-party notices are retained.
Windows now includes the V1.7.4 permanent reminder. The macOS package retains its exact bytes and
signature. Both platforms' superseded V1.7.3 packages, modules and matching signatures are archived.

### Installation

Add the following URL under **Resources → Updates → Manage Repositories**, including the final `/`:

`https://raw.githubusercontent.com/Fluorine7/AstroDiffraction-PixInsight-Releases/main/`

Check for updates, install normally and restart PixInsight when convenient. Open
**Process → Convolution → AstroDiffraction**. For manual installation, extract the entire ZIP and search
its `bin/` directory in **Process → Modules → Install Modules**. Keep the adjacent `.xsgn` and the entire
`doc/tools/AstroDiffraction/` tree; open its HTML file for offline help and licenses. Keep signature checks enabled.
Linux and Intel Mac packages are not provided. Supplied presets are embedded.

### Network, storage and validation

The default solved-coordinate option queries CDS/VizieR over HTTPS on detection, or generation requiring detection.
Requests include the solved field centre, radius, fields, row limit and magnitude filters. Opening the interface
does not query catalogs. Image pixels, filenames, local paths, accounts and device serial numbers are not uploaded.
There is no developer telemetry or usage tracking. Disable the option for local image detection. The service and
any proxy see ordinary connection metadata such as the source IP.

Catalog text stays in memory, with a supplementary Gaia cache of up to ten minutes. Server certificates and hostnames,
response size, table structure and numbers are checked. User presets use `%LOCALAPPDATA%\AstroDiffraction` on Windows
or `~/Library/Application Support/AstroDiffraction` on macOS, with temporary files in the same directory. Low-memory
FFT scratch uses the system temporary directory and is released on completion, cancellation or exceptions.
The module launches no external programs, installs no executable code and requests no elevated privileges.

macOS V1.7.4 compiles successfully. Passing results for unchanged packaging/signing helpers, history
handling and optical algorithms are reused. The new Fluorine7 module signature passes SHA-512/Ed25519
verification; package checks cover the embedded version, production markers, exact signed bytes and
all 16 documentation/license files. The official PI APIs report valid signatures for the new module and
update index. The user has confirmed the reminder is visible on macOS. Earlier history checks
include native/PJSR regressions and exact Undo/Redo on disposable mono32/RGBA64 fixtures in an existing
PI instance; complete workbench GUI validation remains pending.
Windows V1.7.4 builds successfully with VS 2022 x64 Release. This update changes only the interface
reminder, version and documentation; the 39 passing native regressions from V1.7.3 are reused.
The rebuilt security libraries pass the SDK CRC/LUT CVE probe in this build. The transferred DLL was
signed separately on the Mac and passes SHA-512/Ed25519 verification. The official PI APIs report
valid Fluorine7 signatures for the DLL and this update index. The package contains the matching
signature and all 16 documentation/license files. Windows PI loading, the new reminder's appearance
and full GUI/user-image validation remain pending. Windows speed and peak RAM were not rebenchmarked;
a full render at the largest 32768 pupil tier remains pending.

## Acknowledgments and licenses

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors (https://pixinsight.com/).

Both packages include `THIRD-PARTY-NOTICES.txt` and complete license texts under `doc/tools/AstroDiffraction/`.
A CPD signature identifies the developer and verifies integrity; it is not Pleiades Astrophoto product approval or an endorsement.
