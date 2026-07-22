# MrKeanu's Blog

> Powered by [Hexo](https://hexo.io/) with the elegant [Fluid](https://github.com/fluid-dev/hexo-theme-fluid) theme.  
> Sharing insights on programming, deep learning, personal reflections, and life stories.

## Article Categories

All posts are organized into three primary categories, each with its own scaffold template for easy authoring.

| Category | Subcategory | Scaffold | Content |
|---|---|---|---|
| **Incessant Coding** | `Deep Learning` | `hexo new coding` | Technical articles, programming tutorials, and deep learning explorations (PyTorch, neural networks, etc.) |
| **Unceasing Insights** | — | `hexo new insight` | Personal reflections, thoughts on life, and philosophical musings |
| **Everlasting Life** | — | `hexo new life` | Life records, yearly summaries, and personal milestones |

Each category provides custom fields in its front-matter, such as pre-set banner images, tags, and layout options.

## Project Structure

```
MrKeanu-V.github.io/
├── _config.yml             # Hexo core configuration (site, URL, deploy, etc.)
├── _config.fluid.yml       # Fluid theme configuration (appearance, plugins, pages)
├── package.json            # Node.js dependencies and scripts
├── scaffolds/              # Post templates (coding, insight, life, draft, post)
├── source/
│   ├── _posts/             # All blog articles in Markdown
│   ├── _data/              # Data files for the theme (if any)
│   ├── about/              # About page (index.md)
│   └── image/              # Static images (banners, icons, article covers)
│       ├── bg/             # Banner background images
│       ├── icon/           # Avatar, icons, and QR codes
│       └── index/          # Homepage/section cover images
└── themes/                 # Installed themes (fluid via npm or git submodule)
```

- **`_config.yml`** — Global Hexo settings: site metadata, URL structure, Markdown rendering, and Git deployment to `gh-pages`.
- **`_config.fluid.yml`** — All theme-level customisation: navbar menus, banners, post meta, widgets (TOC, category bar, comments via Utterances), and dark mode.
- **`scaffolds/`** — Front-matter templates used by `hexo new <type>` to pre-populate metadata like tags, categories, and cover images.
- **`source/_posts/`** — Where all published articles live. Each `.md` file includes YAML front-matter and Markdown body content.
- **`source/image/`** — Organised subdirectories for background banners, category covers, and personal icons.

## Quick Start

### Hexo CLI

```shell
# 本地预览
hexo server          # 启动本地服务，默认 http://localhost:4000
hexo s               # 简写

# 生成静态文件
hexo generate        # 生成 public/ 目录
hexo g               # 简写

# 部署到 GitHub Pages
hexo deploy          # 推送到 gh-pages 分支
hexo d               # 简写

# 组合命令（生成+部署）
hexo generate --deploy
hexo g -d

# 清除缓存（遇到奇怪问题时试试）
hexo clean
```

## Begin Write

```shell
# 写一篇编程/技术文章
hexo new coding "文章标题"

# 写一篇人生感悟
hexo new insight "文章标题"

# 写一篇生活记录或年度总结
hexo new life "文章标题"

# 写一篇普通文章（不指定类别）
hexo new post "文章标题"

# 写一篇草稿（不立即发布）
hexo new draft "草稿标题"