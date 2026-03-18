# 内容管理指南

本指南说明如何更新网站内容，无需修改代码，只需编辑 Markdown 或 YAML 文件即可。

---

## 一、更新产品信息

产品信息存放在 `content/products/` 目录，每个产品一个 Markdown 文件。

### 添加新产品

在 `content/products/` 目录下创建新的 `.md` 文件，例如 `bms-300a.md`：

```markdown
---
title: "产品名称"
date: 2024-01-15
draft: false
description: "产品简短描述（显示在列表页）"
images:
  - "/images/products/产品图片1.jpg"
  - "/images/products/产品图片2.jpg"
specs:
  - name: "参数名称"
    value: "参数值"
  - name: "额定电流"
    value: "100A"
  - name: "电压范围"
    value: "12V-48V"
features:
  - "特点1"
  - "特点2"
  - "特点3"
---

## 产品概述

这里写产品的详细介绍，支持 **Markdown 格式**。

## 应用场景

- 应用1
- 应用2
- 应用3

## 技术优势

1. 优势一
2. 优势二
```

### 修改现有产品

直接编辑 `content/products/` 目录下对应的 `.md` 文件。

### 产品文件说明

| 字段 | 说明 | 示例 |
|------|------|------|
| title | 产品名称 | "BMS-100A 智能电池管理系统" |
| date | 发布日期 | 2024-01-15 |
| draft | 是否草稿 | false（发布）/ true（草稿） |
| description | 简短描述 | 显示在产品列表页 |
| images | 产品图片列表 | 支持多张图片轮播 |
| specs | 规格参数表 | 显示为表格形式 |
| features | 产品特点 | 显示为列表形式 |

---

## 二、更新下载信息

下载信息存放在 `data/downloads.yaml` 文件中。

### 文件结构

```yaml
software:
  - name: "软件名称"
    version: "v1.0.0"
    date: "2024-01-15"
    size: "15.2 MB"
    platform: "Windows"
    file: "/downloads/软件文件名.exe"
    description: "软件功能描述"
```

### 添加新软件

1. 将软件文件放入 `static/downloads/` 目录
2. 编辑 `data/downloads.yaml`，添加新条目：

```yaml
software:
  - name: "BMS 上位机工具"
    version: "v1.1.0"          # 新版本号
    date: "2024-02-20"         # 发布日期
    size: "16.5 MB"            # 文件大小
    platform: "Windows"        # 平台：Windows/macOS/Linux
    file: "/downloads/BMS-Tool-v1.1.0.exe"  # 文件路径
    description: "BMS 参数配置与监控工具"
```

### 平台图标对应

| platform 值 | 显示图标 |
|-------------|----------|
| Windows | 🪟 |
| macOS | 🍎 |
| Linux | 🐧 |
| 其他 | 📦 |

---

## 三、更新图片

### 产品图片

1. 将图片放入 `static/images/products/` 目录
2. 建议命名格式：`产品型号-序号.jpg`
3. 在产品 Markdown 文件中引用：

```yaml
images:
  - "/images/products/bms-100a-1.jpg"
  - "/images/products/bms-100a-2.jpg"
```

### 图片规格建议

- 格式：JPG 或 PNG
- 尺寸：800x600 像素以上
- 大小：建议不超过 500KB

### 微信小程序二维码

1. 将二维码图片放入 `static/images/` 目录
2. 命名为 `wechat-miniprogram-qr.jpg`
3. 在 `config.toml` 中配置路径：

```toml
[params]
  wechatMiniProgramQR = "/images/wechat-miniprogram-qr.jpg"
```

---

## 四、更新其他页面

### 首页

编辑 `content/_index.md`

### 关于页面

编辑 `content/about/_index.md`

### 下载中心说明

编辑 `content/downloads/_index.md`

---

## 五、更新流程

### 本地预览

```powershell
# 启动本地服务器
./hugo.exe server -D

# 访问 http://localhost:1313 预览效果
```

### 发布更新

1. 提交更改到 Git
2. 推送到 GitHub
3. Cloudflare Pages 自动构建部署

```powershell
git add .
git commit -m "更新产品信息"
git push
```

---

## 六、常见更新场景

### 场景1：发布新产品

1. 准备产品图片 → 放入 `static/images/products/`
2. 创建产品文件 → `content/products/新产品.md`
3. 本地预览确认 → `./hugo.exe server -D`
4. 推送到 GitHub

### 场景2：更新软件版本

1. 放入新版本软件 → `static/downloads/`
2. 更新下载配置 → `data/downloads.yaml`
3. 更新更新日志 → `content/downloads/_index.md`
4. 推送到 GitHub

### 场景3：修改产品参数

1. 编辑对应产品文件 → `content/products/xxx.md`
2. 修改 specs 或 features 部分
3. 推送到 GitHub

---

## 七、文件位置速查

| 内容类型 | 文件位置 |
|----------|----------|
| 产品信息 | `content/products/*.md` |
| 下载配置 | `data/downloads.yaml` |
| 软件文件 | `static/downloads/*` |
| 产品图片 | `static/images/products/*` |
| 微信小程序二维码 | `static/images/wechat-miniprogram-qr.jpg` |
| 网站配置 | `config.toml` |
| 关于页面 | `content/about/_index.md` |
| 首页内容 | `content/_index.md` |
