# Stable 首次信任与撤回

官方发行仓：https://github.com/yundadesk/yundastore-releases
首次信任依赖官方 GitHub 账号、发行仓和 HTTPS 下载链；同仓指纹不是独立身份认证。
CLI 内置根公钥。trust.json 由根密钥签署，release.json 由 trust 授权的发行密钥签署。
各物料和许可按 release 的摘要校验；SHA256SUMS 仅帮助传输完整性检查，不能代替签名。
不要替换内置公钥，不使用测试密钥，不把许可接受当作执行批准。

- root: `SHA256:WYwyPVQmGuvNh/+AZFhkATFKGrI9daYNkH+U1h2d+0M`
- issuer: `SHA256:yX+uCOC1FZ1lrSm4RgezPw/YAz+vLkdpFbZfQ4eeHPg`

本次 trust 有效至 2026-11-21T13:29:28.389Z；安装运行授权有效至 2026-10-23T13:29:28.389Z。
运行授权过期时不得绕过，应取得官方后续有效材料；已部署店铺不会因此被远程删除。
撤回及更新通过官方发行渠道公布签名 trust；本机验证器保留已见撤回并拒绝回退。
