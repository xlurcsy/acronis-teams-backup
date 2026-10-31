# acronis teams backup：实际涵盖哪些内容、缺少哪些内容，以及如何以每月 4 美元的价格运行它

当有人搜索 acronis teams backup 时，通常背后会有两个问题。第一个是功能性问题：Acronis 实际上能捕获多少 Microsoft Teams 数据，因为答案并不直观。第二个是实践问题：运行它需要花费多少，以及是否有比直接购买 Acronis 更便宜的途径。

直接回答：Acronis Cyber Protect 备份整个团队 — 名称、成员列表、频道及其内容、团队邮箱、会议和团队站点 — 并在细粒度级别恢复它们。它不备份聊天消息（Teams 中的私聊和群聊），频道对话无法恢复，只能导出。在成本方面，托管服务提供商 Sharktech 销售 Acronis 备份服务，每月 4 美元起，包含 200 GB 云存储，是运行该服务最便宜的入门途径之一。

> **快速回顾：** 对于大多数寻找托管 Acronis 的小型团队来说，Sharktech 的 200 GB 方案是合理的起点 — 每月 4 美元，按月计费，每增加 1 GB 加收 0.04 美元，没有长期合同。Teams、Exchange、SharePoint 和 OneDrive 工作负载均通过同一个 Acronis 控制台处理。👉 [Check Sharktech's Acronis plans and live pricing](https://portal.sharktech.net/cart.php?a=add&pid=648&configoption%5B1862%5D=200&configoption%5B1863%5D=0&billingcycle=monthly&aff=1626)

## Acronis 实际上在 Microsoft Teams 中备份了什么

根据 Acronis 自身的文档，备份计划捕获整个团队：团队名称、成员列表、所有频道及其内容、团队邮箱和会议，以及关联的团队站点。OneNote 笔记本是一个独立的选项，你必须在备份计划中明确启用它 — 这是一个容易遗漏的复选框，人们往往在稍后发现缺少笔记本时才发现。

在恢复方面，控制权非常细。Acronis 支持恢复整个团队（包含成员和结构）、单个频道、频道文件、团队邮箱、该邮箱内的单个邮件文件夹或消息、会议以及团队站点。这种粒度很重要，因为在部分恢复场景中 — 有人删除了一个文件夹或错误的会议条目 — 你不需要回滚整个团队。

现在来看看需要注意的事项。有些内容根本不会备份：

- 常规频道和自定义频道的审核设置 — 这是 Microsoft Graph beta API 的限制，不是 Acronis 的偷工减料
- 会议笔记
- 聊天部分的消息，包括一对一私聊和群聊
- 表情符号和表扬

频道对话（频道内的帖子）也无法恢复。你可以将它们下载为一个包含线程的单个 HTML 文件，但无法将它们放回 Teams。对于频道选项卡，只有 Word、Excel、PowerPoint、PDF 和文档库选项卡支持备份和恢复。

还有一个大多数人只有在第一次运行作业时才会遇到的运营细节：Teams 备份是资源密集型的，因此 Acronis Cyber Protect 云默认每天仅运行一次自动备份。如果你期待每小时的恢复点，这需要知道 — 尽管你可以为不同的团队以不同的保留策略运行手动计划。

## 为什么 Microsoft 的内置保留策略不能替代备份

Acronis 在其关于 Teams 保护的资料中提出的论点值得理解，即使它来自销售备份的供应商。他们的观点：Microsoft 的原生保留策略是为可用性和治理设计的 — 而非完整的备份、长期保留或可靠的时间点恢复。一旦保留窗口关闭或帐户被删除，内容将永久删除，没有内置的方法可以回滚到特定日期。

结构性原因是 Teams 数据并非存在一个地方。Acronis 将其描述为联合架构：私人和群组聊天存储在 Exchange Online 的隐藏文件夹中，频道消息存储在关联 Microsoft 365 组的邮箱中，频道文件存储在 SharePoint Online 中，聊天中共享的文件存储在 OneDrive for Business 中，会议录制存储在 OneDrive 或 SharePoint 中。删除一个团队会引发连锁反应 — 该组被删除，SharePoint 站点被锁定，Exchange 组件被隐藏 — 而且事后尝试手动拼凑恢复通常是不完整的。

这种风险在现实中有具体的表现形式。Acronis 列出了五种常见场景：离职员工的许可证被删除，将他们的邮箱以及其中的 Teams 聊天记录标记为删除；恶意或被盗的管理员帐户清除频道、清除 SharePoint 库或擦除聊天历史记录 — 即使有回收站，二次删除或保留策略仍然可能使数据永久丢失；配置错误的保留策略；简单的管理员失误；以及延迟发现，即需要某个月份的频道讨论用于审计、HR 调查或法律事务，当保留窗口早已关闭时。受 GDPR、HIPAA 或 SOX 等框架约束的组织通常需要保留比 Microsoft 默认值更长的数据。无论你最终使用哪种备份工具，这都是独立备份存在的理由。

值得一提的是备份本身存储的位置。Acronis 指定了不可变性控制、强加密和隔离存储 — 备份存储在一个独立的系统中，勒索软件无法触及你的生产环境。这就是针对上述场景的“干净恢复点”逻辑。

## 如何在 Acronis Cyber Protect 中设置 Teams 备份

设置是一个云到云的连接过程，从你的 Microsoft 365 组织开始，无需在 Teams 本身上安装任何内容。在 Acronis 控制台内，流程如下：

1. 以管理员身份登录 Acronis Cyber Protect 控制台并进入 **Devices → Microsoft 365**。
2. 点击右上角的 **Add**，滚动到 Applications 部分，选择 **Microsoft 365 Business**。
3. 在 Microsoft Online Portal 登录页面，输入你 Microsoft 365 组织的管理员凭据，然后在权限屏幕上点击 **Accept** 以允许 Acronis 访问你组织的数据。
4. 让自动发现运行。控制台导入你的组、公共文件夹、站点集合、团队和用户。
5. 在左侧菜单中展开 Teams 节点，选择一个团队，点击面板中的 **Backup**，然后 **Create New**。这里你可以设置保留策略（“保留多久”），可以选择使用密码加密备份，然后点击 **Apply**。如果你想要立即进行第一次运行而不是等待计划任务，可以使用 **Run now**。

两点值得了解。首先，你可以创建一个 **Group Backup** 计划，涵盖组织中的所有团队或选定的子集 — 没必要为每个团队单独管理一个计划。其次，Teams 节点内的搜索只能按名称查找团队，且不支持通配符，因此如果你的组织有数百个命名不一致的团队，拼写很重要。

## 以每月 4 美元的价格通过 Sharktech 运行 Acronis

Sharktech 是一家在备份和托管领域拥有 21 年以上经验的托管服务提供商（根据其自己的云备份页面），以 Acronis Backup Service 的形式转售 Acronis 技术。所有方案均包含 200 GB 的起始存储，计费选项如下：

| 计费周期 | 包含存储 | 价格 | 超额存储费 | 订购 |
| --- | --- | --- | --- | --- |
| 每月 | 200 GB | $4.00/月 | $0.02/GB | [Order the monthly 200 GB plan](https://portal.sharktech.net/cart.php?a=add&pid=648&configoption%5B1862%5D=200&configoption%5B1863%5D=0&billingcycle=monthly&aff=1626) |
| 每季度 | 200 GB | $8.00/季度 | $0.04/GB | [Order via Sharktech](https://bit.ly/SharKtech) |
| 每半年 | 200 GB | $12.00/6个月 | $0.06/GB | [Order via Sharktech](https://bit.ly/SharKtech) |
| 每年 | 200 GB | $24.00/年 | $0.12/GB | [Order via Sharktech](https://bit.ly/SharKtech) |

如果你在订购前花 30 秒考虑，有一个细节值得注意：**计费周期越长，基础月费越低，但每 GB 的超额费用就越高。** 年付折合约 $2.00/月 — 最低的基础成本 — 但每额外增加 1 GB 需要支付 0.12 美元，是月付超额率的六倍。

所以计算方式取决于你的预测。运行一台备份量约 250-300 GB 的单台服务器的公司，选择年付并保持在 200 GB 基础范围内，总成本最低。如果备份集徘徊在 2 TB 左右，按月支付超额费用约为 $36（1,800 GB × $0.02），而按年支付则是 $216 — 月付的基础费率完全弥补了更高的基础价格。利用默认的每日计划从 Acronis 文档中估算你的真实保留占用，而不仅仅是你的实时数据大小，然后选择匹配的周期。👉 [Configure your storage and see the exact recurring total](https://portal.sharktech.net/cart.php?a=add&pid=648&configoption%5B1862%5D=200&configoption%5B1863%5D=0&billingcycle=monthly&aff=1626)

平台覆盖范围是标准的 Acronis：Windows、Linux 和 macOS 的物理机，以及主要的虚拟化平台，支持裸机恢复到不同的硬件。所有内容均通过一个 Web 控制台管理，Sharktech 运营一个 24/7 的内部支持团队 — 他们的备份页面强调真人电话支持，而非机器人 — 你的备份存储位于其高可用性、冗余的服务器基础设施之后。

## 购买前需检查的事项

有三点，因为它们会影响你实际支付的费用和服务的行为。

**首先，在结账时确认 Teams 工作负载许可。** Sharktech 的产品页面说明应用和数据库保护取决于工作负载支持和许可，且某些保护选项是单独定价的。记录的 $4 起价针对的是备份服务和存储；Microsoft 365 工作负载（Teams、Exchange、SharePoint、OneDrive）是包含在你的特定配置中还是作为额外项目，应在购物车中查看 — 或者在确认订单前通过支持团队确认。托管 Acronis 提供商根据许可层级打包 M365 工作负载的方式确实存在差异，因此这是在点击购买前值得进行两分钟聊天确认的一个问题。

**其次，不要指望退款窗口。** Sharktech 不宣传其 Acronis 服务的退款保证，且缺乏退款承诺是针对该公司的第三方评论中最常见的投诉。实际上，月付计划是你的低风险选项：支付 4 美元，运行一个月，看看恢复体验是否适合你，然后再做长期承诺。

**第三，注意 File Sync & Share 插件。** 它将备份目标变成 Dropbox 风格的共享驱动器，月付费率为每 GB 0.03 美元。如果你需要这是一个不错的附加功能，但请将其从订单中剔除，因为根据 Sharktech 的计费页面，它只在你选择时才收费。

## 常见问题

**Acronis 会备份 Teams 聊天消息吗？** 不会。Teams 聊天部分的消息 — 私人和群组聊天 — 不在 Acronis 的 Teams 备份范围内。频道对话也无法恢复，尽管你可以将它们导出为 HTML 文件。频道内容、文件、团队邮箱和会议已被覆盖。

**Teams 备份多久运行一次？** 默认每天一次，因为该操作是资源密集型的。你可以通过计划控制保留数据的时间长度，并在需要时触发手动运行。

**如果我删除了整个团队，我可以恢复它吗？** 是的 — Acronis 恢复整个团队，包括成员列表和团队结构，以及单个频道、文件、邮箱项、会议和团队站点。

**我需要运行自己的服务器来使用它吗？** 对于 Microsoft 365 数据，不需要。Teams 备份是通过 Web 控制台在 Acronis 云和你的 Microsoft 365 租户之间的云到云连接。对于服务器和虚拟机，代理通过同一个控制台管理。

## 针对你的情况的快速建议

如果你只需要 Microsoft 365 Teams 覆盖且没有其他 Sharktech 服务，请先仔细查看许可问题，并在确定前使用月付计划 — 4 美元加上按 GB 的超额费用使得第一个月是一个廉价的测试。如果你已经租用了 Sharktech 专用服务器或 VPS，将备份添加到同一家公司意味着你的系统和备份目标位于同一网络上，且有一个支持号码可以联系。如果你的保留占用空间舒适地保持在 200 GB 左右，年付提供的有效月费最低；如果它增长到几百 GB 以上，月付的超额费率将胜出。在该规模的另一端，Acronis 的直接每设备许可和大型企业 Veeam 部署对于单服务器运营商来说定价过高 — Sharktech 恰好填补了这一中端市场。👉 [Start with the 200 GB monthly plan and see your configured price](https://portal.sharktech.net/cart.php?a=add&pid=648&configoption%5B1862%5D=200&configoption%5B1863%5D=0&billingcycle=monthly&aff=1626)
