# Yundastore

通过 AI Agent 的本地设置向导，在你自己的 Railway 和 Vercel 账号里创建电商店铺。
可选基础商店或 B2B electronics 模板，包含店铺前台、商品与订单管理后台。

- **Vercel**：托管店铺前台。
- **Railway**：运行后端、管理后台、Worker 和数据服务。
- **你负责**：云服务账号、域名及相关费用。

> **只需下载一个 ZIP**：[Yundastore 1.0.0 安装包](https://github.com/YundaDesk/yundastore-releases/releases/download/v1.0.0/yundastore-1.0.0-install.1.zip)。
> 解压后已包含安装工具、依赖、Skill、签名发行包及前台部署材料，无需运行 npm install。

## 1. 准备好这些

- macOS 或 Windows，以及支持本地 Skill、终端和浏览器的 AI Agent。
- Node.js **22.23.2**，以及支持 SSHSIG 的 OpenSSH `ssh-keygen`。
- 你自己的 Railway、Vercel 账号和域名。
- 店铺所需的支付、邮件服务配置；按设置向导填写。

Token、密码等凭据稍后在本地设置页面中输入，**不要发送到聊天里**。

## 2. 下载并解压

下载上面的 ZIP，使用系统解压工具解压，打开其中的 `yundastore-install` 文件夹。
不要逐个下载 release 中的其他附件；那些是独立校验材料和历史交付文件。

```text
yundastore-install/
├── README.md
├── refresh.json
├── refresh-offline.json
├── cli/                          # 已含依赖
├── .agents/skills/yundastore-store-lifecycle/
├── bundle/                       # 原签名发行包
├── storefront/                   # Vercel 前台部署材料
└── metadata/                     # 当前签名元数据快照
```

在 Agent 中打开这个目录，确认它已加载 `yundastore-store-lifecycle` Skill。
如果没有自动发现，请让它读取 `.agents/skills/yundastore-store-lifecycle/SKILL.md`。

旧用户也请解压到新目录使用，不要混合覆盖旧 CLI；保留已有安装状态和 checkpoint。
ZIP 不包含 Node.js 或云服务账号，环境要求见上方；执行计划前仍需你明确批准。

## 3. 刷新安装授权，然后交给 Agent

在 `yundastore-install` 目录中，`refresh.json` 已准备好。

执行（也可让 Agent 帮你执行）：

```sh
node cli/bin/yundastorectl.mjs stable refresh --input refresh.json
```

看到 `metadata_refreshed` 后继续。这个步骤会获取并验证当前的 trust 和运行授权，
无需重新下载镜像或模板。以后再次安装前也先执行它。

无法联网时，可使用 ZIP 自带的签名元数据快照：

```sh
node cli/bin/yundastorectl.mjs stable refresh --input refresh-offline.json
```

离线快照也必须仍在有效期内；过期后请联网刷新。安装包无需因快照过期而重新下载。

随后把这段话交给 Agent：

```text
请使用当前目录的 yundastore-store-lifecycle Skill 帮我创建 Yundastore 店铺。
安装工具：cli/bin/yundastorectl.mjs
签名发行包：bundle/
前台部署材料：storefront/

先使用上述新版 CLI 执行 stable refresh（输入文件包含 bundle 路径），确认成功。
再检查安装环境和签名材料，向我展示许可，等我明确接受后打开本地设置向导。
让我在向导中选择模板、填写账号配置与凭据；不要在聊天里收集 Token 或密码。
生成安装计划后，告诉我要创建哪些资源、费用由谁承担，再等我确认执行。
```

Agent 会依次带你完成：

1. 验证安装文件并展示许可，由你确认接受。
2. 打开本地设置页面，选择模板并填写店铺、云账号、域名、支付和邮件配置。
3. 展示安装计划，包括资源、费用边界和域名设置；由你确认后开始执行。
4. 按提示在域名服务商处设置 DNS，随后继续验证店铺和管理后台。

## 4. 安装中断怎么办？

在**原工作目录和原 Agent 会话**中说：

> 请检查刚才的安装进度，使用原计划和 checkpoint 继续，不要重新创建已有资源。

保留本地安装状态。若提示授权过期，先刷新官方签名元数据，再重新生成并批准安装计划。
若提示签名无效、撤回或材料不一致，先让 Agent 解释错误；
不要删除状态文件、修改有效期或反复新建项目。

## 许可与更多说明

Yundastore 采用零价自用许可；云服务和第三方服务费用由你承担。
完整使用范围见 [许可 1.1](https://github.com/YundaDesk/yundastore-releases/blob/main/LICENSE.md)，首次信任和签名说明见 [TRUST.md](https://github.com/YundaDesk/yundastore-releases/blob/main/TRUST.md)，
版本变化见 [发行说明](https://github.com/YundaDesk/yundastore-releases/blob/main/RELEASE-NOTES-1.0.0.md)。
