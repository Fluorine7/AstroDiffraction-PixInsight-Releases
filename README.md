# AstroDiffraction — PixInsight 发布仓库 / Release Repository

© Fluorine Zhu 2026

## 中文

这里提供 AstroDiffraction 原生 PixInsight Process 的安装包，适用于 PixInsight 1.9.5。
**macOS 与 Windows 最新版均为 V1.7.1，模块内部版本 `1.7.1.0002`。**
模块及更新索引使用 **Fluorine7 CPD 开发者身份**签名。

**Windows 签名修订 r2：** 修复原 Windows 包的无效模块签名。DLL 内容及内部版本 `1.7.1.0002` 不变，已单独重签，并使用出错 Windows 的 CPD 公钥通过 SHA-512/Ed25519 验签。请下载下方带 `-r2` 的包或重新检查更新；旧失败包仅保留在归档中。

旧版模块、匹配签名及原安装包保存在 [archive/](archive/)。更新索引只引用当前版本，PixInsight 更新不会下载归档；完整 Git 克隆仍包含它们。

| 平台 | 安装包 |
| --- | --- |
| macOS 14 及以上，Apple Silicon | [下载 macOS 版](AstroDiffraction-1.7.1.0002-macos-arm64.zip) |
| Windows x64 | [下载 Windows 版](AstroDiffraction-1.7.1.0002-windows-x64-r2.zip) |

### 本次更新

- 新增“亮星增宽”0–1 控制，零值关闭额外增宽并保留通量恢复；改善亮星响应、星表核心匹配和 L 滤镜/QE 数据传递。
- 扩展亮星物理计算场，减少远端星芒被截断；重用光学核和积分结果，加快重复渲染。
- 大型 FFT 在内存不足时使用系统临时目录中的计算暂存，保持采样与计算范围。32768 计算场约需 10.1 GiB 暂存空间，另预留 512 MiB；首次计算可能较慢。
- 构建所用 zlib 与 Little CMS 已回移 CVE-2026-27171、CVE-2026-41254、CVE-2026-42798 的修复；不会由模块替换 PixInsight 核心或宿主库。
- 加固用户预设的读写、1 MiB 大小限制和独占临时文件，保留用户已有预设。
- 两个平台均附完整的中英用户说明、PCL 致谢、第三方许可及 PCL 内部算法版权声明。

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

两个平台均已完成原生模块编译；Windows 的 36 项常规原生回归及 SDK CRC/LUT CVE 探针通过。
本地 15 项相关检查覆盖打包、签名助手和亮星宽度；macOS SDK 探针结果复用本轮未变的补丁库验证。
安装包检查覆盖版本、正式构建标记、两平台完整的文档与许可目录。当前版本的完整 PI 界面和用户图像效果验证仍待进行。

## English

AstroDiffraction is a native PixInsight Process for PixInsight 1.9.5.
**Both macOS and Windows are now at V1.7.1, internal version `1.7.1.0002`.**
The modules and update index are signed with the **Fluorine7 CPD identity**.

**Windows signature revision r2:** fixes the invalid module signature in the original Windows package. The DLL bytes and internal version `1.7.1.0002` are unchanged. Its new signature was generated separately and passes SHA-512/Ed25519 verification with the affected Windows installation's CPD public key. Use the `-r2` package or check for updates again; the failed original package is retained only in the archive.

Superseded modules, matching signatures and original packages are kept in [archive/](archive/).
PixInsight's updater downloads only the current packages listed in the update index; full Git clones include the archive.

| Platform | Package |
| --- | --- |
| macOS 14 or later, Apple Silicon | [Download for macOS](AstroDiffraction-1.7.1.0002-macos-arm64.zip) |
| Windows x64 | [Download for Windows](AstroDiffraction-1.7.1.0002-windows-x64-r2.zip) |

This release adds adjustable bright-star widening, improves catalog-core matching and L filter/QE transfer,
extends the physical far field, reuses optical results, and provides bounded-memory FFT scratch storage.
A 32768 field requires about 10.1 GiB of temporary disk space plus a 512 MiB reserve.
Private SDK builds include upstream fixes for CVE-2026-27171, CVE-2026-41254 and CVE-2026-42798.
Preset I/O uses bounded reads and exclusive temporary files. Both packages contain complete user documentation,
PCL acknowledgments and third-party license notices.

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

Both native modules compile successfully. The 36 standard Windows native checks and CRC/LUT CVE probe pass.
Fifteen local checks cover packaging, the signing helper and bright-star width. Existing macOS SDK results are reused
for unchanged patched libraries. Package checks cover versions, production markers and the full documentation tree.
Full PI GUI and user-image validation for this build is still pending.

## Acknowledgments and licenses

This product is based on software from the PixInsight project, developed by Pleiades Astrophoto and its contributors (https://pixinsight.com/).

Both packages include `THIRD-PARTY-NOTICES.txt` and complete license texts under `doc/tools/AstroDiffraction/`.
A CPD signature identifies the developer and verifies integrity; it is not Pleiades Astrophoto product approval or an endorsement.
