---
title: 从Gitee仓库拉取原有的 blog
date: 2021-06-01 9:37:14
# 文章出处名称 #
from: 原创
# 文章出处链接 #
url:
# 文章作者名称 #
author: p0ny
# 文章作者签名 #
about: 一穷二白
# 文章作者头像 #
avatar: 
# 是否开启评论 #
comments: true
# 文章标签 #
tags: Git hexo
# 文章分类 #
categories: Git
# 文章摘要 #
description: 从Gitee仓库拉取原有的 blog
# 文章置顶 #
sticky: 1
---
## 从Gitee仓库拉取原有的 blog
>1. `git clone https://gitee.com/coder_p0ny/blog.git` 拉取项目
>2. 另外新建一个文件夹作为 blog 的根目录，然后该目录下是空白的，直接在该目录下 打开 git终端，然后输入命令 `hexo init` 初始化 hexo,生成 blog 模板，然后再将第一步拉取的blog中的所有文件复制到新建的文件夹中，替换所有相同的文件
>3. 然后执行命令 `hexo s --debug`  开启服务
>4. 浏览器访问 `http://localhost:4000` 即可