---
date: '2025-12-10T19:43:44+08:00'
draft: false
title: '记录此博客的诞生'
description: ""
---

# 创建Github仓库
1. 登录 Github，点击右上角的「 + 」按钮，选择「New repository」。
2. 在「Repository name」输入框中输入你的仓库名称，格式为 <username>.github.io，其中 <username> 是你的 Github 用户名。
3. 在「Description」输入框中输入你的仓库描述（可选）。
4. 选择Public
5. 勾选「Initialize this repository with a README」选项，创建一个 README 文件。
6. 点击「Create repository」按钮，创建你的 Github 仓库。


# 本地安装Hugo
1. 前往Hugo的官方Github仓库 release，选择对应的版本进行下载
2. 然后将hugo.exe所在的路径添加到系统的环境变量中。
3. 安装完成后，输入以下命令验证安装是否成功：
`hugo version`

# 创建Hugo站点
1. 在终端或命令提示符中，输入以下命令创建一个新的 Hugo 站点。其中，<site-name> 是你的站点名称，可以根据自己的喜好进行命名。例如我的站点名称为blog，则命令为：
```
hugo new site <site-name>

# 示例
hugo new site blog
```
2. 进入站点目录：
```
cd <site-name>

# 示例
cd blog
```

# 安装主题
1. 进入站点目录，依次使用以下指令：
```
git init -b main

git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```
如果连接不上，可以改为使用ssh密钥克隆：
```
git submodule add -b main git@github.com:nunocoracao/blowfish.git themes/blowfish
```
前提是配置好ssh密钥：
- 打开git bash
- 依次输入以下命令
```
# 生成 SSH 密钥（如果还没有）
ssh-keygen -t ed25519 -C "your_email@example.com"

# 将密钥添加到 ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 复制公钥到剪贴板
cat ~/.ssh/id_ed25519.pub
```
- 在GitHub上配置
    1. 在 GitHub 任意页面的右上角，单击你的个人资料照片，然后单击“ Settings”。

    2. 在边栏的“Access”部分中，单击 “SSH and GPG keys”。

    3. 单击“新建 SSH 密钥”或“添加 SSH 密钥” 。

    4. 在 "Title"（标题）字段中，为新密钥添加描述性标签。 例如，如果使用的是个人笔记本电脑，则可以将此密钥称为“个人笔记本电脑”。

    5. 选择密钥类型（身份验证或签名）。

    6. 在“密钥”字段中，粘贴公钥。

    7. 单击“添加 SSH 密钥”。
2. 进入themes/blowfish目录，找到archetypes和config目录，复制到站点根目录的archetypes和config，提示要替换文件选择「是」
3. 进入站点根目录下的config/_default文件夹中，将languages.en.toml、menus.en.toml两个文件中间的en改为你的默认语言，例如languages.zh-cn.toml、menus.zh-cn.toml
4. 找到hugo.toml文件，可以在开头看到下面这一段，先添加一句在下面hasCJKLanguage = true，用来后面开启正确的汉字计数。

- 取消第五、六行的注释
- 将your_domain.com替换为你的域名，如果没有域名，可以将其替换为你刚刚创建的git仓库的名字：https://<username>.github.io，其中<username>是你的 Github 用户名
- 将en替换为你的默认语言，例如zh-cn表示中文简体
5. 现在回到站点根目录，使用以下命令启动 Hugo 服务器：
```
hugo server
```
6. 在浏览器中访问 http://localhost:1313，可以看到你的站点已经成功运行了。🎉Congratulations! 现在你已经完成了一半了，接下来就是配置你的站点了。

# 配置站点
1. 在站点根目录下，找到config/_default文件夹，打开languages.zh-cn.toml文件自行修改
2. 打开menus.zh-cn.toml文件进行修改，此部分请参考[Blowfish官方文档](https://blowfish.page/zh-cn/docs/getting-started/#%E8%8F%9C%E5%8D%95)
3. 打开params.toml文件进行修改


# 创建文章
新建一篇文章
```
hugo new posts/my-first-post.md
```
此时会在站点目录下的content文件夹中生成posts文件夹，同时在其中生成文件my-first-post.md。使用文件管理器然后用你喜欢的文本编辑器打开这个.md文件

打开后可以看到已经预生成了一些内容。例如title是标题，date是日期，draft是草稿状态（草稿状态如果设置为true的话后面进行渲染后是看不见的，需要设定参数-D，像这样hugo server -D）。改成false。
```
+++
title = 'My First Post'
date = 2024-08-09T20:03:34+08:00
draft = false
+++
```
后续新建文章初始格式不同。
```
---
title: 'My First Post'
date: 2024-08-09T20:03:34+08:00
draft: false
---
```
此篇文章在上面格式头文件上编辑。

# 部署到Github Pages
1. 连接到远程仓库，仅需执行1次
```
git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
```
如果网络不好切换 Git 远程仓库协议为 SSH：
```
# 1. 删除旧的 HTTPS 远程仓库
git remote rm origin

# 2. 添加 SSH 协议的远程仓库
git remote add origin git@github.com:francis329/francis329.github.io.git

# 确认远程仓库已切换为 SSH 协议
git remote -v
# ✅ 正确输出：
# origin  git@github.com:francis329/francis329.github.io.git (fetch)
# origin  git@github.com:francis329/francis329.github.io.git (push)

# 3. 验证 SSH 连接（关键！确保连通）
ssh -T git@github.com
✅ 验证成功输出：Hi francis329! You've successfully authenticated, but GitHub does not provide shell access.
```
2. 推送更新：
```
# ========== 第一步：进入博客根目录，重新构建静态文件 ==========
cd F:\blog

# 清空旧构建产物（可选，但推荐，避免缓存干扰）
rmdir /s /q public && mkdir public

# 构建最新静态文件（包含新增文章）
hugo build --gc --minify

# ========== 第二步：进入 public 目录，执行 Git 操作 ==========
cd F:\blog\public

# 1. 拉取远程最新内容（仅首次/远程有更新时需要，日常可省略）
# git pull --rebase origin main  

# 2. 添加所有修改的文件（新增文章、CSS/JS 等）
git add .

# 3. 提交修改（提交说明写清楚，如「新增文章：我的第二篇博客」）
git commit -m "feat: add new post <你的文章标题>"

# 4. 推送至 GitHub（-u 仅首次推送需要，后续直接 git push 即可）
git push origin main
```