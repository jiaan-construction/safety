# JIA AN Crane Operator Safety Acknowledgement

JIA AN Construction Pte. Ltd. 塔吊司机线上安全须知与确认系统 V1.1。

## 正式网站 / Live website

**https://jiaan-construction.github.io/safety/**

请把上面的网页链接发给司机，或将该链接制作成二维码供司机扫码。不要直接发送 `index.html` 文件；WhatsApp 和微信通常无法直接预览 HTML 附件。

> 旧地址 `keepmind9697.github.io/jiaan-crane-safety/` 已改为跳转页，仅用于接住已发出的旧链接，不再维护。

## 系统用途

本网站用于让塔吊司机：

1. 阅读 JIA AN 公司级塔吊安全须知；
2. 逐节确认已经阅读并理解；
3. 填写姓名、联系电话及选填的 FIN / Work Permit；
4. **手写签名**，并输入姓名作为签署核对；
5. 记录自动提交到公司系统，同时在手机上生成带确认编号、确认时间和阅读记录的回执；
6. 将回执发回公司，作为司机自己的留底。

这是 Safety Acknowledgement（安全须知确认），不是免责协议，也不能替代培训、能力评估、项目安全交底、起重计划或总包现场规定。

## 司机使用方法

1. 用手机打开正式网站。
2. 点击 **Begin reading the safety document / 开始阅读安全文件**。
3. 填写姓名和联系电话；FIN / Work Permit 为选填。
4. 阅读全部安全章节，滑到每一节底部并完成确认。
5. **在签名框内用手指手写签名**，勾选最终声明，并输入与姓名栏一致的姓名完成签署。
6. 点击确认后，页面会显示提交结果，并生成 **Crane Operator Safety Acknowledgement Receipt / 塔吊司机安全须知确认回执**（回执上带手写签名）。
7. 点击 **Send receipt / 发送回执**，在手机分享菜单中选择 WhatsApp，把回执图片发给指定的 JIA AN 联系人或工作群。
8. 如手机不能直接分享，长按网页生成的回执图片保存，再从 WhatsApp 发送；也可使用页面内的邮件方式发至 `jiaanjason1360@gmail.com`。

## 公司使用方法

1. 把正式网站链接或二维码发给需要确认的司机。
2. 记录自动落库，在 Supabase 项目 `jiaan-safety` 查看：
   - **Table Editor → `safety_acknowledgements`**：全部确认记录
   - **Table Editor → `safety_ack_latest`**：每位司机最新一次确认（按电话去重）
   - **Storage → `signatures` → `ack/`**：按确认编号命名的手写签名图
3. 查人请按 **电话** 过滤，不要按姓名——工人重名情况普遍。
4. 文件升版、司机重新入职或公司要求重新确认时，重新发送网站链接并取得新记录。

## 数据与隐私（V1.1）

签署后，下列资料会提交到 JIA AN 在 **新加坡区（ap-southeast-1）** 的 Supabase 数据库：

姓名、联系电话、FIN / 工准证号、手写签名图、确认编号、文件编号与版本、签署时间、8 节确认状态、条款全文 SHA-256 哈希、阅读时长。

- 页面上已向司机作出收集告知（用途、存放地、查询与更正联系方式）。
- 页面只持有 Supabase 的 **publishable key**，数据库启用行级安全：该 key **只能新增记录，不能读取、修改或删除任何数据**；签名存储桶为私有，且只允许写入 `ack/<确认编号>.png` 这一种路径，已存在的签名无法覆盖。
- 提交失败（例如工地无信号）不会阻断回执：页面会明确显示「公司系统未收到」并提供重试，回执仍可正常发送。
- 不采集 IP、设备信息或其他个人资料。

## 当前边界（不要当成已完成）

- **没有公司后台界面**，查数据要登 Supabase 面板；没有按工地／按月的报表。
- **没有速率限制**。publishable key 是公开的，格式约束能挡住乱码，挡不住格式正确的伪造记录。
- **确认编号由手机签发**，是归档把手，不是防伪凭证。权威时间以服务器 `created_at` 为准，`signed_at` 来自手机时钟。
- **PDPA 保存年限尚未设定**；WSH / MOM / ETA 合规核查尚未完成。
- **Rev.01 尚未经公司最终批准放行**，页面上的生效日为 2026-09-01。
- Level 2 项目级（Site-specific）与 Level 3 每日操作前确认尚未制作。

## Repository files

- `index.html` — GitHub Pages 发布文件，单文件运行，无外部依赖、无第三方 CDN，唯一出站请求是本公司的 Supabase 项目。
- `README.md` — 网站入口、用法、数据与隐私说明、当前边界。
- `如何上线.md` — 静态托管与发布说明。

## Version

- System: V1.1（2026-08-21：手写签名 + 记录自动落库 + 收集告知）
- Document: `JAC-CR-SAF-001 Rev. 01`
- Publisher: JIA AN Construction Pte. Ltd.
