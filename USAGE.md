# BMS 硬件产品中心 - 使用指南

## 架构

所有配置和数据集中管理：
- **`config.toml`** — 所有配置（网站信息、联系方式、首页、下载、关于我们）
- **`content/products/*.md`** — 产品内容（每个产品一个文件）
- **`static/`** — 所有静态资源（图片、CSS、JS、下载文件）

## 项目结构

```
WebSite/
├── config.toml              # 统一配置
├── content/
│   ├── products/            # 产品 .md 文件
│   │   ├── ble200a.md
│   │   └── pd100w.md
│   ├── downloads/_index.md  # 路由
│   └── about/_index.md      # 路由
├── layouts/                 # HTML 模板
├── static/                  # 所有资源
│   ├── css/style.css
│   ├── js/main.js
│   ├── downloads/           # 软件安装包
│   └── images/              # 所有图片
│       ├── products/        # 产品图片
│       └── wechat-miniprogram-qr.jpg
└── public/                  # 构建输出
```

## 快速命令

```powershell
.\hugo.exe server            # 本地预览
.\hugo.exe --gc --minify     # 构建生产版本
```

## 配置说明（config.toml）

| 配置项 | 说明 |
|--------|------|
| `[params.contact]` | 联系方式 |
| `[params.hero]` | 首页 Hero 区域 |
| `[params.features]` | 首页特性卡片 |
| `[params.productsPreview]` | 首页热门产品 |
| `[params.cta]` | 首页底部号召 |
| `[params.downloads.software]` | 下载软件列表 |
| `[params.downloads.changelog]` | 更新日志 |
| `[params.about.sections]` | 关于我们内容 |
| `[menu.main]` | 导航菜单 |

## 产品管理

### 添加产品
```powershell
.\hugo.exe new products/产品名.md
```

### 产品文件模板
```yaml
---
title: "产品名称"
date: 2024-01-10
draft: false
description: "简短描述"
images:
  - "/images/products/图片1.png"
specs:
  - name: "参数名"
    value: "参数值"
features: ["特点1", "特点2"]
applications: ["场景1", "场景2"]
advantages: ["**优势**：说明"]
---

产品介绍正文
```

## 静态资源管理

所有资源统一放在 `static/` 下：

| 类型 | 位置 |
|------|------|
| 产品图片 | `static/images/products/` |
| 微信二维码 | `static/images/` |
| Logo | `static/images/` |
| 软件安装包 | `static/downloads/` |
| CSS | `static/css/` |
| JS | `static/js/` |

## 部署

```powershell
git add .
git commit -m "更新内容"
git push
```
