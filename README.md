# Ecoutez! · 站点说明

| | |
|---|---|
| 站点 | <https://pumpkingppk.github.io/> |
| 仓库 | <https://github.com/pumpkingppk/pumpkingppk.github.io> |
| 托管 | GitHub Pages，`main` 分支，根目录 `/(root)` |
| 本地 | `D:\1,files\Ecoutez` |

纯静态 HTML/CSS，没有构建步骤。改文件 → 提交 → 等一分钟 → 网站上就有了。

---

## 一、改哪里的文字

| 想改的内容 | 文件 | 找什么 |
|---|---|---|
| 首页大标题 `Écoutez !` | `index.html` | `<h1>` |
| 首页副标题 | `index.html` | `class="lede"` |
| 「关于」两段 | `index.html` | `class="prose"` |
| 数学笔记条目 | `index.html` + `writings.html` | `class="entry"` |
| 创作条目 | `index.html` + `creative.html` | `class="work-line"` / `class="entry"` |
| 页脚版权 | 每个 HTML | `class="footer"` |
| 浏览器标签页标题 | 每个 HTML | `<title>` |

**改法**：仓库里点开文件 → 右上角铅笔 → 改 → 拉到页面底部点 **Commit changes** → 等一分钟 → `Ctrl + F5`。

只改标签中间的文字，别动尖括号。正文里的 `<`、`>`、`&` 是特殊字符，其余随便写。

---

## 二、加一篇数学笔记

**1.** PDF 放进 `assets/pdfs/`，文件名用英文，例如 `Complex_Analysis.pdf`

**2.** 复制 `notes/riemann-surfaces.html`，改名成 `notes/complex-analysis.html`，改四处：

- `<title>` 和 `<h1>` 的标题
- `class="entry-meta"` 里的年份
- `<div class="prose">` 里的摘要（**不要**加 `class="placeholder"`，那是灰色斜体的占位样式）
- 三个 `../assets/pdfs/xxx.pdf` 链接

**3.** `writings.html` 里复制一个 `<li class="entry">…</li>` 块，贴到最上面，改标题、链接、年份、摘要

**4.** `index.html` 的「数学笔记」区块照做，只留最近两三篇

---

## 三、加一篇创作

比笔记简单，没有独立阅读页，直接链 PDF。

**1.** PDF 放进 `assets/pdfs/`

**2.** `creative.html` 里复制一个 `<li class="entry">…</li>` 块，改体裁、年份、标题、链接

**3.** `index.html` 的「创作」区块里复制一行 `<li class="work-line">…</li>`

---

## 四、把网页上的改动同步到本地

网页和本地是两个副本，不会自动同步，得手动对一次。

**前提**：网页上的改动必须已经 **Commit**，编辑器里没提交的不算。

**方式一（对话里）**：说一句「同步一下」，助手会用这个地址把文件拉回来覆盖本地：

```
https://raw.githubusercontent.com/pumpkingppk/pumpkingppk.github.io/main/文件名
```

**方式二（自己来）**：打开文件的 GitHub 页面，点右上角下载图标，把文件拖进 `D:\1,files\Ecoutez` 覆盖。

**约定**：方向是「网页 → 本地」。助手在本地改的东西，会明确告诉你需要上传，不会让它悄悄和网页分叉。

---

## 五、目录结构

```
Ecoutez/                          ← 仓库根目录 = 网站根目录
├── index.html                    首页：Écoutez ! + 数学笔记 + 创作 + 关于
├── writings.html                 「数学」列表
├── creative.html                 「创作」列表
├── 404.html                      找不到页面时的提示
├── notes/
│   ├── riemann-surfaces.html     Riemann Surfaces 阅读页（内嵌 PDF）
│   └── _template.html            数学笔记模板（含 KaTeX）
├── assets/
│   ├── css/style.css             全部样式
│   ├── js/main.js                主题切换、年份
│   ├── favicon.svg               站点图标（∑）
│   └── pdfs/
│       ├── Riemann_Surfaces_Pang_Yumo.pdf
│       ├── Zanghua.pdf
│       └── Color_of_Summer_Dream.pdf
├── .nojekyll                     空文件，阻止 Jekyll 处理（不要删）
├── .gitignore                    忽略系统文件和临时文件
└── README.md                     本文件
```

**`.nojekyll` 不能删。** GitHub Pages 默认用 Jekyll 处理站点，而 Jekyll 会忽略所有下划线开头的文件。删了这个空文件，`notes/_template.html` 之类的东西会直接 404。

**`_template.html` 是公开可访问的**（`/notes/_template.html`）。不想让人看到就删掉，或者改名。

---

## 六、可选项：绑定自己的域名

1. 域名商控制台加解析：
   - 裸域 `example.com`：4 条 **A 记录** → `185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`
   - `www.example.com`：1 条 **CNAME** → `pumpkingppk.github.io`
2. 仓库 **Settings → Pages → Custom domain** 填域名，Save
3. DNS 生效后勾选 **Enforce HTTPS**

顺序不能反：先配 DNS，再填域名，否则校验会失败。

---

## 七、可选项：用 Git 命令行

装好 Git 后，一次接通：

```powershell
cd D:\1,files\Ecoutez
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin https://github.com/pumpkingppk/pumpkingppk.github.io.git
git pull origin main --allow-unrelated-histories
git push -u origin main
```

以后在网页上改完，本地一条命令同步：

```powershell
git pull
```

本地改完要发布：

```powershell
git add .
git commit -m "post: 新增一篇笔记"
git push
```

---

## 八、常见问题

**打开是 404**
仓库是否 Public；`Settings → Pages` 的 Source 是否 `Deploy from a branch`、分支 `main`、文件夹 `/(root)`；根目录有没有 `index.html`；是否还在构建（等两分钟）。

**样式全丢了**
`<link rel="stylesheet" href="assets/css/style.css">` 用的是相对路径。子目录里的页面要写成 `../assets/...`。

**PDF 打不开**
还没上传，或文件名大小写不一致。服务器区分大小写，`Zanghua.pdf` 和 `zanghua.pdf` 是两个文件。中文文件名在 URL 里会被转义，一律用英文。

**改了没生效**
浏览器缓存，`Ctrl + F5` 强刷；或者 Pages 还在构建，等一分钟。

**摘要变成了灰色斜体**
说明那段还带着 `class="placeholder"`。把 class 删掉就恢复正常样式。

**想写带公式的 HTML 笔记**
用 `notes/_template.html`，已经接好 KaTeX。正文里写 `$行内公式$`、`$$独立公式$$` 就会渲染。

---

## 九、限制

站点 ≤ 1 GB，每月约 100 GB 流量，单文件 ≤ 100 MB，网页上传单文件 ≤ 25 MB。
只支持静态文件，没有后端和数据库。

`*.github.io` 在国内访问可能不稳定。如果主要读者在国内，可以把同一份文件再部署到 Cloudflare Pages 或 Vercel 作为备用线路，都是免费的。
