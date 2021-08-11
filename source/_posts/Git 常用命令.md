---
title: Git 常用命令
date: 2021-06-8 18:45:01
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
tags: Git
# 文章分类 #
categories: Git 命令
# 文章摘要 #
description: Git 命令
# 文章置顶 #
sticky: 1
---
### 1、git常用命令
|命令名称|作用|
|---|---|
|git config --global user.name 用户名|设置用户签名|
|git config --global user.email 邮箱|设置用户签名|
|git init|初始化本地库|
|git status|查看本地库状态|
|git add 文件名|添加到暂存区|
|git reset HEAD|将 暂存区 里 所有文件 恢复到 工作区|
|git reset HEAD 1.txt|将 暂存区 里 指定文件 恢复到 工作区|
|git commit -m "日志信息" 文件名|提交到本地库|
|git reflog|查看历史记录|
|git reset --hard 版本号|版本穿梭|
|git remote add **仓库别名** **仓库地址**|添加别名为 origin的远程仓库地址|
|git remote -v | 查看添加的远程仓库地址|
|git push **仓库别名** master| push 到别名为 origin的远程仓库|

### 1.1、配置 Git客户端
`git config --global user.name p0ny`
`git config --global user.email p0ny@88.com`

为 Git客户端创建这么一个用户【以上的用户信息是虚拟的，只适用于本地的Git】

![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621832433778-image.png)

验证是否成功？：
在 `C:\Users\xxxx\` 下有这么一个 `.gitconfig` 文件，使用 记事本打开，可以看到如下内容

![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621832600633-image.png)

### 1.2、初始化本地库

![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621837286704-image.png)

在当前项目的根目录下右键 ，然后点击 `Git Bash Here`

然后执行 `git init` 命令

![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621837380100-image.png)


可以看到，会在该目录下生成一个隐藏目录 `.git`

![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621837421469-image.png)


### 1.3、分支的操作
|命令名称|作用|
|---|---|
|git branch 分支名|创建分支|
|git branch|查看分支|
|git checkout 分支名|切换分支|
|git mergge 分支名|把指定的分支合并到当前分支上|

### 1.4、分支合并操作
- 存在 master分支，然后创建一个分支的时候，该分支下自动存在 master分支下的所有文件。

1. 正常合并

   创建一个分支 `hot-fix` 
   
   创建分支成功后，执行命令 `git checkout hot-fix` 
   
   修改 `hot-fix` 下的文件内容，

   然后执行命令 `git add 文件名` 添加到 暂存区
   
   最后执行 `git commit -m "自定义的日志信息" 文件名` 提交到本地库中

   将 `hot-fix` 分支合并到 `master` 分支，
   
   切换至 `master` 分支
   
   然后执行 `git merge hot-fix` 。
   
   将 `hot-fix` 分支合并到当前分支【master】
   
   **综上操作，只是创建一个分支，在该分支下读写文件内容，然后提交到本地库之后，切换至master分支，然后执行命令合并命令**
   **针对于此，只是修改了 新分支下的文件内容**
   
   
2. 合并冲突【依次修改并且提交相同的文件名】、

   已有两个分支 `hot-fix` , `master` 
   
   依次在以上的分支修改相同的文件`hello.txt`并提交
   
   然后切换至 `master` 分支下，执行合并命令 `git merge hot-fix` 
   此时会 提示一下信息：
   
   ```
   Auto-merging hello.txt
   CONFLICT (content): Merge conflict in hello.txt
   Automatic merge failed; fix conflicts and then commit the    result.
   ```
   
   自动 合并失败，这里的解决方式是需要手动编辑保留自己想要的内容
   
   
   ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621847389612-image.png)
   <br>
   <br>
   
   2.1 编辑【保留自己需要的内容】
   
   ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621847777522-image.png)

    <br>
   <br>
   
   2.2 编辑【保留自己需要的内容】
   
      执行添加到 暂存区的命令： `git add hello.txt` 
   
      执行提交本地库命令 ： `git commit -m "merge test"`
   
   ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621847976777-image.png)

   
### 1.5、回滚
1. 【通过版本号回滚】此前已经 往本地库中 提交过，就会有版本号，通过版本号来回滚到文件的某一状态

   命令： `git reset --hard 完整的版本号`


   ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-25/1621927434654-image.png)

2. 【将文件从工作区的红色区域回滚到初始状态，仅对已经被添加到暂存区的文件有效】

   命令： `git checkout -- 文件`
   
   ![初始内容](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-25/1621928976304-image.png)
   
   
   ![修改文件内容](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-25/1621929186135-image.png)
   
   
   最后执行 `git checkout -- hello.txt` ：将 hello.txt 的内容回滚到 初始内容的状态
   
   ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-25/1621929550814-image.png)
   
   
   
 3. 【将文件从工作区的红色区域添加到暂存区，然后将暂存区的文件回滚到工作区的红色区域】
 
 
    新增 `new.txt` 文件

    ![git 检测新增文件](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-25/1621929886477-image.png)

    将文件添加到 暂存区
    
    ![将新增的文件添加到暂存区](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-25/1621930038596-image.png)
    
    
    将暂存区的文件回滚到工作区中
    
    执行 `git reset HEAD new.txt`
    ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-25/1621930227194-image.png)























   

   
   









