# 本 fork 的签名约定

fork：`erev988/Android-AI-gateway`

## 证书

| 项 | 值 |
|---|---|
| Subject | `CN = AI Gateway (erev988 fork), O = erev988, C = CN` |
| 算法 | RSA 2048，SHA-256 自签 |
| 有效期 | 2026-10-27 → 2056-10-19（30 年） |
| SHA-256 指纹 | `B6:36:3D:79:84:12:F9:AF:E5:D5:6B:7C:C5:E7:A0:7F:32:6E:AA:61:52:86:76:14:06:08:6A:92:E4:D7:64:B7` |
| keyAlias | `aigw-release` |
| 格式 | PKCS#12，AES-256-CBC / PBKDF2-SHA256 |

## CI secrets（已写入 fork）

`KEYSTORE_BASE64`、`KEYSTORE_PASSWORD`、`KEY_ALIAS`、`KEY_PASSWORD`

`KEYSTORE_BASE64` 是上面那个 keystore 的 base64；`KEYSTORE_PASSWORD` 与 `KEY_PASSWORD` 相同。

## 与上游官方包的兼容性

**签名不同，不能覆盖安装。** 上游官方 release 包用的是另一套证书
（SHA-256 `9B:37:A8:F0:54:97:19:25:31:7C:12:81:DC:AB:AA:99:B1:9B:6D:31:0A:EB:E3:88:60:CD:FF:66:14:2D:96:B0`）。
从官方包切到本 fork 的包，需先卸载官方版（会丢应用内数据）；之后本 fork 的包之间可以原地升级。

## 密钥丢失的后果

`keytool`/keystore 一旦丢失，已安装的包就再也无法原地升级，只能卸载重装。
**keystore 本体只存在于 GitHub secrets 里**，本地不留副本。
