# Waves Ye · Personal Website

一个持续更新的个人空间，用来记录研究兴趣、进行中的项目、学习笔记和文章。原生 HTML + CSS，无框架、无依赖、无构建步骤，也不需要 JavaScript。

仓库：[wavesye/PersonalWebsite](https://github.com/wavesye/PersonalWebsite)

GitHub Pages 开启并部署成功后的地址：**https://wavesye.github.io/PersonalWebsite/**

## 文件结构

```text
PersonalWebsite/
├── index.html      # 所有页面内容、导航和链接
├── styles.css      # 排版、颜色、手机布局、系统深色模式
├── README.md       # 本说明
├── .nojekyll       # 让 GitHub Pages 直接发布静态文件
├── .gitignore      # 忽略本机临时文件
└── assets/
    └── .gitkeep    # 保留空目录，以后存放图片、PDF 等
```

`index.html` 通过 `<link rel="stylesheet" href="./styles.css">` 加载样式。所有内容都写在 HTML 中，浏览器打开就能阅读；站内导航通过 `href="#research"` 跳到对应的 `id="research"`。没有 `script.js`，因为当前页面没有需要脚本的功能。

## 1. 本地打开

直接双击 `index.html`，或拖进浏览器即可。修改文件并保存后刷新页面。

如果电脑安装了 Python，也可以在项目目录运行：

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

然后访问 http://127.0.0.1:8000 。终端按 `Ctrl+C` 停止服务。这个服务仅供本地预览，部署时不需要 Python。

## 2. 修改内容

打开 `index.html`，搜索以下注释或 section ID：

| 内容 | 修改位置 |
| --- | --- |
| 姓名、简短介绍、顶部导航 | `<header class="site-header">` |
| About | `<!-- ABOUT:` / `id="about"` |
| Research | `<!-- RESEARCH:` / `id="research"` |
| Projects | `<!-- PROJECTS:` / `id="projects"` |
| Notes | `<!-- NOTES:` / `id="notes"` |
| Writing | `<!-- WRITING:` / `id="writing"` |
| 邮箱、GitHub、版权 | `<footer class="site-footer">` |
| 浏览器标签页名称、搜索简介 | `<title>` 和 `<meta name="description">` |

About 是可替换的简短初稿，没有添加学历、任职或成果。Research 的说明是兴趣描述。Projects 根据“正在做”暂时统一标为 `Active`，可以逐项改成 `Experimental`、`Paused` 等。

### Research

在 `research-list` 内复制一个完整的 `<div>`，修改 `<dt>` 中的方向名称和 `<dd>` 中的说明。

### Projects

在 `project-list` 内复制一个完整的 `<li>...</li>`。项目名在 `<h3>`，状态在 `<span class="status">`，一句话说明在 `<p>`。

未提供的地址用不可点击的 `span` 占位，避免 `href="#"` 点击后跳回页首。准备好真实地址后，将整段占位：

```html
<span class="pending-link" role="link" aria-disabled="true">GitHub <span class="link-note">— link coming soon</span></span>
```

替换为普通链接，下面的 `YOUR_REPOSITORY` 需要改成真实仓库名：

```html
<a href="https://github.com/wavesye/YOUR_REPOSITORY">GitHub</a>
```

### Notes 和 Writing

Notes 每个分类对应一个 `<li>`。有内容后，把占位 `span` 换成链接，例如：

```html
<li><a href="./notes/computer-networks.html">Computer Networks</a></li>
```

Writing 分为 Law、Engineering、Computer Science。将相应分类中 `<li class="muted">No entries yet.</li>` 替换成真实文章列表，例如：

```html
<li><a href="./writing/first-note.html">My first note</a></li>
```

只有在对应文件已创建时再添加链接。可以继续用 Markdown 写作，先链接到 GitHub 上的 `.md` 文件供阅读；以后需要在本站显示排版后的文章时，再将 Markdown 转成 HTML 并链接到生成的 `.html`。**当前 `.nojekyll` 方案不会把 Markdown 自动转换成网页**，也没有在浏览器内加入 Markdown 渲染器。

### 邮箱与附件

将 Footer 中 Email 的整段占位 `span` 改为 `<a href="mailto:YOUR_EMAIL">Email</a>`，把 `YOUR_EMAIL` 换成你的邮箱。

图片或 PDF 放进 `assets/`，链接用 `./assets/filename.pdf` 这样的相对路径。避免使用 `/assets/...`：开头的 `/` 会跳过项目网站的 `/PersonalWebsite/` 路径。

### 调整样式

`styles.css` 顶部 `:root` 中可修改背景色、文字色、链接色以及 `--content-width`（默认 `850px`）。`prefers-color-scheme: dark` 定义系统深色模式的颜色；底部两个媒体查询负责小屏幕布局。正文使用系统字体，不请求 Google Fonts 或其他外部资源。

页面内容默认是英文；如果主要改成中文，把 `<html lang="en">` 改为 `<html lang="zh-CN">`。

## 3. Push 到 GitHub

首次上传（在本项目目录执行；如果已经初始化或关联远程，跳过对应步骤）：

```sh
git init
git add index.html styles.css README.md .nojekyll .gitignore assets/.gitkeep
git commit -m "Create minimal personal website v0.1"
git branch -M main
git remote add origin https://github.com/wavesye/PersonalWebsite.git
git push -u origin main
```

用 `git remote -v` 检查已有远程地址。已正确配置 `origin` 时不用再添加。需要在 GitHub 上先创建同名仓库；如果远程已有提交，先同步历史，避免强制推送覆盖内容。

后续更新：

```sh
git status
git add index.html styles.css
git commit -m "Update personal website content"
git push
```

如果新建笔记、文章或附件，也将相应文件路径加入 `git add`。首次推送可能要求 GitHub 登录；可以使用 GitHub Desktop 或已配置的 Git 凭据，不要把访问令牌写进代码或 README。

## 4. 开启 GitHub Pages

1. 打开仓库的 **Settings → Pages**。
2. 在 **Build and deployment** 下，将 **Source** 设为 **Deploy from a branch**。
3. 选择 **main** 分支和 **/ (root)** 目录，点击 **Save**。
4. 等待 GitHub Pages 部署完成。可在 **Actions** 查看 `pages build and deployment` 的结果，在 **Settings → Pages** 查看实际访问地址。
5. 成功后访问 https://wavesye.github.io/PersonalWebsite/ 。首次部署可能需要几分钟，后续 push 到 `main` 会自动更新。

这个项目的根目录直接包含 `index.html`，所有资源使用相对路径；不需要安装依赖、运行构建命令或额外配置 Actions 工作流。`.nojekyll` 让这些静态文件按原样发布。

GitHub Free 可以为公开仓库启用 Pages；私有仓库是否可用取决于账户计划。发布后的个人网页通常是公开可访问的。

官方说明：[配置 GitHub Pages 的发布来源](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。

## 5. 如果仓库名是 username.github.io

使用与 GitHub 用户名一致的仓库名 `username.github.io`，网站地址就是 `https://username.github.io/`，没有项目名后缀。

对当前账号而言：

| 仓库名 | 网站地址 |
| --- | --- |
| `PersonalWebsite`（当前） | `https://wavesye.github.io/PersonalWebsite/` |
| `wavesye.github.io` | `https://wavesye.github.io/` |

不需要为此改动 HTML 或 CSS 的相对路径。这里只说明两种地址的区别，当前项目继续使用你指定的 `PersonalWebsite` 仓库。

## 简单自检

- 在浏览器中打开页面，点击顶部导航，检查是否跳到对应章节。
- 用开发者工具查看 320px、390px、768px 和桌面宽度，确认没有横向滚动。
- 切换系统外观或模拟 `prefers-color-scheme: dark`，检查文字和链接是否清晰。
- 用 `Tab` 检查导航焦点；第一个焦点是 “Skip to content”。
- 放大页面或文字到 200%，检查内容仍然可读。
- 添加实际链接后检查地址；“coming soon”和空分类在补齐前保持不可点击。
