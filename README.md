# 个人主页 · 使用说明

这个文件夹就是你的网站，也是要推到 GitHub 的仓库。
纯静态 HTML/CSS，没有构建步骤，改完保存、推送即可。

---

## 一、第一次发布（约 5 分钟）

### 1. 建仓库

登录 GitHub → 右上角 `+` → **New repository**

- **Repository name**：填 `你的用户名.github.io`
  （把「你的用户名」换成你的 GitHub 用户名，**必须完全一致**，全小写。
  例如用户名是 `pangyumo`，仓库名就是 `pangyumo.github.io`）
- **Visibility**：选 **Public**（免费版的 Pages 只支持公开仓库）
- 不要勾 Add a README / .gitignore / license
- 点 **Create repository**

> 为什么必须叫这个名字：这是 GitHub 的约定，只有这个仓库名才能得到
> `https://你的用户名.github.io` 这样的根地址。叫别的名字也能用，但网址会变成
> `https://你的用户名.github.io/仓库名/`。

### 2. 上传文件

在新建好的仓库页，点 **Add file** → **Upload files**，
然后打开 `D:\1,files\Ecoutez`，**选中里面所有文件和文件夹**（不要选 Ecoutez 文件夹本身），
拖进浏览器上传框。

底部填一句说明，比如 `initial site`，点 **Commit changes**。

