# BMS 硬件产品展示网站规划方案

## 项目概述

使用 Cloudflare Pages + GitHub 构建一个静态个人网站，主要用于展示 BMS（电池管理系统）硬件产品的图文介绍，并提供上位机软件下载功能。

---

## 一、技术栈选择

### 推荐方案：Hugo + Cloudflare Pages

| 组件 | 选择 | 理由 |
|------|------|------|
| 静态站点生成器 | Hugo | 构建速度快、配置简单、主题丰富、维护活跃 |
| 前端框架 | 原生 HTML/CSS/JS | 静态展示为主，无需复杂框架 |
| 代码托管 | GitHub | 免费、与 Cloudflare Pages 无缝集成 |
| 部署平台 | Cloudflare Pages | 免费、全球 CDN、自动部署、自定义域名 |
| 文件下载 | 直接静态文件 | 上位机软件作为静态资源直接提供下载 |

### 备选方案对比

| 方案 | 优点 | 缺点 |
|------|------|------|
| Hugo (推荐) | 构建极快、配置简单、主题多 | 需要学习模板语法 |
| Next.js | 功能强大、生态好 | 对于纯展示网站过于复杂 |
| VitePress | Vue 生态、文档友好 | 定制性稍弱 |
| 纯 HTML | 最简单 | 维护困难、无模板复用 |

---

## 二、网站结构设计

```
WebSite/
├── .github/
│   └── workflows/           # GitHub Actions 配置（可选）
├── archetypes/              # Hugo 内容模板
├── assets/                  # 需要处理的资源
│   ├── css/
│   ├── js/
│   └── images/
├── content/                 # 网站内容
│   ├── _index.md           # 首页
│   ├── products/           # 产品介绍
│   │   ├── _index.md       # 产品列表页
│   │   ├── bms-100a.md     # 具体产品页面
│   │   └── bms-200a.md
│   ├── downloads/          # 下载页面
│   │   └── _index.md
│   └── about/              # 关于我们
│       └── _index.md
├── data/                    # 数据文件（JSON/YAML）
├── layouts/                 # 页面模板
│   ├── _default/
│   │   ├── baseof.html     # 基础模板
│   │   ├── list.html       # 列表页模板
│   │   └── single.html     # 单页模板
│   ├── partials/           # 公共组件
│   │   ├── header.html
│   │   ├── footer.html
│   │   └── nav.html
│   └── index.html          # 首页模板
├── static/                  # 静态资源（直接复制）
│   ├── downloads/          # 上位机软件存放目录
│   │   └── bms-tool-v1.0.0.zip
│   ├── images/             # 产品图片
│   │   └── products/
│   └── files/              # 其他文件
├── themes/                  # 主题目录（如使用第三方主题）
├── config.toml             # Hugo 配置文件
└── README.md               # 项目说明
```

---

## 三、功能模块设计

### 3.1 首页
- 公司/个人简介
- 核心产品亮点展示
- 快速导航入口

### 3.2 产品展示页
- 产品列表（网格/卡片布局）
- 单个产品详情页
  - 产品图片（支持多图轮播）
  - 产品参数规格表
  - 功能特点介绍
  - 应用场景说明
  - 相关下载链接

### 3.3 下载中心
- 上位机软件列表
  - 软件名称
  - 版本号
  - 更新日期
  - 文件大小
  - 下载按钮
- 版本更新日志

### 3.4 关于页面
- 公司/团队介绍
- 联系方式
- 技术支持信息

---

## 四、部署流程

### 4.1 GitHub 仓库设置

```
1. 在 GitHub 创建仓库（如：bms-website）
2. 将本地代码推送到 GitHub
3. 仓库结构建议：
   - main 分支：生产环境
   - dev 分支：开发环境（可选）
```

### 4.2 Cloudflare Pages 配置

