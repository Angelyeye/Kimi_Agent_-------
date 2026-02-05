# 🚀 部署指南

## GitHub Pages 一键部署

### 步骤 1: 创建 GitHub 仓库

1. 登录 [GitHub](https://github.com)
2. 点击右上角 `+` → `New repository`
3. 填写仓库名称：`spring-festival-simulator`
4. 选择 `Public`（公开）
5. 点击 `Create repository`

### 步骤 2: 上传代码

#### 方法一：使用 Git 命令行

```bash
# 初始化本地仓库
cd spring-festival-simulator

# 初始化 git
git init

# 添加所有文件
git add .

# 提交
git commit -m "Initial commit: Spring Festival Simulator v1.0"

# 添加远程仓库（替换 yourusername 为你的 GitHub 用户名）
git remote add origin https://github.com/yourusername/spring-festival-simulator.git

# 推送到 GitHub
git push -u origin main
```

#### 方法二：直接上传文件

1. 在 GitHub 仓库页面点击 `Add file` → `Upload files`
2. 拖拽或选择 `src` 目录下的所有文件
3. 点击 `Commit changes`

### 步骤 3: 启用 GitHub Pages

1. 进入仓库的 `Settings` 页面
2. 左侧菜单点击 `Pages`
3. 在 `Source` 部分选择 `Deploy from a branch`
4. 选择 `main` 分支和 `/ (root)` 文件夹
5. 点击 `Save`

### 步骤 4: 访问游戏

等待 1-2 分钟后，访问：
```
https://yourusername.github.io/spring-festival-simulator/
```

## 🔧 自定义域名（可选）

1. 在 `src` 目录下创建 `CNAME` 文件
2. 写入你的域名，如：`spring-festival.yourdomain.com`
3. 在域名服务商处添加 CNAME 记录指向 `yourusername.github.io`
4. 在 GitHub Pages 设置中启用 `Enforce HTTPS`

## 📱 移动端适配

游戏已内置响应式设计，无需额外配置。

### PWA 支持（可选）

如需添加 PWA 功能：

1. 在 `src` 目录添加 `manifest.json`：
```json
{
  "name": "春节模拟器",
  "short_name": "春节模拟器",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#0D0D0D",
  "theme_color": "#C41E3A",
  "icons": [
    {
      "src": "assets/icon-192.png",
      "sizes": "192x192"
    },
    {
      "src": "assets/icon-512.png",
      "sizes": "512x512"
    }
  ]
}
```

2. 在 `index.html` 的 `<head>` 中添加：
```html
<link rel="manifest" href="manifest.json">
```

## 🔄 自动部署（GitHub Actions）

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./src
```

## 🐛 常见问题

### Q: 页面显示 404
A: 检查 GitHub Pages 设置是否正确，确保选择了正确的分支

### Q: 样式没有加载
A: 检查文件路径是否正确，GitHub Pages 区分大小写

### Q: 游戏数据没有保存
A: 检查浏览器是否支持 LocalStorage，是否开启了隐私模式

### Q: 如何更新游戏
A: 修改代码后重新 push 到 GitHub，GitHub Pages 会自动更新

## 📞 技术支持

如有问题，请提交 [Issue](https://github.com/yourusername/spring-festival-simulator/issues)

---

🎮 **祝你部署顺利，游戏愉快！** 🧧
