---
title: Windows常用技巧
date: 2021-05-29 19:14:20
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
tags: Windows
# 文章分类 #
categories: Windows常用技巧
# 文章摘要 #
description: Windows常用技巧
# 文章置顶 #
sticky: 1
---

#### 1. 手动驱动备份【需要管理员权限】

> 参考：`http://www.baiyunxitong.com/jiaocheng/4786.html` 

使用 win+r  输入 cmd，跳出命令提示符窗口然后输入以下命令，来提升为 管理员权限

`runas /user:administrator cmd` 

如果出现

![image-20210301000731586](https://gitee.com/coder_p0ny/Typora_img/raw/master/Java/img/cmd%E6%8F%90%E5%8D%87%E4%B8%BA%E7%AE%A1%E7%90%86%E5%91%98%E6%9D%83%E9%99%90%E9%94%99%E8%AF%AF.png)

* 很大可能是 Administrator账户的密码为空的。

    解决方式：

    1. win+r 输入 `compmgmt.msc` 

        ![image-20210301001027050](https://gitee.com/coder_p0ny/Typora_img/raw/master/Java/img/%E6%8F%90%E5%8D%87%E7%AE%A1%E7%90%86%E5%91%98%E6%9D%83%E9%99%90%E8%A7%A3%E5%86%B3%E6%96%B9%E5%BC%8Fstep1.png)

         

    2.  点击 ”用户“

         ![image-20210301001239472](https://gitee.com/coder_p0ny/Typora_img/raw/master/Java/img/%E6%8F%90%E5%8D%87%E7%AE%A1%E7%90%86%E5%91%98%E6%9D%83%E9%99%90%E8%A7%A3%E5%86%B3%E6%96%B9%E5%BC%8Fstep2.png)

         

    3. 右键点击  “设置密码”

        ![image-20210301001616934](https://gitee.com/coder_p0ny/Typora_img/raw/master/Java/img/%E6%8F%90%E5%8D%87%E7%AE%A1%E7%90%86%E5%91%98%E6%9D%83%E9%99%90%E8%A7%A3%E5%86%B3%E6%96%B9%E5%BC%8Fstep3.png)

         

    4. 效果图

        ![image-20210301001820364](https://gitee.com/coder_p0ny/Typora_img/raw/master/Java/img/%E6%8F%90%E5%8D%87%E7%AE%A1%E7%90%86%E5%91%98%E6%9D%83%E9%99%90%E8%A7%A3%E5%86%B3%E6%96%B9%E5%BC%8F%E6%95%88%E6%9E%9C%E5%9B%BE.png)

         

最后使用命令 `dism /online /export-driver /destination:目标文件夹路径` 

![image-20210301002109435](https://gitee.com/coder_p0ny/Typora_img/raw/master/Java/img/cmd%E6%89%8B%E5%8A%A8%E5%A4%87%E4%BB%BD%E9%A9%B1%E5%8A%A8.png)



#### 2. 手动还原驱动命令【需要管理员权限】

`dism /online /Add-Driver /Driver:目标文件夹路径 /Recurse` 

![image-20210301002630148](https://gitee.com/coder_p0ny/Typora_img/raw/master/Java/img/%E8%BF%98%E5%8E%9F%E9%A9%B1%E5%8A%A8%E5%91%BD%E4%BB%A4.png)





































