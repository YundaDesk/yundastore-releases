# Yundastore

通过 AI Agent 的本地设置向导，在你自己的 Railway 和 Vercel 账号里创建电商店铺。
可选基础商店或 B2B electronics 模板，包含店铺前台、商品与订单管理后台。

- **Vercel**：托管店铺前台。
- **Railway**：运行后端、管理后台、Worker 和数据服务。
- **你负责**：云服务账号、域名及相关费用。

> **当前版本安装提示**：Stable 1.0.0 的安装授权有效至 **2026 年 10 月 23 日 21:29（UTC+8）**。
> 授权更新功能尚未发布。超过该时间请等待新的安装工具与授权材料；重复下载 1.0.0 不会续期。
> 已部署的店铺不会因此停止运行。

## 1. 准备好这些

- macOS 或 Windows，以及支持本地 Skill、终端和浏览器的 AI Agent。
- Node.js **22.23.2**，以及支持 SSHSIG 的 OpenSSH `ssh-keygen`。
- 你自己的 Railway、Vercel 账号和域名。
- 店铺所需的支付、邮件服务配置；按设置向导填写。

Token、密码等凭据稍后在本地设置页面中输入，**不要发送到聊天里**。

## 2. 下载四个安装文件

打开 [Stable 1.0.0 下载页](https://github.com/YundaDesk/yundastore-releases/releases/tag/v1.0.0)，下载：

| 文件 | 用途 |
| --- | --- |
| [yundastorectl-1.0.0.tar.gz](https://github.com/YundaDesk/yundastore-releases/releases/download/v1.0.0/yundastorectl-1.0.0.tar.gz) | 本地安装工具及其依赖 |
| [yundastore-skill-1.0.0.tar.gz](https://github.com/YundaDesk/yundastore-releases/releases/download/v1.0.0/yundastore-skill-1.0.0.tar.gz) | 指导 Agent 建店的 Skill |
| [yundastore-stable-1.0.0-bundle.tar.gz](https://github.com/YundaDesk/yundastore-releases/releases/download/v1.0.0/yundastore-stable-1.0.0-bundle.tar.gz) | 安装工具验证的签名发行包 |
| [storefront-deployment-source-frozen.tar.gz](https://github.com/YundaDesk/yundastore-releases/releases/download/v1.0.0/storefront-deployment-source-frozen.tar.gz) | 部署到 Vercel 的前台材料 |

首次建店无需手动下载其余 SBOM、报告或单独的模板归档，也无需自行构建 Docker 镜像。

## 3. 解压到一个工作目录

例如创建 `yundastore-install`，按下面的布局解压。CLI 压缩包中的隐藏 `.dependencies` 目录
也要保留，不要只复制 `cli` 文件夹。

```text
yundastore-install/
├── cli/
├── .dependencies/
├── .agents/skills/yundastore-store-lifecycle/
├── bundle/
│   ├── release.json
│   ├── release.sig
│   ├── trust.json
│   ├── trust.sig
│   └── blobs/
└── storefront/
    └── apps/storefront/…
```

macOS 可在四个下载文件所在的目录执行：

```sh
mkdir -p yundastore-install/bundle yundastore-install/storefront
tar -xzf yundastorectl-1.0.0.tar.gz -C yundastore-install
tar -xzf yundastore-skill-1.0.0.tar.gz -C yundastore-install
tar -xzf yundastore-stable-1.0.0-bundle.tar.gz -C yundastore-install/bundle
tar -xzf storefront-deployment-source-frozen.tar.gz -C yundastore-install/storefront
```

Windows 可让 Agent 帮你按同样布局解压，保留压缩包中的目录关系。
在 Agent 中打开这个工作目录，并确认它已加载 `yundastore-store-lifecycle` Skill。
如果没有自动发现，请让它读取 `.agents/skills/yundastore-store-lifecycle/SKILL.md`。

## 4. 把这段话交给 Agent

```text
请使用当前目录的 yundastore-store-lifecycle Skill 帮我创建 Yundastore 店铺。
安装工具：cli/bin/yundastorectl.mjs
签名发行包：bundle/
前台部署材料：storefront/

先检查安装环境和签名材料，向我展示许可，等我明确接受后打开本地设置向导。
让我在向导中选择模板、填写账号配置与凭据；不要在聊天里收集 Token 或密码。
生成安装计划后，告诉我要创建哪些资源、费用由谁承担，再等我确认执行。
```

Agent 会依次带你完成：

1. 验证安装文件并展示许可，由你确认接受。
2. 打开本地设置页面，选择模板并填写店铺、云账号、域名、支付和邮件配置。
3. 展示安装计划，包括资源、费用边界和域名设置；由你确认后开始执行。
4. 按提示在域名服务商处设置 DNS，随后继续验证店铺和管理后台。

## 5. 安装中断怎么办？

在**原工作目录和原 Agent 会话**中说：

> 请检查刚才的安装进度，使用原计划和 checkpoint 继续，不要重新创建已有资源。

保留本地安装状态。若提示授权过期、签名无效或材料不一致，先让 Agent 解释错误；
不要删除状态文件、修改有效期或反复新建项目。

## 许可与更多说明

Yundastore 采用零价自用许可；云服务和第三方服务费用由你承担。
完整使用范围见 [许可 1.1](LICENSE.md)，首次信任和签名说明见 [TRUST.md](TRUST.md)，
版本变化见 [发行说明](RELEASE-NOTES-1.0.0.md)。
