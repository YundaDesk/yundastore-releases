# Yundastore Stable 1.0.0

Yundastore 提供运行在用户自有 Railway 与 Vercel 账号中的基础店铺，包含 default 和
B2B electronics 模板。云服务、域名及第三方服务费用由用户承担。

下载后保持 CLI 与依赖目录的相对布局，并安装 Node 22.23.2 和支持 SSHSIG 的 ssh-keygen。
将签名 bundle 解包到本地目录，将 Storefront deployment source 解包到另一个目录。
安装 Skill 后，由兼容 Agent 调用 yundastorectl 展示已验签许可、收集明确接受、
打开本地设置向导并生成精确 Plan。凭据只在本地向导中输入，不发送到聊天。

首次信任来自官方 GitHub 账号、发行仓与 HTTPS 下载链；公钥已内置 CLI。
同仓公布的指纹不构成独立身份证明。不得用下载文件中的任意根公钥覆盖内置根。
无法取得有效签名材料、信任或运行授权已经过期时，CLI 会拒绝执行。

许可为 1.1，署名 yundadesk；以已签 release 绑定的完整许可文本为准。
第三方组件受原许可约束，NOTICE、SBOM、来源材料和上游漏洞记录随发行提供。
上游漏洞依 ADR-0034 仅记录、不阻断，这不表示产物没有漏洞。

许可接受不等于云操作批准。Agent 必须展示 Plan 摘要、资源和费用边界，取得明确批准后
才执行。中断时沿用原批准和 checkpoint 恢复，不能通过改摘要、换根密钥或直接重试云 API 绕过拒绝。
本版本 Stable Plan 6.2 不导入旧 RC continuation/handoff。

撤回与运行授权更新由同一官方发行渠道提供签名材料。收到撤回后不得以旧版本材料绕过；
离线缓存也必须满足原有效期及本机已记录的撤回状态。公开发行不自动部署任何生产店铺。
