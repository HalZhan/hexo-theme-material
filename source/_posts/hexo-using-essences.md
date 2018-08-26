---
title: Hexo博客工具使用精粹
date: 2018-08-25 15:52:07
tags:
- Hexo
- Tools
- Node.js
categories:
- Tools
---
# 主题管理
大多数时候我们需要使用到第三方主题来进行我们博客站点的美化，一般来说都是通过`git clone`的方式拷贝到本地的`themes`目录里。但是这种`clone`到本地的第三方仓库是无法在`git push`时发布到远程仓库的，一旦你在另一台机器上新`clone`了一份自己仓库，你会发现`themes`下所有的内容都丢失了，又要重新`clone`一份，如果你还对第三方主题配置进行过很多修改，重新拷贝一份的话就意味着得重新再做一次修改，这会带来极大的不便。所以，我们需要找到一种方式来解决这些问题。幸好，`git`提供了一种`subtree`（`1.5.2`版本之前有`submodule`）的机制，我们可以利用`fork`+`subtree`的机制来进行第三方库的管理。

- 删除`themes`目录下的`next`文件夹，并将修改`push`到远程。
- 进入`next`主题的`github`首页，`fork`之。
- `fork`完成后，绑定`next`项目为子项目：
```bash
git remote add -f next git@github.com:HalZhan/hexo-theme-next.git
```
- 更新子项目：
```bash
git fetch next master
git subtree pull --prefix=themes/next next master --squash
```
- 从子目录`push`修改到远程仓库：
```bash
git subtree push --prefix=themes/next next master
```
- 提交并发布本地修改到远程仓库：
```bash
git add .
git commit -m "next theme"
git push
```

现在再去远程仓库看`themes/next`目录下就有内容了，而且同子项目的远程仓库保持同步，在主项目的子项目文件目录里所做的修改也可以`push`到子项目的远程。这样就不必担心主题配置丢失了。