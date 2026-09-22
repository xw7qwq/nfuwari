# 关于

我是 [Lucius7](https://github.com/theLucius7)，喜欢算法、PT 站点和自托管。在这里记录题目复盘、工具改造，以及维护个人服务时遇到的问题。写博客，是为了把做过的题和踩过的坑整理成以后还能看懂的笔记。

## 兴趣与技术方向

我喜欢折腾自己会用到的东西：搭建算法训练环境、使用 OpenCD、维护邮件和数据看板，再把重复操作或不顺手的地方做成工具。PT 对我来说也是持续改进工具的动力——从账户状态同步，到容量管理和做种维护，都有具体的问题可以解决。

我的项目实践主要围绕 **后端开发、接口适配和自动化**，使用 Python、Go、JavaScript / TypeScript，也会改前端、接 API，并用 Linux、Docker Compose、Caddy 和 systemd 维护部署。我关心的不只是功能能否运行，还包括状态是否一致、失败后如何恢复，以及怎样验证一次修改。

## 我在做的项目

这些项目大多基于开源软件，结合自己的使用需求做定制。下面介绍的是我维护和改造的部分。

### 算法训练与评测：DMOJ

基于 DMOJ 搭建算法训练环境，处理赛事题库导入、不同来源的 checker 适配，以及同进度排名和受限附件访问。为接入 Windows 特殊判题程序，也折腾过 Wine、Unix socket 与独立容器的组合。这些实践把刷题之外的数据整理、后端逻辑和部署问题串了起来。

### PT、OpenCD 与做种维护

我喜欢玩 PT 站，目前使用 OpenCD。围绕日常做种和资源管理，对 PT Tools 与 qBittorrent 的配套流程做了定制：让后台账户刷新不依赖浏览器，在添加任务前重新检查实际大小与容量，并用 Python 守护检查任务完成情况、文件是否存在，以及 tracker 的确认状态。

这类改造也让我更关注并发任务、状态同步和异常处理。我会把关键判断拆成可以用 mock API 测试的逻辑，让工具的行为更容易检查和维护。

### 网络服务门户：NeXus

基于 EZ-Theme、Xboard 等开源项目改造个人网络服务门户，涉及 Vue 页面、Go 同源中间层、流量统计和客户端配置兼容。前端实践包括按需加载、合并进行中的读取请求，以及处理登录状态变化后的异步响应。

### 邮件与认证：Bulwark / Stalwart

围绕多域邮件使用，定制归档规则、文件夹维护和 Passkey 登录接入。这部分主要接触 JMAP、Sieve、WebAuthn 和 TypeScript，也会考虑撤销凭据、状态变化或请求失败时该怎样处理。

### 数据同步与展示：Fitbaus

在既有 Fitbit 看板上扩展缓存、日周月汇总、定时同步、中文界面和 JSON API / SVG 输出。我喜欢这种从数据整理到界面展示的完整过程，也会关注重复同步、缓存失效和管理操作的权限边界。

## 支撑这个博客的项目

本站的源码和配套项目放在 [xw7qwq](https://github.com/xw7qwq) 组织中：文章、代码、刷题记录与设备状态各有自己的来源，在博客里汇合。

| 项目 | 负责什么 | 与本站的关系 |
| --- | --- | --- |
| [nfuwari](https://github.com/xw7qwq/nfuwari) | 基于 Astro / Fuwari 的博客 | 保存文章、生成页面，接入下方介绍的公开 API |
| [MacFlare](https://github.com/xw7qwq/macflare) | 采集并发布 Mac 的应用与音乐状态 | 为顶部导航提供应用图标和歌曲封面 |
| [OJFlare](https://github.com/xw7qwq/ojflare) | 汇总多平台提交、比赛进度与 Rating | 为左侧最近提交和本页 AC 贡献图提供数据 |
| [CodeFlare](https://github.com/xw7qwq/codeflare) | 整理算法源码、模板与提交归档 | 提供独立的代码检索和源码阅读页面，作为题解与复盘的参考 |
| [.github](https://github.com/xw7qwq/.github) | 组织介绍、贡献指南与协作约定 | 统一各仓库的维护方式 |

## 一篇文章如何上线

文章以 Markdown 保存在 nfuwari 中，中文和英文分别维护。写作时先用草稿状态在本地预览，准备好后提交到 GitHub，通过检查并合入 `main`，由 GitHub Actions 构建和发布。

**Markdown → Astro 构建 → GitHub Pages → 阿里云 ESA → 你的浏览器**

Astro 负责把文章和页面生成静态文件，Fuwari 提供博客主题；数学公式由 KaTeX 渲染，Pagefind 在构建时生成搜索索引。GitHub Pages 托管构建结果，阿里云 ESA 为 `blog.lucius7.cn` 提供边缘分发和 HTTPS。阅读文章时，浏览器直接加载这些已生成的页面。

具体写作和部署方法记录在仓库的[写作指南](https://github.com/xw7qwq/nfuwari/blob/main/docs/WRITING.md)与[部署指南](https://github.com/xw7qwq/nfuwari/blob/main/docs/DEPLOYMENT.md)中。

## 网站如何选择中文或英文

**语言由网址前缀决定，默认语言是中文。** 当前没有按浏览器语言或 IP 自动选择语言，也不会保存上次的语言选择。

| 访问地址 | 打开的内容 |
| --- | --- |
| `blog.lucius7.cn/` | 固定跳转到中文首页 `/zh/` |
| [/zh/](/zh/) | 中文界面、中文文章与中文搜索结果 |
| [/en/](/en/) | 英文界面、英文文章与英文搜索结果 |

顶部的「中文 / EN」按钮会根据当前页面选择目标：

- **首页、关于、归档**：打开另一种语言的对应页面。例如 `/zh/about/` 切换到 `/en/about/`。
- **文章页**：有已发布的对应译文时打开译文；没有译文时，进入目标语言的首页。文章正文和译文分别撰写。
- **分页与筛选**：跨语言切换会回到目标首页或归档页，不保留当前页码、分类或标签筛选。

切换语言会完整加载目标页面，让菜单、侧栏和搜索一同更新。再次打开不带语言前缀的根网址，仍会进入中文；想直接进入英文，可以收藏 [/en/](/en/)。旧的 `/about/` 和 `/archive/` 入口也分别跳到中文的关于页和归档页。

## 页面里的动态信息从哪里来

### 应用与音乐：MacFlare

Mac 上的原生采集程序记录应用和 Apple Music 状态，经认证上传到 Cloudflare Worker，由 Workers KV 保存状态。博客在浏览器中读取公开的 [`/api/now`](https://macflare.lucius7.dev/api/now) 和 [`/api/icons`](https://macflare.lucius7.dev/api/icons)，在标题旁显示应用图标；音乐播放时显示歌曲封面。悬停、聚焦或点击图标可以查看名称。

这里显示的是最近公开的状态快照。图标随接口更新，状态过期或不可用时会隐藏。服务的 API 与接入文档见 [MacFlare](https://macflare.lucius7.dev/)。

### 最近提交与 AC 贡献图：OJFlare

OJFlare 的同步任务从 Codeforces、AtCoder、QOJ 和牛客整理练习记录，生成公开的 [`dashboard.json`](https://ojflare.lucius7.dev/data/dashboard.json)。博客读取这份数据，呈现两种视图：

- **左侧最近提交**：按提交时间展示最近三条 Codeforces / AtCoder 的 AC 记录，点击直达原平台提交页。同一题的多次 AC 可以分别出现。
- **本页 AC 贡献图**：按 UTC+8 统计已收集记录中每天首次 AC 的题目数。同一题只在最早记录的通过日期计入，支持按年份和平台筛选。

这两个区域共享一次数据请求，并在页面可见时定期刷新。数据新鲜度取决于 OJFlare 的同步与发布；实现细节见其 [API 文档](https://github.com/xw7qwq/ojflare/blob/main/docs/API.md)。这些公开接口在页面加载后读取，因此文章的构建与阅读不依赖状态接口当时是否在线。

### 从提交记录到源码：CodeFlare

[CodeFlare](https://codeflare.lucius7.dev/) 按平台和目录展示代码，支持搜索和在线阅读。它的归档工具可以利用 OJFlare 的题目、比赛与 AC 元数据辅助整理，再从可获取的来源补充提交信息和源码。

源码归档与 AC 统计分别维护：仓库也会保存模板、未完成代码和未通过的尝试，不能用文件数量代表通过题数。博客中的分析由我撰写，当前通过链接与代码归档配合使用；本站直接接入的数据 API 来自 MacFlare 和 OJFlare。

## 联系我

欢迎通过 [GitHub](https://github.com/theLucius7)、[B 站](https://space.bilibili.com/1814052279)、[X](https://x.com/theLucius7) 或 [i@lucius7.dev](mailto:i@lucius7.dev) 交流。网站与项目的问题，也可以提交到对应仓库的 Issues。
