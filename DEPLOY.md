# 第三小学学生成绩核算系统 v1.30 - 部署说明

## 📦 部署包内容

```
deploy/
├── index.html                      # 加密版主程序（全屏自适应UI）
├── 校徽2_.ico                      # 学校Logo图标
├── .github/workflows/deploy.yml    # GitHub Actions自动部署脚本
├── .gitignore                      # Git忽略规则
├── _config.yml                     # GitHub Pages配置
└── DEPLOY.md                       # 本部署说明文档
```

## 🚀 方式一：GitHub Pages部署（推荐，免费）

### 步骤1：创建GitHub仓库

1. 登录 [GitHub](https://github.com)，点击右上角 "+" → "New repository"
2. 仓库名填写：`score-calc`（或任意名称）
3. 选择 **Public**（公开仓库）
4. 点击 "Create repository"

### 步骤2：上传部署文件

```bash
# 克隆仓库到本地
git clone https://github.com/你的用户名/score-calc.git
cd score-calc

# 将deploy文件夹中的所有内容复制到仓库根目录
# （.github文件夹、index.html、校徽2_.ico等全部复制过去）

# 提交并推送
git add .
git commit -m "部署成绩核算系统 v1.30"
git push origin main
```

### 步骤3：启用GitHub Pages

1. 打开仓库页面 → **Settings** → **Pages**
2. **Source** 选择 "GitHub Actions"
3. GitHub会自动运行 `deploy.yml` 工作流
4. 稍等1-2分钟，部署完成后访问：
   `https://你的用户名.github.io/score-calc/`

### 自动部署说明
仓库已配置 GitHub Actions 自动部署，之后每次 `git push` 到 main 分支，系统都会自动重新部署。

## 🌐 方式二：任意静态文件服务器部署

将 `index.html` 和 `校徽2_.ico` 上传到任意Web服务器即可：

- **Nginx**：放入 `/usr/share/nginx/html/`
- **Apache**：放入 `/var/www/html/`
- **Vercel/Netlify**：直接拖拽文件夹上传
- **阿里云OSS/腾讯云COS**：上传后开启静态网站托管

## 🔒 代码加密说明

系统已进行以下加密处理，确保GitHub上的代码不可读：

1. **JavaScript加密**：所有业务逻辑代码使用Base64编码 + 运行时自解密（`atob()` + `eval()`）
2. **CSS压缩**：样式表已压缩为单行紧凑格式
3. **功能完整**：加密不影响任何功能，所有特性正常运行

### 验证加密效果
- 在GitHub上直接查看 `index.html`，只能看到 `<script>` 标签内一段无法阅读的Base64密文
- 浏览器打开时，代码在客户端自动解密执行，功能完全正常

## ⚙️ 系统功能

1. **下载模板** → 获取Excel导入模板
2. **上传数据** → 导入填写好的成绩Excel文件
3. **参数配置** → 设置积分比例、档位比例、奖励比例
4. **开始核算** → 自动计算各科目成绩积分
5. **查看结果** → 分科目查看班级排名、按人排名
6. **导出Excel** → 导出完整的核算结果报表

## 📋 技术依赖

- **xlsx.js** (v0.18.5) - Excel文件读取（CDN加载）
- **ExcelJS** (v4.4.0) - Excel文件生成导出（CDN加载）
- 两个库均通过CDN引入，无需安装任何依赖

## ⚠️ 注意事项

1. 系统依赖CDN加载 xlsx.js 和 ExcelJS 库，部署环境需能访问 `cdn.jsdelivr.net`
2. 如在国内服务器部署，CDN访问通常正常；如遇加载失败，可替换为国内CDN镜像
3. 系统所有数据在浏览器本地处理，不会上传到任何服务器
4. 数据通过浏览器 localStorage 缓存，清除浏览器缓存会丢失缓存数据

---

**版本**：v1.30  
**更新日期**：2026年6月  
**作者**：冬阳