下载 [升级工具包](https://github.com/YundaDesk/yundastore-releases/releases/download/v1.0.2/yundastore-to-1.0.2-upgrade.1.zip)，解压后按以下步骤操作。

# Yundastore 升级至 1.0.2

适用于已有官方 **1.0.0 或 1.0.1** 店铺。更新配套后端、Worker 和前台，包含多级分类、完整结果分页及筛选栏溢出修复。原数据库、Redis、对象存储和其他配置继续使用，不重新导入商品。

## 准备

Node.js **22.23.2**、支持 SSHSIG 的 OpenSSH、支持本地 Skill 的 Agent。ZIP 已包含 CLI/依赖、Skill、两版源签名 bundle、1.0.2 bundle、前台源码、许可和元数据，不需要 npm install。Windows 原生运行未在本次验证。

解压到独立目录，保留原安装目录、Plan、checkpoint、本地受保护凭据 Profile 和品牌资产。从原安装/升级历史确认**当前版本**，不要猜测。模板保持不变。

## 刷新升级授权

在解压后的目录运行，第一条按实际源版本选择：

```sh
# 当前为 1.0.0 时：
node cli/bin/yundastorectl.mjs stable upgrade-refresh --input refresh-source-1.0.0.json
# 当前为 1.0.1 时改用：
node cli/bin/yundastorectl.mjs stable upgrade-refresh --input refresh-source-1.0.1.json
# 两种情况都执行：
node cli/bin/yundastorectl.mjs stable upgrade-refresh --input refresh-target.json
```

离线改用同名 `-offline.json`。当前签名授权到期时间为台北 **2026-11-22 00:08**；过期后必须获取官方续发元数据，不修改有效期、不删除状态。

## 交给 Agent

让 Agent 读取 `.agents/skills/yundastore-store-lifecycle/SKILL.md`，并告诉它：

> 请把我已有的 Yundastore 店铺升级到 1.0.2。先从原历史确认当前是 1.0.0 还是 1.0.1。使用当前目录的 `cli/bin/yundastorectl.mjs`，目标 bundle 为 `bundle/`、目标前台材料为 `storefront/`；源 bundle 和材料分别选择 `source-bundles/<当前版本>/`、`source-storefronts/<当前版本>/`。先刷新两版授权、核对许可、定位原资源，完成外部备份，再展示完整升级计划；我明确批准后才执行。保留店铺数据、图片、配置和品牌资产，不走新建流程，不在聊天收集 Token，不创建真实订单。

已有同一许可接受可以复用，缺少记录时须用户明确接受。备份和升级分别需要批准精确 Plan。顺序：备份核验 → 原资源核验 → Backend/Admin → Worker → 前台 → readiness/Bridge/CORS/前台身份验证。

中断保留原 Plan 和 checkpoint，使用 `stable upgrade-resume`，不要再次 apply；只读验收使用 `stable upgrade-verify`。构建等待、ACK 丢失或短暂探针失败可继续读取原部署；身份漂移、缺失备份和过期批准会阻断。未提供全栈自动回退，破坏性恢复须单独计划。

完成后人工检查分类、筛选、排序、分页及桌面/手机布局，核对原商品图片与库存。下载包验收使用合成 Provider，不等同于具体店铺实测；实际执行后仍须验收。

许可见 `LICENSE-1.1.md`，签名规则见 `TRUST.md`，输入字段见 Skill 的 `references/upgrade.md`。下载或刷新本身不会修改店铺。
