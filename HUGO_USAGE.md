# Hugo 使用指南

## 1. 下载 Hugo 便携版本

### 方法一：官方网站下载
1. 访问 [Hugo 官方下载页](https://github.com/gohugoio/hugo/releases)
2. 下载适合 Windows 的便携版本（例如：hugo_0.120.0_windows-amd64.zip）
3. 解压到项目根目录

### 方法二：使用 PowerShell 下载（推荐）
```powershell
# 下载 Hugo 便携版
Invoke-WebRequest -Uri "https://github.com/gohugoio/hugo/releases/download/v0.120.0/hugo_0.120.0_windows-amd64.zip" -OutFile "hugo.zip"

# 解压到当前目录
Expand-Archive -Path "hugo.zip" -DestinationPath "."

# 清理压缩包
Remove-Item "hugo.zip"
```

## 2. 本地预览网站

```powershell
# 运行 Hugo 本地服务器（开发模式）
./hugo.exe server -D

# 访问地址：http://localhost:1313
```

## 3. 构建静态网站

```powershell
# 构建生产版本
./hugo.exe

# 构建结果将输出到 public/ 目录
```

## 4. 项目结构说明

```
WebSite/
├── config.toml              # Hugo 配置文件
├── archetypes/              # 内容模板
├── content/                 # 网站内容
│   ├── products/           # 产品页面
│   ├── downloads/          # 下载中心
│   └── about/              # 关于页面
├── data/                   # 数据文件
│   └── downloads.yaml      # 下载软件配置
├── layouts/                # 页面模板
├── static/                 # 静态资源
│   ├── css/                # 样式文件
│   ├── js/                 # JavaScript
│   ├── downloads/          # 软件存放目录
│   └── images/             # 图片目录
└── public/                 # 构建输出目录
```

## 5. 添加内容

### 添加产品
1. 在 `content/products/` 目录下创建新的 Markdown 文件
2. 参考现有产品文件的格式添加内容

### 添加上位机软件
1. 将软件安装包放入 `static/downloads/` 目录
2. 在 `data/downloads.yaml` 中添加软件信息

## 6. 部署到 Cloudflare Pages

1. **创建 GitHub 仓库**
   - 在 GitHub 上创建新仓库
   - 将项目推送到仓库

2. **配置 Cloudflare Pages**
   - 登录 Cloudflare Dashboard
   - 进入 Pages → 创建项目
   - 连接 GitHub 仓库
   - 配置构建参数：
     - 构建命令：`hugo`
     - 输出目录：`public`
     - 环境变量：`HUGO_VERSION=0.120.0`

3. **部署完成**
   - Cloudflare 会自动构建并部署网站
   - 访问分配的子域名或绑定自定义域名

## 7. 常见问题

### Q: 本地服务器启动失败
A: 检查 Hugo 是否正确解压，确保 `hugo.exe` 在项目根目录

### Q: 页面显示空白
A: 检查内容文件是否有 `draft: true`，开发模式下使用 `-D` 参数

### Q: 图片不显示
A: 确保图片路径正确，使用相对路径（例如：`/images/products/bms-100a.jpg`）

### Q: 下载链接无效
A: 确保软件文件已放入 `static/downloads/` 目录，且路径配置正确
