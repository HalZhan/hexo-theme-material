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
大多数时候我们需要使用到第三方主题来进行我们博客站点的美化，一般来说都是通过`git clone`的方式拷贝到本地的`themes`目录里。但是这种`clone`到本地的第三方仓库是无法在`git push`时发布到远程仓库的，一旦你在另一台机器上新`clone`了一份自己仓库，你会发现`themes`下所有的内容都丢失了，又要重新`clone`一份，如果你还对第三方主题配置进行过很多修改，重新拷贝一份的话就意味着得重新再做一次修改，这会带来极大的不便。所以，我们需要找到一种方式来解决这些问题。幸好，`git`提供了一种`submodule`的机制，我们可以利用这个机制来进行第三方库的管理。

```bash
git submodule add https://github.com/theme-next/hexo-theme-next themes/next
```

这个命令会让`git`将第三方主题拷贝到`themes/next`目录下，同时将其纳入成为自己的`submodule`。我们可以使用如下命令查看所有`submodule`的状态：
```bash
git submodule status
```
![](http://halzhan.github.io/static/pic/submodule_status.png)


