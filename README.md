# 法律检索 · Kimi WebBridge 改编版

本项目基于 [THUYRan/Legal-Skills-Chinese](https://github.com/THUYRan/Legal-Skills-Chinese) 中的 [`legal-article-retrieval`](https://github.com/THUYRan/Legal-Skills-Chinese/tree/main/skills/legal-article-retrieval) 技能改编。原有法律检索方法论来自上游；本仓库由 [Z-rrsss](https://github.com/Z-rrsss) 维护浏览器接入及本地版本的调整。

## 本版本的主要改动

- 接入 Kimi WebBridge，通过用户真实浏览器检索，沿用浏览器现有登录态。
- 使用浏览器作为默认检索通道，不要求配置北大法宝 MCP/API。
- 增加任务独立标签页、详情页弹窗与真实链接导航、跨域 iframe 和 OFD/PDF 正文识别规则。
- 增加环境检查、公开来源降级及无法核验时的明确标记。
- 调整报告结构、法规与案例表格、编号引用及脚注规则。

来源、比对版本和许可核验情况见 [UPSTREAM.md](./UPSTREAM.md)。上游当前未提供明确许可证，本仓库不自行添加 MIT 等开源许可声明。Kimi WebBridge 是独立工具，本仓库不包含其程序、浏览器扩展或 `kimi-webbridge` 技能包，需要另行安装。

## 浏览器接入

`legal-article-retrieval`（法律检索）不绑定具体数据库，**不需要也不使用 MCP**。检索通过 Kimi WebBridge 操作真实浏览器完成，沿用你浏览器里已登录的账号权限，不配置 API 密钥、不导出 Cookie。

> ⚠️ 无法在线核验的法条一律标注 `[待查]` 或“未取得原文核验”，不得凭模型记忆编造条文编号或内容。

## 运行环境

- Kimi WebBridge 浏览器扩展 + 本机守护进程（`http://127.0.0.1:10086`）。
- 守护进程未启动：运行 `~/.kimi-webbridge/bin/kimi-webbridge start` 后重试。
- 未安装：按官方帮助页安装（中文 https://www.kimi.com/zh-cn/features/webbridge ，英文 https://www.kimi.com/features/webbridge ），装好扩展、启动守护进程、确认扩展显示已连接后再开始检索。

## 工作方式

- 一个任务一个 session，首次导航新建本任务标签页；不接管、不导航、不关闭你原有的标签页，只清理本任务创建的标签页。
- 打开页面后先读快照或正文再引用；正文在跨域 iframe、OFD/PDF 阅读器或画布中读不到时，直接打开该 iframe 地址或改查发布机关的 HTML 正文；仍读不到就写“未取得原文核验”。
- 按你账号的权限检索：国家法律法规数据库（flk.npc.gov.cn）、中国人大网、中国政府网、最高人民法院及公报，以及北大法宝、威科先行等商业数据库。
- 不使用、不配置北大法宝 MCP/API，也不调用未授权的数据库接口。

## 降级

- 未安装 WebBridge：先按帮助页安装；或经你同意改用 AppleScript 驱动 Chrome、safaridriver 驱动 Safari。
- 都不可用：只用 `web_search`／`web_fetch` 读公开来源，并在报告中注明哪些材料因缺少登录态或工具而未取得原文。
- 内置浏览器没有你的账号权限，不能替代付费库检索；遇到验证码、双因素或登录失效，请手动完成后继续。

## 与其他文件的关系

方法论与报告格式见 [`SKILL.md`](./SKILL.md)；本文件只说明运行环境与接入方式。
