# Stable 首次信任与撤回

官方发行仓：https://github.com/yundadesk/yundastore-releases
首次信任依赖官方 GitHub 账号、发行仓和 HTTPS 下载链；同仓指纹不是独立身份认证。
CLI 内置根公钥。trust.json 由根密钥签署，release.json 由 trust 授权的发行密钥签署。
各物料和许可按 release 的摘要校验；SHA256SUMS 仅帮助传输完整性检查，不能代替签名。
不要替换内置公钥，不使用测试密钥，不把许可接受当作执行批准。

- root: `SHA256:WYwyPVQmGuvNh/+AZFhkATFKGrI9daYNkH+U1h2d+0M`
- issuer: `SHA256:yX+uCOC1FZ1lrSm4RgezPw/YAz+vLkdpFbZfQ4eeHPg`

当前安装包：[1.0.3](https://github.com/YundaDesk/yundastore-releases/releases/tag/v1.0.3)。
安装前使用新版 CLI 的 `stable refresh` 获取当前签名 trust 和运行授权，步骤见 [README](README.md)。

当前 trust revision 2 / runtime update revision 1，有效至 **2026-11-22 00:08（UTC+8）**。
后续同一个 Stable 发行包可继续使用更高修订的签名元数据，不需要重建镜像或模板。
维护方须在到期前提供后续签名材料；这不是自动签发或永久离线安装。
原 Stable 1.0.0 包内的旧 trust/运行授权和所有旧发行附件保留不变。

安装更新与撤回通过官方 stable-metadata 渠道提供；已有店铺升级使用 `stable upgrade-refresh` 和独立的 stable-upgrade-metadata 渠道。历史快照保存在对应工具更新发行中。
CLI 验证固定根签名、发行密钥授权、精确 release/descriptor 绑定、修订号、有效期和累计撤回。
缓存有效时可以离线使用；缓存过期、损坏或已撤回时不能绕过。已部署店铺不会因此被远程删除。
运行授权更新后旧 Plan 不自动续期；重新生成计划并取得明确批准后才执行云操作。
