# Yundastore 1.0.1 — 分类商品展示修复

父分类和中间分类现在汇总自身及所有有效、对店铺可见的后代分类商品，保留直接子分类快捷入口。叶子分类仍只展示自身商品。

商品按 ID 去重，筛选、排序、总数和分页在服务端处理，移除前 100 件商品截断。分类移动、删除及商品关联变化在后续查询中生效；保留发布状态、销售渠道、地区价格和库存规则。

本版本同时交付 Backend/Admin、Worker、default 和 B2B electronics 前台材料。Backend 与 Storefront 必须配套更新。发布不会自动升级任何已有店铺；已有店铺升级需另行生成并批准受控计划。

## 下载

下载 `yundastore-1.0.1-install.zip` 即可获得 CLI、依赖、Skill、签名发行包和前台部署源码。`zip-delivery.json` 与 `zip-delivery.sig` 用于校验安装包；安装前按 README 执行 `stable refresh`。

保留 v1.0.0 原有下载与签名材料。许可继续使用 1.1，Bridge Contract 继续使用 1.5.0。

## 验证

- 真实 Medusa/PostgreSQL 分类测试覆盖三级分类、父分类直接关联、多分类去重、超过 200 件商品的分页和排序、库存筛选、分类及关联变更、未发布及其他销售渠道隔离。
- 分类专项 37 项前台测试、5 项后端单元测试通过；真实数据库集成测试另行通过。
- 原生 Linux/amd64 两轮独立构建一致，实际镜像运行验证通过。
- CLI 全量 895 项测试通过，无失败或跳过。
- default 与 B2B electronics 各两轮原生构建产物一致，两套封装部署源码构建通过。
- 本次生成 SBOM、NOTICE 和来源证明；未改商品名称、图片或现有店铺数据。

第三方上游漏洞按 ADR-0034 仅记录。本次复用未变依赖的历史漏洞记录，并生成当前产物 SBOM，不声称完成新的漏洞数据库扫描或消除全部上游漏洞。

## 官方镜像

- `ghcr.io/yundadesk/yundastore-backend-admin-public@sha256:44b521b07948442d9969cca388a58e799fa4de1d55100d716574cb3f41df2a85`
- `ghcr.io/yundadesk/yundastore-worker-public@sha256:5413af0a03d4d2c407d9e1276f105743bb57c8e9a75e045b232ccca6a2aecf58`

产品源码提交：`304e01b63e8ca6083a5d889a9b8a678889a7d451`。私有源码未推送到公开发行仓库。
