# 已失效的 Windows r1 签名归档 / Invalid Windows r1 signature

此目录保留 1.7.1.0002 首次 Windows 发布的原 DLL、原签名及 ZIP，仅供追溯。
原 `.xsgn` 已确认无法通过 SHA-512/Ed25519 验签，会导致 PI 报 Invalid code signature。
请使用根目录的 Windows `-r2.zip`；其中 DLL 字节相同，签名已单独重建并通过验签。
本目录不进入更新索引。

The original Windows r1 XSGN is cryptographically invalid and is retained as historical evidence.
Use the current Windows `-r2.zip` at the repository root. It contains the same DLL with a corrected,
independently verified signature. This archive is excluded from the update index.
