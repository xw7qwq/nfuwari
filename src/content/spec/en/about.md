# About

I'm [Lucius7](https://github.com/theLucius7). I enjoy algorithms, private trackers, and self-hosting. I write about problems I've solved, tools I've customized, and lessons from maintaining my own services. These notes help me return to an idea and understand how I reached it.

## Interests and technical focus

I like improving the tools I use for algorithm practice, OpenCD, email, and data dashboards. Repetitive tasks and rough edges often turn into small tools. Using private trackers also gives me practical reasons to improve account synchronization, capacity management, and seeding maintenance.

My projects focus on **backend development, API integration, and automation**, using Python, Go, and JavaScript / TypeScript. I also customize frontends and maintain deployments with Linux, Docker Compose, Caddy, and systemd. I care about consistent state, recovery from failures, and checking that a change does what it is supposed to do.

## Projects I work on

Most of these projects build on open-source software, adapted to my own needs. The descriptions below focus on the parts I maintain and customize.

### Algorithm practice and judging: DMOJ

I use DMOJ as the foundation for an algorithm practice environment, working on contest imports, checker compatibility, rankings at equal elapsed contest time, and access to restricted attachments. Integrating Windows special judges has also involved Wine, Unix sockets, and a separate container. This connects algorithm practice with data preparation, backend logic, and deployment work.

### Private trackers, OpenCD, and seeding maintenance

I enjoy using private trackers (PT), and currently use OpenCD. For everyday seeding and resource management, I have customized workflows around PT Tools and qBittorrent: refreshing account information without an open browser, rechecking actual size and capacity before admitting tasks, and using a Python guard to check task completion, file availability, and tracker acknowledgement.

These changes have led me to spend more time on concurrent tasks, state synchronization, and failure handling. I separate key decisions into logic that can be tested with mock APIs, making the tools easier to inspect and maintain.

### Network service portal: NeXus

I customize a personal network service portal based on open-source projects including EZ-Theme and Xboard. The work spans Vue pages, a Go same-origin backend, traffic statistics, and client configuration compatibility. Frontend changes include lazy loading, sharing in-flight read requests, and handling asynchronous responses after login state changes.

### Email and authentication: Bulwark / Stalwart

For email across multiple domains, I customize filing rules, folder maintenance, and Passkey login integration. This involves JMAP, Sieve, WebAuthn, and TypeScript, with attention to credential revocation, changing state, and failed requests.

### Data synchronization and presentation: Fitbaus

I extend an existing Fitbit dashboard with caching, daily/weekly/monthly summaries, scheduled synchronization, a Chinese interface, and JSON API / SVG output. I enjoy connecting data preparation to a usable interface, including the details of overlapping sync jobs, cache invalidation, and access controls for administrative actions.

## Projects behind this blog

