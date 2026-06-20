# 山洞中学个人主页 —— 使用说明

## 这是什么

一个会"自动检测"图片的网站。你只需要把图片丢进 `images` 文件夹推送到 GitHub，
GitHub Actions 会自动扫描文件夹、生成图片清单（`images/list.json`），网站读取
这个清单来展示所有图片 —— **不需要手动写文件名，1000多张也没问题**。

---

## 第一次设置步骤（只需做一次）

### 1. 创建 GitHub 仓库
- 登录 GitHub，新建一个仓库（Repository）
  - 如果想用 `用户名.github.io` 作为网址，仓库名必须正好是 `你的用户名.github.io`
  - 否则用任意仓库名也可以，网址会是 `你的用户名.github.io/仓库名`

### 2. 上传文件
把这个文件夹里的全部内容（包括隐藏的 `.github` 文件夹）上传到仓库的 `main` 分支：

```
仓库根目录/
├── index.html
├── .github/
│   └── workflows/
│       └── deploy.yml
└── images/
    └── list.json   (占位文件，会被自动更新)
```

**⚠️ 重要：`.github` 文件夹名字前面有个点，是隐藏文件夹。**
如果你用网页拖拽上传，记得也要把这个文件夹传上去（用 git 命令行上传不会有这个问题）。

推荐用 git 命令行操作：
```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main
```

### 3. 开启 GitHub Pages
1. 打开仓库 → 点 **Settings**（设置）
2. 左侧菜单找到 **Pages**
3. 在 "Build and deployment" 下的 **Source** 选择 **GitHub Actions**（注意不是 "Deploy from a branch"）

### 4. 等待自动部署
- 打开仓库的 **Actions** 标签页，能看到一个工作流正在运行（绿色对勾代表成功）
- 完成后，回到 Settings → Pages，顶部会显示你的网址，例如：
  `https://你的用户名.github.io/仓库名/`

---

## 以后怎么加图片（全自动）

1. 把新图片拖进本地的 `images` 文件夹（支持 jpg / jpeg / png / gif / webp / bmp / svg）
2. 推送到 GitHub：
   ```bash
   git add .
   git commit -m "添加新图片"
   git push
   ```
3. 完事了。GitHub Actions 会自动：
   - 扫描 `images` 文件夹里所有图片
   - 生成最新的 `images/list.json`
   - 重新部署网站

整个过程 1-2 分钟左右，刷新网站就能看到新图片，**不需要手动改任何代码**。

---

## 网站功能

- 顶部左侧「联系方式」按钮 + 右侧导航「联系」：点击弹出电话和QQ
  - 电话：16768413020
  - QQ：1900940676
- 中间：图片网格展示，点击任意图片可放大查看
- 图片很多时自动分批加载（每次60张），有「加载更多」按钮，避免一次性卡顿
- 底部：山洞中学 版权信息

## 如果想本地预览效果（不推送也能看大概样子）

`images/list.json` 是空数组 `[]`，本地打开 `index.html` 只会看到"暂未检测到图片"的提示，
这是正常的——清单需要由 GitHub Actions 在云端生成。如果想本地测试图片展示效果，
可以手动把文件名填进 `images/list.json`，例如：

```json
["photo1.jpg", "photo2.png"]
```

但这只是本地测试用，正式上线后清单会被 Actions 自动覆盖，无需手动维护。
