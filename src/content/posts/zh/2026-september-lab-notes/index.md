---
title: "2026 年阶段记录：算法训练、自建服务与开源贡献"
published: 2026-09-22
description: '记录 2026 年 1 月 1 日至 9 月 22 日的算法训练、比赛与开源贡献，以及自建服务的维护现状。'
image: ''
tags: [个人记录, 算法竞赛, 自建服务, 开源, VPS]
category: '折腾记录'
draft: false
lang: zh_CN
---

从 2026 年 1 月 1 日到 9 月 22 日，我主要在做三件事：练算法、维护自己的服务，以及把使用开源项目时做的修改提交回上游。

这篇文章把今年的提交记录、比赛表现和代码放在一起，回顾算法训练的进展与不足，也记录这段时间的开源贡献、比赛成绩，以及目前维护的服务。

## 今年的算法训练

### 做题量与比赛成绩

今年在 Codeforces 和 AtCoder 上合计新增通过 **472 道题**。这里按每道题在账号记录中的首次 AC 计数，重复提交和往年已经通过的题目不重复计算。

| 平台 | 今年新增通过 | 今年计分赛 | 年初 Rating → 当前 | 变化 |
| --- | ---: | ---: | ---: | ---: |
| [Codeforces](https://codeforces.com/profile/Lucius7) | 246 题 | 6 场 | 1718 → 1617 | −101 |
| [AtCoder Algorithm](https://atcoder.jp/users/Lucius7) | 226 题 | 27 场 | 1083 → 1463 | +380 |

过题数据来自 [OJFlare](https://ojflare.lucius7.dev/) 的 9 月 21 日 12:59（UTC+8）快照；计分赛与 Rating 按 9 月 22 日的 [Codeforces 官方记录](https://codeforces.com/contests/with/Lucius7)和 [AtCoder 官方记录](https://atcoder.jp/users/Lucius7/history)统计。

这两组数字回答的是不同的问题。过题记录包含练习和补题，不能直接说明能否在比赛中独立完成；Rating 则反映限时比赛的结果，两站分数也不能直接换算。目前 Codeforces 为 Expert，AtCoder 为水色。今年的变化更值得关注：AtCoder 有明显提升，Codeforces 的比赛成绩还没有跟上练习中的积累。

### 从代码里看训练内容

今年新增通过的 Codeforces 题目中，142 道有官方难度评分，其中 **26 道在 2000 分及以上**；其余 104 道没有评分，不把它们当作低分题。结合 [CodeFlare](https://codeflare.lucius7.dev/) 中的具体实现，图论模型的组合是这一阶段比较集中的积累。

| 代码样本 | 实现中的关键处理 |
| --- | --- |
| [CF160D · 2300](https://codeflare.lucius7.dev/code.html?path=Codeforces/160/D.cpp) | 按边权分组做 Kruskal，用并查集合并更小权值的连通块，在同权边构成的图上找桥，再判断边在最小生成树中的地位。整组判定后才合并，避免同权边互相干扰。 |
| [CF1215F · 2700](https://codeflare.lucius7.dev/code.html?path=Codeforces/1215/F.cpp) | 用 2-SAT 同时表示站点选择和有序阈值，把区间限制、互斥关系与阈值单调性转成蕴含边，再通过强连通分量求解。 |
| [CF241E · 2600](https://codeflare.lucius7.dev/code.html?path=Codeforces/241/E.cpp) | 先筛出起点到终点路径涉及的点，再建立差分约束，通过势能差构造边权。建模前的范围筛选和后续约束求解需要配合。 |
| [ABC476E](https://codeflare.lucius7.dev/code.html?path=AtCoder/abc476/e.cpp) | 结合线段树的区间极值与按值组织的位置集合，定位需要交换的位置，并同步更新数组、线段树和集合。 |
| [ABC445F](https://codeflare.lucius7.dev/code.html?path=AtCoder/abc445/f.cpp)、[ABC471E](https://codeflare.lucius7.dev/code.html?path=AtCoder/abc471/e.cpp) | 前者用 min-plus 矩阵快速幂加速最小代价转移；后者展开子集元素和的平方，按单个元素与元素对计算组合贡献。 |
| [ABC476F](https://codeflare.lucius7.dev/code.html?path=AtCoder/abc476/f.cpp) | 用 `i+j`、`i-j` 变换坐标，按对角线聚合权重，再用前后缀和计算加权距离，减少重复枚举。 |

这些样本都在今年首次通过。它们说明训练已经涉及“如何把条件转成模型，再把多个算法或数据结构接起来”，也覆盖了 DP、计数和代数化简。不过，完成一份专题练习或补题代码，与在没有标签提示的比赛中及时识别模型，仍然是两件需要分别训练的事。

### 限时比赛中的表现

Codeforces 今年的 6 场计分赛都完成了 A、B、C，其中一场进一步通过 D，另一场通过 D1。这个结果说明前半场有一定基础，但中段题的突破还不稳定，前面的题也会因错误提交损失时间。

[Round 1111](https://codeforces.com/contest/2247) 是一个具体例子：D1 在约 92 分钟时通过，随后 D2 在最后约 17 分钟内连续提交了 10 次，均为 TLE。对于这种情况，复盘需要回到操作次数上界和重复计算上，判断是否应该调整算法或数据结构。比赛最后才反复尝试，很难留出重新建模的时间。相关记录：[D1 的 AC](https://codeforces.com/contest/2247/submission/383361672)、[D2 的首次 TLE](https://codeforces.com/contest/2247/submission/383365598)与[最后一次 TLE](https://codeforces.com/contest/2247/submission/383373107)。

Codeforces 最近一次计分赛停在 7 月 18 日，所以 1617 还不能充分反映 8、9 月练习后的状态。要判断后续训练是否有效，需要再用完整的限时比赛检验。

AtCoder 今年从 1083 升到 1463，最高到过 1475。最近参加的 8 场 ABC 中，6 场完成 5 题，2 场完成 4 题；这 8 场都完成了 A 到 D，其中 ABC467、ABC469 是跳过 E 做出 F。按题目特点调整顺序已经能带来收益，但更高难度题目的持续输出还需要积累。

7 月的 [ABC467](https://atcoder.jp/contests/abc467/standings?watching=Lucius7) 取得了 2049 的单场 Performance；最近 6 场计分赛的 Performance 则在 1414–1512 之间。全年有进步，近期也进入了需要继续突破的阶段，不能把最好的一场当作稳定水平。

最近的 ABC476 中，E 在开赛约 46 分钟时通过，F 则在次日补出。这道 F 的坐标变换和距离贡献处理已经进入代码积累，但尚不能计为赛时六题。把[赛中提交](https://atcoder.jp/contests/abc476/submissions/79373498)和[赛后补题](https://atcoder.jp/contests/abc476/submissions/79396187)分开看，更容易找到下一步要改进的环节。

### 下一阶段的训练方向

根据今年的代码和比赛记录，接下来我想把重点放在三件事上：

1. **增加不看标签的限时混合训练。** 以 Codeforces 1700–2000 分题、ABC E/F 和部分 ARC 题为主要候选，按实际难度选题，练习从条件中识别模型。每次记录建模耗时、首交结果，以及是否借助提示。
2. **把复杂度与实现检查前移。** 提交前明确状态数、每次操作的代价和总操作次数；遇到 TLE 时先重新估算上界。多种结构共同维护状态的题，可以写小规模直接模拟来对照；调用模板前检查平行边、边界下标和整数范围。
3. **持续参加完整比赛并复盘下一道题。** 用计分赛或完整虚拟赛检验专题训练能否迁移，区分赛时独立完成、赛后独立补出和参考题解后的实现。保留图论专题训练，同时继续覆盖 DP、计数与构造，避免只在熟悉的题型里练习。

## 博客与代码记录

我把这组项目放在 [xw7qwq](https://github.com/xw7qwq) 组织下，各自负责一部分内容：

| 项目 | 作用 |
| --- | --- |
| [nfuwari](https://github.com/xw7qwq/nfuwari) | 博客本体，基于 Astro 和 Fuwari，保存文章与学习笔记 |
| [OJFlare](https://github.com/xw7qwq/ojflare) | 汇总多平台 AC、比赛和 Rating 记录，为最近提交与贡献图提供数据 |
| [CodeFlare](https://github.com/xw7qwq/codeflare) | 归档算法源码和模板，提供独立的代码检索、阅读入口 |
| [MacFlare](https://github.com/xw7qwq/macflare) | 提供 Mac 上的应用和音乐状态，在博客顶部展示应用图标与歌曲信息 |
| [.github](https://github.com/xw7qwq/.github) | 组织介绍、贡献说明和维护约定 |

博客文章用 Markdown 编写，经 Astro 构建后发布到 GitHub Pages，域名通过阿里云 ESA 分发。刷题记录和应用状态由浏览器向各自的公开 API 请求，CodeFlare 则作为独立的源码站点供文章引用。完整的网站结构可以在[关于页面](/zh/about/)查看。

OJFlare 的贡献图按 UTC+8 统计每道题的首次 AC；CodeFlare 保存的内容更广，还包括模板、尝试和未完成的代码。前者记录做题进度，后者留下推导和实现，两者配合起来，比较适合用来复盘。

## VPS 上的个人工具

截至 2026 年 9 月 22 日，我的 VPS 上运行着 19 组 Docker Compose 项目、34 个容器，另有一些由 systemd 或独立进程管理的服务。从评测、邮件到笔记和监控，日常会用到的工具逐渐聚到了一起。

这些服务大多基于已有开源项目。我做的事情主要是部署、配置，以及围绕自己的使用需求修改接口和界面。

平时也会在 NodeSeek、LINUX DO 逛逛，看社区里的讨论。

### DMOJ：从提交代码到维护评测环境

和算法训练关系最紧密的是 [DMOJ](https://github.com/DMOJ/site)。这套部署包含网页、后台任务、通信桥、评测机、数据库和缓存，另有 PDF 服务与 HDU 特殊评测适配服务。

一次代码提交会经过网页接收、任务分发、编译运行和结果回传。平时在 OJ 上看到的提交状态、时间限制和比赛排名，到了自己的环境里，都成了需要配置和维护的具体环节。

我在这套部署中做了比赛计分、排名可见性和提交界面等适配，也接入了 HDU SPJ。题目迁移时，输入输出约定、checker 行为、编译环境和评分规则需要一起考虑。维护评测环境，让平时做题时接触到的规则有了更具体的实现。

### 邮箱：Stalwart 与 Bulwark

邮件服务端使用 Stalwart，网页客户端使用 [Bulwark Webmail](https://github.com/bulwarkmail/webmail)。我的部署包含按域名组织文件夹、JMAP 交互和 Passkey 登录相关的本地适配。

邮件客户端的工作涉及一整套状态：界面上的文件夹如何对应到服务端，登录状态怎样延续到后续请求，操作失败后又该如何提示。这些改动需要把界面、认证和协议放在一起考虑。

### 数据看板、笔记与信息获取

FitBaus 提供 Fitbit 数据看板和只读 API；Fast Note Sync 与 Obsidian 插件配合，同步笔记和附件。RSSHub、OpenList、TaoSync 等工具则承担信息获取、文件入口与同步工作。

这些服务处理的数据不同，维护时却经常遇到相似的问题：更新什么时候发生，失败后如何重试，旧数据是否仍然可用，以及怎样知道上一次成功同步的时间。它们也让我把注意力从单个页面，延伸到数据更新和多端状态上。

### 多人同步与接口适配

[DreamStream99](https://github.com/ypnomania/DreamStream99) 把 Win98 风格的静态前端与房间同步、媒体处理服务分开。多人一起观看视频时，播放、暂停、跳转和重新加入房间都需要同步，还要处理房主权限和重复操作。

NeXus / Xboard 这一组服务则包含前端、同源中间层和既有后端。中间层把浏览器操作映射到后端接口；前端根据接口实际提供的能力展示功能。这与我在 EZ-Theme 中做的兼容工作有直接联系。

### 配套服务与日常维护

其余工具主要负责入口、监控、通知和后台任务：

| 用途 | 项目或组件 |
| --- | --- |
| 反向代理与访问入口 | Caddy、Cerberus |
| 资源监控 | Komari、Beszel 及对应 Agent |
| 运维入口 | Nexterm |
| 消息通知 | Apprise |
| 订阅、文件与搜索 | RSSHub、Browserless、OpenList、Meilisearch、TaoSync |
| 日常管理与后台任务 | Wallos、qBittorrent、PT Tools（主要配合 OpenCD 使用）、seed guard |
| 课程信息与工作流实验 | yuketang-cloud |
| 进程与部署管理 | systemd、Supervisor、Docker Compose |

服务部署之后，维护还会继续：处理异常、跟进上游更新、保存本地修改，以及整理升级和恢复步骤。容器的运行状态只是其中一部分，实际功能仍需要从使用过程去检查。

## 提交回上游的改动

我的 GitHub 账号是 [theLucius7](https://github.com/theLucius7)。除了维护自己的项目，我也会把使用开源软件时遇到的问题整理成 PR。

### QQ Chat Exporter

[QQ Chat Exporter #675](https://github.com/shuakami/qq-chat-exporter/pull/675) 处理的是 WebSocket 认证。网页通过 HTTP 完成认证之后，实时进度和流式搜索使用的 WebSocket 也需要携带访问令牌，重新连接时同样如此；HTTPS 入口则需要对应的 `wss` 连接。

随后提交的 [#677](https://github.com/shuakami/qq-chat-exporter/pull/677) 在 **2026 年 9 月 6 日** 合并，把实验性的私聊漫游查询接入了现有导出流程。

用户可以从已有私聊会话进入，也可以先通过 QQ 号查找对应的 `peerUid`。选定日期范围后，服务端创建任务、查找消息锚点并查询记录，再复用现有的消息解析、资源处理和格式导出能力。任务页提供进度、取消和下载入口。

这部分工作除了查询本身，还涉及任务排队、并发控制、取消和状态恢复。查询有日期跨度、消息数量和执行预算等限制；结果中保留不完整标记与停止原因，说明这次任务实际完成了什么。它仍是依赖已登录 QQ 和桥接能力的实验性私聊功能，不能保证恢复全部云端历史。

### 其他贡献

| 合并日期（UTC） | 项目与 PR | 内容 |
| --- | --- | --- |
| 2026-09-21 | [Daily_CF_Problems #15809](https://github.com/Yawn-Sean/Daily_CF_Problems/pull/15809) | 一份个人 C++ 题解 |
| 2026-09-06 | [QQ Chat Exporter #677](https://github.com/shuakami/qq-chat-exporter/pull/677) | 实验性私聊漫游查询与导出任务 |
| 2026-09-02 | [QQ Chat Exporter #675](https://github.com/shuakami/qq-chat-exporter/pull/675) | WebSocket 连接和重连时的认证 |
| 2026-08-18 | [DreamStream99 #1](https://github.com/ypnomania/DreamStream99/pull/1) | 服务端房间创建、房主与访客权限、播放操作去重和 YouTube 同步改进 |
| 2026-07-27 | [EZ-Theme #45](https://github.com/PangHu-Code/EZ-Theme/pull/45) | Xboard 礼品卡接口、会话字段与时间格式兼容、撤销会话和自动续费展示 |

Daily_CF_Problems 是另一种持续参与开源的方式：把日常做题留下的解法整理好，提交到共同维护的题解仓库。[已合并的题解 PR](https://github.com/Yawn-Sean/Daily_CF_Problems/pulls?q=is%3Apr+is%3Amerged+author%3AtheLucius7) 也记录了这部分积累。

## 比赛与获奖

今年截至 9 月 22 日的比赛记录包括 **4 项金奖、4 项银奖、3 项铜奖**，共 11 个赛事阶段。团队赛的成绩也属于一起参赛的队友。

| 比赛日期 | 赛事 | 获奖 |
| --- | --- | --- |
| 2026-09-13 | 2026–2027 ICPC 贵州省赛 | 银奖，总榜第 10 名 |
| 2026-08-21 | 第八届码蹄杯 · 本科院校赛道国赛 | 金奖 |
| 2026-08-21 | 第 22 届百度之星 · 人才专项赛道决赛 | 金奖 |
| 2026-07-29 | ICPC 沈阳全国邀请赛 | 铜奖 |
| 2026-06-14 | 第十四届重庆市大学生程序设计大赛 | 银奖 |
| 2026-05-31 | 第十八届四川省大学生程序设计大赛 | 银奖 |
| 2026-05-30 | CCPC 全国邀请赛（福州） | 银奖 |
| 2026-05-24 | CCPC 全国邀请赛（秦皇岛） | 铜奖 |
| 2026-05-14 | 第八届码蹄杯 · 本科院校赛道四川省赛 | 金奖 |
| 2026-05-14 | 第 22 届百度之星 · 人才专项赛道省赛 | 金奖 |
| 2026-05-02 | ICPC 陕西全国邀请赛（西安） | 铜奖 |

### 证书

<details>
<summary>ICPC 贵州省赛（2026–2027 赛季） · 银奖 · 总榜第 10 名</summary>

The 2026-2027 ICPC China Guizhou Provincial Programming Contest。比赛日期：2026-09-13。

![ICPC 贵州省赛（2026–2027 赛季） · 银奖 · 总榜第 10 名，本人证书](./assets/2026-icpc-guizhou-provincial.webp)

</details>

<details>
<summary>码蹄杯 · 国赛 · 金奖</summary>

2026 年第八届码蹄杯程序设计大赛本科院校赛道国赛。比赛日期：2026-08-21。

![码蹄杯 · 国赛 · 金奖，本人证书](./assets/2026-matibei-undergraduate-national.webp)

</details>

<details>
<summary>百度之星 · 决赛 · 金奖</summary>

第 22 届百度之星程序设计大赛决赛（人才专项赛道）。比赛日期：2026-08-21。

![百度之星 · 决赛 · 金奖，本人证书](./assets/2026-baidu-star-talent-final.webp)

</details>

<details>
<summary>ICPC 沈阳邀请赛 · 铜奖</summary>

2026 ICPC China Shenyang National Invitational Programming Contest。比赛日期：2026-07-29。

![ICPC 沈阳邀请赛 · 铜奖，本人证书](./assets/2026-icpc-shenyang-invitational.webp)

</details>

<details>
<summary>重庆市大学生程序设计大赛 · 银奖</summary>

2026 年重庆市第十四届大学生程序设计大赛。比赛日期：2026-06-14。

![重庆市大学生程序设计大赛 · 银奖，团队证书](./assets/2026-chongqing-cpc.webp)

</details>

<details>
<summary>四川省大学生程序设计大赛 · 银奖</summary>

第十八届四川省大学生程序设计大赛。比赛日期：2026-05-31。

![四川省大学生程序设计大赛 · 银奖，本人证书](./assets/2026-sichuan-cpc.webp)

</details>

<details>
<summary>CCPC 福州邀请赛 · 银奖</summary>

2026 年中国大学生程序设计竞赛—全国邀请赛（福州）。比赛日期：2026-05-30。

![CCPC 福州邀请赛 · 银奖，团队证书](./assets/2026-ccpc-fuzhou-invitational.webp)

</details>

<details>
<summary>CCPC 秦皇岛邀请赛 · 铜奖</summary>

2026 年中国大学生程序设计竞赛全国邀请赛（秦皇岛）。比赛日期：2026-05-24。

![CCPC 秦皇岛邀请赛 · 铜奖，团队证书](./assets/2026-ccpc-qinhuangdao-invitational.webp)

</details>

<details>
<summary>码蹄杯 · 四川省赛 · 金奖</summary>

2026 年第八届码蹄杯程序设计大赛本科院校赛道四川赛区省赛。比赛日期：2026-05-14。

![码蹄杯 · 四川省赛 · 金奖，本人证书](./assets/2026-matibei-undergraduate-sichuan-provincial.webp)

</details>

<details>
<summary>百度之星 · 省赛 · 金奖</summary>

第 22 届百度之星程序设计大赛省赛（人才专项赛道）。比赛日期：2026-05-14。

![百度之星 · 省赛 · 金奖，本人证书](./assets/2026-baidu-star-talent-provincial.webp)

</details>

<details>
<summary>ICPC 陕西邀请赛（西安） · 铜奖</summary>

2026 ICPC China Shaanxi National Invitational Programming Contest。比赛日期：2026-05-02。

![ICPC 陕西邀请赛（西安） · 铜奖，本人证书](./assets/2026-icpc-shaanxi-invitational.webp)

</details>

## 接下来

算法训练上，我想让今年积累的模型和实现更稳定地转化为赛时结果。服务维护上，继续整理升级、备份与恢复步骤，把值得展开的部署和适配过程写下来；遇到适合独立提交的改动，就继续整理成 PR。

这份记录止于 2026 年 9 月 22 日。后续的训练、比赛和项目进展，再通过新的记录继续补充。