The blog and its supporting projects live in the [xw7qwq](https://github.com/xw7qwq) organization. Articles, source code, solving history, and device activity have their own sources and meet here on the blog.

| Project | Purpose | Role on this site |
| --- | --- | --- |
| [nfuwari](https://github.com/xw7qwq/nfuwari) | An Astro / Fuwari blog | Stores articles, builds pages, and integrates the public APIs described below |
| [MacFlare](https://github.com/xw7qwq/macflare) | Publishes Mac application and music activity | Supplies the app icon and track artwork in the top navigation |
| [OJFlare](https://github.com/xw7qwq/ojflare) | Collects submissions, contest progress, and ratings | Supplies recent submissions and this page's AC contribution calendar |
| [CodeFlare](https://github.com/xw7qwq/codeflare) | Archives solutions, templates, and submission records | Provides a separate searchable source browser for reference when writing and reviewing solutions |
| [.github](https://github.com/xw7qwq/.github) | Organization profile and shared guidelines | Documents how the repositories are maintained |

## How an article reaches you

Articles are Markdown files in nfuwari, with separate Chinese and English content. I preview drafts locally, submit the changes to GitHub, and merge them into `main` after checks pass. GitHub Actions then builds and publishes the site.

**Markdown → Astro build → GitHub Pages → Alibaba Cloud ESA → your browser**

Astro generates static pages, and Fuwari provides the blog theme. KaTeX renders mathematics; Pagefind builds the search index. GitHub Pages hosts the generated files, while Alibaba Cloud ESA provides edge delivery and HTTPS for `blog.lucius7.cn`. Reading an article loads an already-built page.

The repository's [writing guide](https://github.com/xw7qwq/nfuwari/blob/main/docs/WRITING.md) and [deployment guide](https://github.com/xw7qwq/nfuwari/blob/main/docs/DEPLOYMENT.md) explain the workflow.

## How the site chooses Chinese or English

**The URL prefix determines the language, with Chinese as the default.** The site does not automatically choose a language based on your browser or IP address, and it does not remember your previous language selection.

| Address | What opens |
| --- | --- |
| `blog.lucius7.cn/` | Always redirects to the Chinese home page, `/zh/` |
| [/zh/](/zh/) | Chinese interface, articles, and search results |
| [/en/](/en/) | English interface, articles, and search results |

The **中文 / EN** buttons in the top navigation choose a destination based on the current page:

- **Home, About, and archive:** open the equivalent page in the other language. For example, `/zh/about/` switches to `/en/about/`.
- **Articles:** open the corresponding published translation when available; otherwise, open the target language's home page. Articles and translations are written separately.
- **Pagination and filters:** switching languages returns to the target home or archive page without carrying over page numbers, categories, or tag filters.

A language switch fully loads the destination page so that menus, sidebars, and search update together. Opening the root URL again still takes you to Chinese. Bookmark [/en/](/en/) to enter the English site directly. The legacy `/about/` and `/archive/` entry points also redirect to their Chinese counterparts.

## Where the changing information comes from

### Applications and music: MacFlare

A native collector on my Mac records application and Apple Music activity. It sends authenticated updates to a Cloudflare Worker, with state stored in Workers KV. The blog reads the public [`/api/now`](https://macflare.lucius7.dev/api/now) and [`/api/icons`](https://macflare.lucius7.dev/api/icons) endpoints in your browser. An app icon appears beside the site title, along with track artwork when music is playing. Hover, focus, or tap an icon to see its name.

These are the most recently published activity snapshots. The icons update from the API and disappear when the state expires or becomes unavailable. API and integration documentation is available at [MacFlare](https://macflare.lucius7.dev/).

### Recent submissions and AC contributions: OJFlare

OJFlare sync jobs collect solving records from Codeforces, AtCoder, QOJ, and Nowcoder, then publish [`dashboard.json`](https://ojflare.lucius7.dev/data/dashboard.json). The blog presents two views of that data:

- **Recent submissions in the sidebar** show the latest three accepted Codeforces / AtCoder submissions, with direct links to the original submission pages. Repeat ACs on the same problem can appear separately.
- **The AC contribution calendar below** counts each problem on its earliest recorded AC date in UTC+8, based on the collected history. Each problem counts only once. You can filter by year and platform.

Both widgets share a data request and refresh periodically while the page is visible. Freshness depends on OJFlare's sync and publication schedule; see its [API documentation](https://github.com/xw7qwq/ojflare/blob/main/docs/API.md). The public APIs are read after the page loads, so building and reading articles does not depend on those services being available at that moment.

### From submission records to source code: CodeFlare

[CodeFlare](https://codeflare.lucius7.dev/) organizes code by platform and directory, with search and an online source reader. Its archive tools can use OJFlare's problem, contest, and AC metadata to help organize imports, then supplement submission records and source code from available sources.

Source archives and AC statistics are maintained separately. The archive also includes templates, unfinished code, and unsuccessful attempts, so its file count is not a solved-problem count. I write the blog's explanations myself and use links to connect them with the code archive. The data APIs directly integrated into this site currently come from MacFlare and OJFlare.

## Get in touch

You can find me on [GitHub](https://github.com/theLucius7), [Bilibili](https://space.bilibili.com/1814052279), and [X](https://x.com/theLucius7), or email [i@lucius7.dev](mailto:i@lucius7.dev). For website or project issues, please use the relevant repository's Issues page.
