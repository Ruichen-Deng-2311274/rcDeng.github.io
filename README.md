# Personal homepage

一个简洁的英文个人主页：About、Notes、Useful Links。为 GitHub Pages 准备，使用它原生支持的 Jekyll 和 Markdown。没有前端框架、数据库或浏览器脚本，也不加载外部字体。

三个栏目是独立页面：`index.html` 显示个人简介，`notes.html` 显示笔记列表，`links.html` 显示常用链接。顶部导航切换页面，当前栏目带下划线。Notes 支持直接打开 PDF，也支持文字笔记；文字笔记的 “All notes” 返回笔记列表。

## 平时只改这些

| 想改什么 | 编辑哪个文件 |
| --- | --- |
| 姓名、单位、邮箱、网站描述 | `_config.yml` 最上面的四项 |
| 个人简介、教育经历、研究兴趣 | `content/about.md` |
| Useful Links | `content/links.md` |
| 上传或替换 PDF 笔记 | 把 PDF 放进 `assets/pdfs/`，列表自动更新 |
| PDF 的显示标题、说明或日期（可选） | `_data/pdf_notes.yml` |
| 文字笔记 | `_notes/` 中对应的 `.md` 文件 |

页面上的方括号文字、Your Name、邮箱和示例笔记都需要换成你自己的内容。单位或邮箱不想显示时，在 `_config.yml` 中保留字段，值改为 `""`。日常修改不需要碰 `_layouts/`、三个 `.html` 页面或 `assets/style.css`。

## 第一次放到 GitHub Pages

1. 在 GitHub 新建公开仓库，名称为 **你的用户名.github.io**。
2. 把本文件夹的**内容**上传到仓库根目录。不要把整个 `personal-homepage` 文件夹套在仓库里面。确认 `_config.yml`、`index.html`、`notes.html`、`links.html`、`_layouts/`、`_notes/`、`_data/`、`content/` 和 `assets/` 都已上传。
3. 进入仓库的 **Settings → Pages → Build and deployment**。
4. Source 选择 **Deploy from a branch**，分支选择 **main**，文件夹选择 **/ (root)**，点击 Save。
5. 等 GitHub 完成构建，访问 `https://你的用户名.github.io/`。可在仓库的 Actions 页面查看构建状态。

不要添加 `.nojekyll` 文件，它会关闭这里需要的 Markdown 构建。仓库中也不需要上传预览文件夹或压缩包。本模板的站内链接使用相对路径，也支持普通项目仓库的 `/仓库名/` 地址。

此版本只在本地制作和预览，尚未创建 GitHub 仓库或公开发布。

## 以后如何维护

在 GitHub 打开对应的文件，点击铅笔图标，改完后点击 **Commit changes**。GitHub Pages 会自动重新生成网页；不需要重新上传整个网站，也不需要在电脑上安装软件。

### 上传 PDF 笔记（推荐）

在 GitHub 打开仓库中的 `assets/pdfs/` 文件夹，选择 **Add file → Upload files**，把你的 PDF 拖进去并提交。下一次 GitHub Pages 构建完成后，Notes 会自动列出新文件，**不需要另写 Markdown，也不需要手动添加列表条目**。

- 点击标题直接打开原 PDF，公式、图片和原有排版保持不变。浏览器支持预览时直接阅读，否则会下载或交给系统阅读器；可用浏览器返回按钮回到 Notes。
- 每个 PDF 旁边都有 `PDF` 标记和 **Download PDF** 链接，下载行为仍由浏览器决定。
- 默认标题来自文件名：例如 `Linear-Algebra.pdf` 显示为 `Linear Algebra`。建议使用简短文件名；空格、中文和大写 `.PDF` 扩展名也支持。
- 更新同一篇笔记时，用新 PDF 替换同名文件，链接保持不变。删除文件后，相应条目会在重新构建后自动消失。
- PDF 按文件路径排序，出现在文字笔记前。支持 `assets/pdfs/` 中的子文件夹。

当前带了一份 `assets/pdfs/sample-pdf-note.pdf` 作为可打开的示例。上传自己的 PDF 后，可以删除它。要移除文字示例，删除 `_notes/a-first-note.md`；两种示例都删除后，如果没有自己的文件，Notes 会显示 “No notes yet.”。

#### 可选：自定义 PDF 标题、说明和日期

只上传文件就够用。若想让标题更正式，编辑 `_data/pdf_notes.yml`，按下面格式增加一项：

```yaml
"Linear-Algebra.pdf":
  title: "Notes on Linear Algebra"
  description: "Vector spaces, linear maps, and eigenvalues."
  date: 2026-09-21
```

第一行必须与 PDF 文件名完全一致，包含大小写和扩展名；子文件夹中的文件写成 `course/Linear-Algebra.pdf`。下面三项都可省略，缩进使用两个空格。日期是你填写的笔记日期，不会用上传时间替代。删除 PDF 后，可同时删除它在这里的配置。

### 新增文字笔记（可选）

在 GitHub 仓库首页选择 **Add file → Create new file**，文件名输入 `_notes/my-note.md`。使用小写英文字母、数字和连字符命名，复制下面的内容并修改：

```markdown
---
title: "My new note"
date: 2026-09-21
description: "A short summary of the note."
---

Write the first paragraph here.

## A section heading

- First point
- Second point
```

提交后，Notes 页面会自动出现这篇笔记，按日期从新到旧排列。可选的 `description` 是笔记列表中的一行简介。删除 `_notes/a-first-note.md` 可移除示例笔记；没有笔记时 Notes 页面会显示 “No notes yet.”。`templates/new-note.md` 中也保留了可复制的模板。

### 改简介与链接

简介是普通 Markdown：空一行表示分段，`### Education` 是小标题，`-` 开头表示列表，`**文字**` 表示加粗。

链接按下面格式新增一行即可：

```markdown
- [Resource name](https://example.com/) — A short description.
```

外部网址写完整的 `https://...`。如要给文字笔记加图片，可放入 `assets/files/`，从笔记引用 `../assets/files/文件名.png`；也可以链接到 `../assets/pdfs/文件名.pdf`。文字笔记支持 Markdown 正文、列表、表格、链接、图片和代码块，未额外配置数学公式渲染；PDF 中已有的公式无需转换。

## 可选：在自己电脑上预览

日常在 GitHub 修改无需这一步。有 Ruby 环境时，可在本文件夹运行：

```sh
bundle install
bundle exec jekyll serve
```

随后打开终端显示的本地地址。`_config.yml` 修改后需重启预览。源文件 `index.html` 包含模板语法，不能直接双击当作成品；本次同时提供了已生成的 `preview` 文件夹，可直接打开其中的 `index.html` 查看当前版本。

## 官方说明

- [GitHub Pages 快速开始](https://docs.github.com/en/pages/quickstart)
- [GitHub Pages 与 Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)
- [设置发布来源](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
