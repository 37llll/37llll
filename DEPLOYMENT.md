# 🚀 GitHub 个人主页部署指南（纯命令行版）

## 前置要求

确保已安装以下工具：
- `git` - 版本控制（macOS 通常已预装）
- `gh` - GitHub CLI

### 安装 GitHub CLI

```bash
# 使用 Homebrew 安装（如果没有 Homebrew，先安装：/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"）
brew install gh
```

## 步骤 1: 登录 GitHub CLI

```bash
# 登录 GitHub（会打开浏览器进行认证）
gh auth login

# 选择 GitHub.com
# 选择 HTTPS
# 选择 Yes 来认证 Git
# 选择 Login with a web browser
```

## 步骤 2: 初始化 Git 并提交文件

```bash
# 进入项目目录
cd /Users/yulong/Desktop/project/github_page_beauty_project

# 初始化 Git 仓库
git init

# 添加所有文件
git add .

# 提交文件
git commit -m "Add beautiful GitHub profile page"

# 设置主分支为 main
git branch -M main
```

## 步骤 3: 创建同名仓库并推送

**重要**：仓库名必须与你的 GitHub 用户名完全一致（例如：`37llll`）

```bash
# 创建公开仓库并推送代码（替换 37llll 为你的用户名）
gh repo create 37llll --public --source=. --remote=origin --description="My GitHub profile page" --push

# 如果上面的命令失败，可以分步执行：
# gh repo create 37llll --public --description="My GitHub profile page"
# git remote add origin https://github.com/37llll/37llll.git
# git push -u origin main
```

## 步骤 4: 配置 GitHub Actions 权限

```bash
# 设置 Actions 工作流权限为读写
gh api repos/37llll/37llll/actions/permissions \
  --method PUT \
  --field enabled=true \
  --field allowed_actions=all

# 或者使用更详细的配置
gh api repos/37llll/37llll/actions/permissions \
  --method PUT \
  -f enabled=true \
  -f allowed_actions=all \
  -f default_workflow_permissions=write
```

## 步骤 5: 手动触发蛇形动画生成

```bash
# 触发 GitHub Actions 工作流
gh workflow run "Generate Snake Animation" --repo 37llll/37llll

# 查看工作流运行状态
gh run list --workflow="Generate Snake Animation" --repo 37llll/37llll

# 查看最新运行日志（实时）
gh run watch --repo 37llll/37llll
```

## 步骤 6: 验证部署

```bash
# 查看仓库信息
gh repo view 37llll/37llll

# 在浏览器中打开仓库
gh repo view 37llll/37llll --web
```

## 步骤 6.5: ⚠️ 重要！启用个人主页显示

**这是关键步骤！** GitHub 不会自动将仓库 README 显示在个人主页上，需要手动启用：

1. 在浏览器中打开仓库页面：`https://github.com/37llll/37llll`
2. 在仓库页面右侧找到 **"Share to profile"** 按钮（或类似的提示框）
3. 点击该按钮，将 README 内容显示在你的个人主页上
4. 如果没有看到按钮，可以尝试：
   - 刷新页面
   - 检查仓库是否为公开（Public）
   - 确认仓库名与用户名完全一致

完成后，访问 `https://github.com/37llll` 就能看到美化的个人主页了！

## 步骤 7: 自定义内容（可选）

编辑 `README.md` 文件，然后提交：

```bash
# 编辑文件（使用你喜欢的编辑器）
# vim README.md
# 或
# code README.md

# 提交更改
git add README.md
git commit -m "Update personal information"
git push
```

需要填写的内容：
1. **个人信息** - 在 `About Me` 部分
2. **技能图标** - 在 `Tech Stack` 部分添加技能徽章
3. **项目展示** - 在 `Featured Projects` 部分添加项目卡片
4. **社交媒体** - 在 `Connect with Me` 部分添加链接

## 🎨 自定义颜色主题

使用命令行批量替换颜色：

```bash
# 替换为橙色主题
sed -i '' 's/00ff88/ff6b35/g' README.md

# 替换为红色主题
sed -i '' 's/00ff88/ff1744/g' README.md

# 替换为蓝色主题
sed -i '' 's/00ff88/2196f3/g' README.md

# 替换为紫色主题
sed -i '' 's/00ff88/9c27b0/g' README.md

# 替换为粉色主题
sed -i '' 's/00ff88/e91e63/g' README.md

# 提交颜色更改
git add README.md
git commit -m "Update color theme"
git push
```

## ✅ 完成！

访问 `https://github.com/37llll` 查看你的美化主页！

---

## 常用命令速查

```bash
# 查看工作流状态
gh run list --repo 37llll/37llll

# 重新触发工作流
gh workflow run "Generate Snake Animation" --repo 37llll/37llll

# 查看仓库文件
gh repo view 37llll/37llll --web

# 拉取最新更改
git pull origin main

# 查看 Git 状态
git status
```

---

**提示**：
- 所有统计数据都是实时更新的
- 蛇形动画每天自动更新一次（通过 cron 任务）
- 访问计数器会自动记录访问次数
- 如果 Actions 没有自动运行，使用 `gh workflow run` 手动触发
