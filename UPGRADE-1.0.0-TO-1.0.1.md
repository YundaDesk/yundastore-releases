# Yundastore 1.0.0 → 1.0.1 升级工具

[下载官方升级 ZIP](https://github.com/YundaDesk/yundastore-releases/releases/download/upgrade-1.0.0-to-1.0.1-1/yundastore-1.0.0-to-1.0.1-upgrade.1.zip) · [发行及签名附件](https://github.com/YundaDesk/yundastore-releases/releases/tag/upgrade-1.0.0-to-1.0.1-1)

用于已有的官方 Yundastore 1.0.0 店铺。更新 Backend/Admin、Worker 和前台，复用原数据服务和配置，不重新导入商品。不要用此工具新建店铺。

## 准备

- Node.js **22.23.2**，支持 SSHSIG 的 OpenSSH `ssh-keygen`，支持本地 Skill 的 Agent。
- 保留原安装目录、Plan、checkpoint、本地凭据 Profile 和原品牌资产。不要覆盖旧 CLI 或删除状态。
- 本 ZIP 包含 CLI 及依赖、Skill、1.0.0/1.0.1 签名发行包、两版前台材料、许可和元数据快照，无需 npm install。
- 解压到独立目录；模板保持不变，不能通过本次升级切换模板。

## 先刷新两版授权

在解压出的 `yundastore-upgrade` 目录执行：

```sh
node cli/bin/yundastorectl.mjs stable upgrade-refresh --input refresh-source.json
node cli/bin/yundastorectl.mjs stable upgrade-refresh --input refresh-target.json
```

离线时把输入换成 `refresh-source-offline.json` 和 `refresh-target-offline.json`。离线快照仍受有效期约束；过期后联网刷新，不改时间或删除状态。此工具使用独立升级通道，不影响旧安装器。当前授权有效至 **2026-11-22 00:08（台北时间）**，后续由官方续发。

## 交给 Agent

在原安装会话中提供这个新目录，或让新会话读取原安装历史，然后发送：

> 请使用这个目录的 `.agents/skills/yundastore-store-lifecycle/SKILL.md`，把我已有的 Yundastore 1.0.0 店铺升级到 1.0.1。CLI 是 `cli/bin/yundastorectl.mjs`，源 bundle 是 `source-bundle/`，目标是 `bundle/`；源前台材料是 `source-storefront/`，目标是 `storefront/`。保留原 Plan、checkpoint、店铺数据、配置和品牌资产。先刷新两版升级授权、核验许可、定位原资源并完成外部备份，再给我看完整升级 Plan 和费用；我明确批准后才执行。不要走新建店铺流程，不要在聊天收集 Token，不要创建真实订单。

Agent 会通过受保护本地 Profile 获取凭据；已有许可接受可复用，缺少记录时需你明确接受。备份和升级分别需要批准精确 Plan。

升级顺序：备份核验 → 原资源核验 → Backend/Admin → Worker → 前台 → readiness、Bridge、CORS 和前台身份验证。商品、订单、客户、图片等仍使用原数据库与对象存储，其他环境变量不重写。维护期间可能短暂不可用。

## 中断与验收

保留原输入和检查点，使用 `stable upgrade-resume`；不要重复 apply。`stable upgrade-verify` 用于只读验收。构建等待或 ACK 丢失会查找同一部署；身份漂移、无备份或过期批准会阻断。全栈自动回退未提供，不能用仅双镜像回退代替整店恢复。

完成后浏览父分类、子分类、筛选及分页，确认商品图片、库存和价格；未经单独授权不创建真实订单。没有有效许可和精确 Plan 批准时，下载或刷新本身不会修改店铺。

详细输入与恢复说明：ZIP 内的 `UPGRADE-REFERENCE.md`。许可：[许可 1.1](LICENSE.md)；签名：ZIP 内的 `TRUST.md`。本工具已做本地签名和合成 Provider 流程验收，不宣称替代具体用户店铺的升级后验收。Windows 原生执行未在本次验证。
