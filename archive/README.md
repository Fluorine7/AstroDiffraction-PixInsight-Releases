# 历史版本归档 / Release archive

从 V1.7.1.0002 开始，正式发布被新版本取代后，按以下结构保留其模块、原始匹配签名与完整安装包：

```text
archive/<模块内部版本>/<平台>/
  AstroDiffraction-pxm.dylib 或 AstroDiffraction-pxm.dll
  AstroDiffraction-pxm.xsgn
  AstroDiffraction-<版本>-<平台>.zip
```

当前归档的历史发布：

- [macOS arm64 1.7.2.0001](1.7.2.0001/macos-arm64/)
- [Windows x64 1.7.1.0002 r2（有效签名）](1.7.1.0002/windows-x64/)
- [macOS arm64 1.7.1.0002](1.7.1.0002/macos-arm64/)
- [macOS arm64 1.6.4.0001](1.6.4.0001/macos-arm64/)
- [Windows x64 1.6.0.0001](1.6.0.0001/windows-x64/)
- [Windows 1.7.1.0002 首次发布（无效签名，仅供追溯）](1.7.1.0002/windows-x64/invalid-signature-r1/)

归档用于版本追溯，保留原文件及原签名，不使用新版本覆盖旧文件。
旧安装包保留其当时的文档和资源，不能用当前版本的功能或验证结论描述它们。
常规安装和更新请使用仓库根目录的当前安装包及 `updates.xri`。

`updates.xri` 不引用本目录中的任何文件，因此 PixInsight 更新系统不会下载这些归档。
直接克隆或下载整个 Git 仓库仍会包含归档。

Superseded official releases are retained by internal module version and platform, with their original
module, matching signature and complete ZIP. Archived files are not overwritten by subsequent releases.
They preserve the documentation and resources of their original release; current validation claims do not
apply retrospectively. Use the current packages at the repository root for normal installation.

The update index never references this directory, so PixInsight's updater does not download archived files.
A full Git clone or repository download still includes the archive.
