---
title: ADB无线调试真机
date: 2021-06-27 01:22:57
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
tags: android
# 文章分类 #
categories: ADB 无线调试安卓真机
# 文章摘要 #
description: android adb
# 文章置顶 #
sticky: 1
---
# ADB 无线调试安卓真机

### 准备条件
   1. 一部需要被调试的手机【**小米max2 为例**】【**手机已经root**】
   2. 下载终端模拟器APP `https://p0ny.lanzoui.com/iLcz7qpr7rc` 
   
### 步骤：
0. 准备好 以上条件

1. 打开 手机自带的 `手机管家` 

    ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-26/1624703388149-image.png)


    
2. 点击 `应用管理`
  
    ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-26/1624703432831-image.png)



3. 点击 `权限`
    
![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-26/1624703469380-image.png)

    



4. 然后 给 `终端模拟器` 开启 Root权限
    ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-26/1624703501843-image.png)
    【如果 进去之后**没有终端模拟器**的条目，那么就先运行 终端模拟器app，然后输入命令 `su`回车，然后再返回 `root权限管理`，就会有终端模拟器这个条目了】




5. 然后运行 `终端模拟器APP`

6. 在终端 **分别执行** 以下命令：【一行 代表 一条命令】
    
    ```
    setprop service.adb.tcp.port 5555
    stop adbd
    start adbd
    ```
    
    
7. 然后在终端执行 `ifconfig` 查看手机的IP
    
![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-26/1624708629208-image.png)




8. 在电脑 cmd 中执行命令 ADB远程 `adb connect 手机IP:5555`


   ![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-26/1624702318441-image.png)


   