```
1. 登录 Cloudflare Dashboard
2. 进入 Pages → 创建项目
3. 连接 GitHub 仓库
4. 配置构建设置：
   - 构建命令：hugo
   - 输出目录：public
   - 环境变量：HUGO_VERSION=0.120.0
5. 绑定自定义域名（可选）
```

### 4.3 自动部署流程

```
代码推送到 GitHub
        ↓
Cloudflare 自动检测变更
        ↓
触发构建流程
        ↓
Hugo 生成静态文件
        ↓
部署到全球 CDN
        ↓
网站自动更新
```

---

## 五、实施步骤

### 第一阶段：项目初始化
1. 安装 Hugo（本地开发环境）
2. 初始化 Hugo 项目结构
3. 选择并配置主题（推荐：hugo-theme-landing 或自定义）
4. 创建基础配置文件

### 第二阶段：页面开发
5. 开发公共组件（Header、Footer、导航）
6. 开发首页模板
7. 开发产品列表页模板
8. 开发产品详情页模板
9. 开发下载中心页面

### 第三阶段：内容填充
10. 编写产品介绍内容（Markdown）
11. 准备产品图片资源
12. 上传上位机软件到 static/downloads

### 第四阶段：部署上线
13. 创建 GitHub 仓库并推送代码
14. 配置 Cloudflare Pages
15. 测试部署流程
16. 绑定自定义域名（如有）

### 第五阶段：优化完善
17. SEO 优化（meta 标签、sitemap）
18. 性能优化（图片压缩、CDN）
19. 添加 Google Analytics（可选）
20. 编写使用文档

---

## 六、配置文件示例

### config.toml

```toml
baseURL = "https://your-domain.com"
languageCode = "zh-cn"
title = "BMS 硬件产品中心"
theme = ""  # 使用自定义模板

[params]
  description = "专业 BMS 电池管理系统硬件产品展示"
  author = "Your Name"
  
[menu]
  [[menu.main]]
    name = "首页"
    url = "/"
    weight = 1
  [[menu.main]]
    name = "产品中心"
    url = "/products/"
    weight = 2
  [[menu.main]]
    name = "下载中心"
    url = "/downloads/"
    weight = 3
  [[menu.main]]
    name = "关于我们"
    url = "/about/"
    weight = 4
```

---

## 七、下载功能实现

### 方案：静态文件直接下载

将上位机软件放置在 `static/downloads/` 目录：

```
static/
└── downloads/
    ├── BMS-Tool-v1.0.0.exe
    ├── BMS-Tool-v1.0.0.dmg    # macOS 版本
    └── release-notes.md       # 更新日志
```

下载链接格式：
```html
<a href="/downloads/BMS-Tool-v1.0.0.exe" download>
  下载 Windows 版本
</a>
```

### 下载页面数据管理

使用 `data/downloads.yaml` 管理下载信息：

```yaml
software:
  - name: "BMS 上位机工具"
    version: "v1.0.0"
    date: "2024-01-15"
    size: "15.2 MB"
    platform: "Windows"
    file: "/downloads/BMS-Tool-v1.0.0.exe"
    description: "BMS 参数配置与监控工具"
```

---

## 八、成本估算

| 项目 | 费用 |
|------|------|
| GitHub 仓库 | 免费 |
| Cloudflare Pages | 免费 |
| 域名（可选） | 约 ¥50-100/年 |
| **总计** | **免费或约 ¥100/年** |

---

## 九、后续扩展

1. **多语言支持**：Hugo 原生支持多语言
2. **博客功能**：添加技术文章/新闻模块
3. **在线文档**：集成文档系统
4. **反馈系统**：集成第三方评论/反馈工具
5. **搜索功能**：集成 Algolia 或本地搜索

---

## 十、注意事项

1. **文件大小限制**：GitHub 单文件限制 100MB，大文件需使用 Git LFS
2. **构建时间**：Cloudflare Pages 免费版构建时间限制
3. **带宽限制**：Cloudflare 免费版有合理使用限制
4. **备份策略**：定期备份内容和配置
5. **版本管理**：使用 Git 标签管理软件版本
