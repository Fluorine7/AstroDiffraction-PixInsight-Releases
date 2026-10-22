# AstroDiffraction — PixInsight 发布仓库 / Release Repository

© Fluorine Zhu 2026

## 中文

这里提供 AstroDiffraction 原生 PixInsight Process 的安装包，适用于 PixInsight 1.9.5。
**macOS 最新版为 V1.7.3，模块内部版本 `1.7.3.0001`；Windows 保持 V1.7.1，内部版本 `1.7.1.0002`（签名修订 r2）。**
模块及更新索引使用 **Fluorine7 CPD 开发者身份**签名。

**Windows 签名修订 r2：** 修复原 Windows 包的无效模块签名。DLL 内容及内部版本 `1.7.1.0002` 不变，已单独重签，并使用出错 Windows 的 CPD 公钥通过 SHA-512/Ed25519 验签。请下载下方带 `-r2` 的包或重新检查更新；旧失败包仅保留在归档中。

旧版模块、匹配签名及原安装包保存在 [archive/](archive/)。更新索引只引用当前版本，PixInsight 更新不会下载归档；完整 Git 克隆仍包含它们。

| 平台 | 安装包 |
| --- | --- |
| macOS 14 及以上，Apple Silicon | [下载 macOS 版](AstroDiffraction-1.7.3.0001-macos-arm64.zip) |
| Windows x64 | [下载 Windows 版](AstroDiffraction-1.7.1.0002-windows-x64-r2.zip) |

### 本次 macOS 更新 — V1.7.3

- 修复“撤回星芒”只还原像素、却保留已应用 AD 历史的问题；现在同时恢复 PixInsight 的历史位置。
- 撤回后仍可通过 PI“重做”恢复结果；再次生成会替换旧分支，已应用历史中只保留新的 AD 步骤，之前的其他处理不受影响。
- 生成后若又修改了图像或历史，要求按顺序使用 PI 撤销，避免撤掉其他处理。
- 避免反复调整时累积旧 AD 历史和暂存数据；首次计算的峰值内存没有因此下降。

### 沿用 V1.7.2 的采样与速度改进

- 修复大核与远场的采样精度：所有物理远场层采用 2 倍强度采样、Lanczos-16 像元积分，并提前衔接标准场与远场，改善远端星芒轮廓及能量分布。
- 用最多八个、受硬件和任务规模限制的工作线程加速首次光学计算，保持修正后的采样精度、双精度运算和计算范围。
- 本机配对原生基准中，大核首次构建耗时减少约 36%，扩展远场探针首次渲染减少约 23%。基线是已修复精度的版本；这些数据不是相对 V1.7.1 的对比，也不代表所有机器或完整 PI 工作流的速度。
- 修复星表下载取消后继续请求的问题，加入请求时限，并加固测光数值边界。
- 大型 FFT 继续使用系统临时目录控制内存。32768 入瞳网格采用 2 倍采样时，频谱暂存约需 16.1 GiB；若强度也写入磁盘则约需 24.1 GiB，另预留 512 MiB。
- 保留此前的 SDK 安全回补、预设 I/O 加固及完整中英用户文档和第三方许可。

Windows 的 r2 包继续提供 V1.7.1 功能和已修复的模块签名，本次未更新 Windows 二进制。

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

macOS V1.7.3 已完成原生模块编译，打包／签名助手的 17 项检查通过。撤回逻辑的原生回归及生成的 PJSR 接口检查通过；在现有 PI 中对独立的 32 位灰度和 64 位 RGBA 图像验证了逐像素撤销／重做，以及再次生成后只有一条已应用 AD。运行中的已安装模块未被替换，因此尚未对 V1.7.3 工作台按钮完成整套 GUI 验证。光学算法未改动，沿用 V1.7.2 的采样与计算验证结果。模块使用 Fluorine7 CPD 签名，并通过 SHA-512/Ed25519 密码学验证；安装包检查覆盖内部版本、正式构建标记和全部文档许可。PI 官方接口对模块及更新索引的验签结果均为有效。
Windows r2 复用原有已通过的编译、36 项常规原生回归及 SDK CRC/LUT CVE 探针结果。本次没有把 macOS 的优化或速度结论套用到 Windows。完整 PI 界面、用户图像效果验收和最高 32768 入瞳档完整渲染仍未完成。

## English

AstroDiffraction is a native PixInsight Process for PixInsight 1.9.5.
**macOS is now V1.7.3, internal version `1.7.3.0001`. Windows remains V1.7.1, internal version `1.7.1.0002` (signature revision r2).**
The modules and update index are signed with the **Fluorine7 CPD identity**.

**Windows signature revision r2:** fixes the invalid module signature in the original Windows package. The DLL bytes and internal version `1.7.1.0002` are unchanged. Its new signature was generated separately and passes SHA-512/Ed25519 verification with the affected Windows installation's CPD public key. Use the `-r2` package or check for updates again; the failed original package is retained only in the archive.

Superseded modules, matching signatures and original packages are kept in [archive/](archive/).
PixInsight's updater downloads only the current packages listed in the update index; full Git clones include the archive.

| Platform | Package |
| --- | --- |
| macOS 14 or later, Apple Silicon | [Download for macOS](AstroDiffraction-1.7.3.0001-macos-arm64.zip) |
| Windows x64 | [Download for Windows](AstroDiffraction-1.7.1.0002-windows-x64-r2.zip) |

### macOS V1.7.3

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
high-accuracy source revision. These are not comparisons with V1.7.1 or full PixInsight workflow timings.
Catalog downloads now stop on cancellation and have total time limits; photometry bounds are hardened.

With factor-2 sampling, a 32768 pupil grid requires about 16.1 GiB of spectrum scratch space,
or 24.1 GiB if intensity also spills to disk, plus a 512 MiB reserve. SDK security backports,
hardened preset I/O, complete user documentation and third-party notices are retained.
The Windows r2 binary and its V1.7.1 functionality are unchanged in this release.

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

macOS V1.7.3 compiles successfully; 17 packaging/signing-helper checks pass.
The production retraction-handler regression and generated PJSR bridge checks pass. In an existing
PI session, disposable 32-bit mono and 64-bit RGBA fixtures verify exact Undo/Redo and one applied AD
step after regeneration. The installed module was not replaced, so a complete GUI check of the
V1.7.3 workbench button remains pending. Unchanged optical code retains the V1.7.2 validation results.
The Fluorine7 module signature is verified with SHA-512/Ed25519; package checks cover the embedded
version, production markers and complete documentation. The official PI APIs report valid Fluorine7
signatures for the module and update index.
The existing Windows compilation, 36 standard native checks and CRC/LUT CVE probe results still apply to
its unchanged r2 package. macOS performance claims do not apply to that Windows binary.
Full PI GUI/user-image validation and a complete render at the largest 32768 pupil tier remain pending.

## Acknowledgments and licenses

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors (https://pixinsight.com/).

Both packages include `THIRD-PARTY-NOTICES.txt` and complete license texts under `doc/tools/AstroDiffraction/`.
A CPD signature identifies the developer and verifies integrity; it is not Pleiades Astrophoto product approval or an endorsement.