> 网页上传的限制：单文件 25 MB，一次最多 100 个文件。
> 如果 PDF 超过 25 MB，改用 [GitHub Desktop](https://desktop.github.com/) 上传。

### 3. 开启 Pages

仓库顶部 **Settings** → 左侧 **Pages** → **Build and deployment**

- **Source**：`Deploy from a branch`
- **Branch**：`main`，文件夹 `/ (root)`
- 点 **Save**

等 1～5 分钟，刷新这个页面，顶部会出现：
`Your site is live at https://你的用户名.github.io/`

### 4. 确认 PDF 在资源目录里

笔记页链接的是 `assets/pdfs/Riemann_Surfaces_Pang_Yumo.pdf`，
这份文件已经复制进去了（约 0.96 MB），上传时会一起带上去，不需要额外操作。

根目录下的同名 PDF 是原件，可以保留作备份，也可以在确认无误后删掉。

---

## 二、日常更新：加一篇新笔记

假设你又写好了一份 `Complex_Analysis.pdf`。

**第 1 步**：把 PDF 放进 `assets/pdfs/`。

**第 2 步**：复制 `notes/riemann-surfaces.html`，改名为 `notes/complex-analysis.html`，
然后改这几处：

- `<title>` 和 `<h1>` 里的标题
- `note-meta` 里的分类和年份
- 摘要段落（替换掉 `placeholder` 那段）
- 三个 PDF 链接，把文件名换成 `../assets/pdfs/Complex_Analysis.pdf`
- 上一页/返回链接保持不变即可

**第 3 步**：打开 `writings.html`，复制一整个 `<li class="entry">…</li>` 块，
粘到列表最上面，改标题、链接、日期、摘要。
首页 `index.html` 里「近期写作」也照做，只留最新的 2～3 篇。

**第 4 步**：推送。等一分钟，刷新网页。

---

### 加一篇创作

创作那部分比数学简单，没有独立的阅读页，直接链 PDF：

1. 把 PDF 放进 `assets/pdfs/`，文件名用英文
2. 打开 `creative.html`，复制一整个 `<li class="entry">…</li>` 块改掉，
   链接写成 `assets/pdfs/文件名.pdf`
3. 首页 `index.html` 的「创作」区块里，复制一行 `<li class="work-line">…</li>`

如果某篇想写长一点的介绍，可以照 `notes/riemann-surfaces.html` 单独建一个
`works/xxx.html`，再改链接指向它。

---

## 三、要替换的占位内容

发布前把这些找出来改成你自己的（用编辑器全局搜索）：

| 位置 | 现在的内容 | 改成 |
|---|---|---|
| 所有页面的 `.brand`、`<title>`、页脚，以及 `index.html` 的 `<h1>`（现为 `Écoutez&nbsp;!`） | `Pang Yumo` | 你的名字或站点名 |
| `index.html` 的 hero 段落 | 兴趣描述 | 你自己的介绍 |
| `index.html`、`writings.html` 的 GitHub 链接 | `https://github.com/your-username` | 你的主页 |
| `index.html` 的「关于」两段 | 通用文案 | 你的真实介绍 |
| `notes/riemann-surfaces.html` 的摘要 | 斜体占位 | 这篇笔记的摘要 |
| `index.html` 的 `<meta name="description">` | 通用描述 | 一句话介绍 |

---

## 四、可选：绑定自己的域名

1. 去域名商控制台加解析：
   - 裸域 `example.com`：加 4 条 **A 记录**，值分别为
     `185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`
   - `www.example.com`：加 1 条 **CNAME**，指向 `你的用户名.github.io`
2. 仓库 **Settings → Pages → Custom domain** 填 `example.com`，Save。
3. DNS 生效后（几分钟到几小时），勾选 **Enforce HTTPS**。

顺序不能反：先配 DNS，再填域名，否则校验会失败。

---

## 五、可选：用 Git 命令行更新

装了 Git 之后，一次性把本地和远程接上：

```powershell
cd D:\1,files\Ecoutez
git init
git add .
git commit -m "init: personal site"
git branch -M main
git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
git push -u origin main
```

以后每次改完：

```powershell
git add .
git commit -m "post: 新增复分析笔记"
git push
```

---

## 六、目录结构

```
Ecoutez/                        ← 仓库根目录 = 网站根目录
├── index.html                  首页：自我介绍 + 数学笔记 + 创作
├── writings.html               数学笔记列表
├── creative.html               创作列表（剧本 / 小说）
├── 404.html                    找不到页面时的提示
├── notes/
│   ├── riemann-surfaces.html   单篇笔记的阅读页（内嵌 PDF）
│   └── _template.html          HTML 数学笔记模板（含 KaTeX）
├── assets/
│   ├── css/style.css           全部样式
│   ├── js/main.js              主题切换、年份
│   ├── favicon.svg             站点图标
│   └── pdfs/                   放 PDF 的地方
├── .nojekyll                   空文件，阻止 Jekyll 处理（重要）
└── README.md                   本文件
```

`.nojekyll` 不要删。GitHub Pages 默认用 Jekyll 处理站点，
它会忽略所有以下划线开头的文件和文件夹。这个空文件能关掉这个行为。

---

## 七、常见问题

**打开是 404**
依次检查：仓库是不是 Public；Settings → Pages 是否已 Save；分支是否 `main`、
文件夹是否 `/ (root)`；根目录是否有 `index.html`；是否还在构建（等 2 分钟）。

**样式丢了、页面很丑**
CSS 链接用的是相对路径 `assets/css/style.css`。如果你把首页放到了子文件夹里，
路径就要跟着改。这个站点的设计前提是「所有页面都在仓库内，用相对路径互相引用」。

**PDF 打不开 / 显示 404**
PDF 还没上传，或文件名大小写不一致。Linux 服务器区分大小写，
`Riemann_Surfaces.pdf` 和 `riemann_surfaces.pdf` 是两个文件。

**改了没生效**
浏览器缓存。按 `Ctrl + F5` 强制刷新，或等 1 分钟再试。

**想加数学公式的 HTML 笔记**
用 `notes/_template.html`，里面已经接好了 KaTeX，
直接写 `$行内公式$` 和 `$$独立公式$$` 就会渲染。

---

## 八、限制

站点 ≤ 1 GB，每月约 100 GB 流量，单文件 ≤ 100 MB。
只支持静态文件，没有后端和数据库。
`*.github.io` 在国内访问可能不稳定，这是网络环境问题；如果主要读者在国内，
可以把同一份文件再部署一份到 Cloudflare Pages 或 Vercel 作为备用线路。
