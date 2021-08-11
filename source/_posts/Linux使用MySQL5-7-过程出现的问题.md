---
title: Linux使用MySQL5.7 过程出现的问题
date: 2021-02-16 16:23:36
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
tags: MySQL
# 文章分类 #
categories: 数据库
# 文章摘要 #
description: Linux使用MySQL5.7 过程出现的问题
# 文章置顶 #
sticky: 1
---
# Linux使用MySQL5.7 过程出现的问题
1. 执行修改密码命令  
`alter user user() identified by 'root';`  
或者  
`set password for root@localhost = password('root');`   

    出现错误信息  
    `ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
    `
    
    信息上说明设置的密码是弱级别的，需要提高密码强度。

    
   **解决：**
    -  将安全级别设置为 `LOW` ,如果向将密码设置为 `root` ,那么还需要更改密码长度
    
        【**默认密码长度为8**，可以设置为其它值，最小4位】  
        设置安全级别：
        `set global validate_password_policy=LOW;`  
        
        更改密码默认长度： 
        `set global validate_password_length=4;`
        
        执行以上两条命令之后就可以将密码设置为 **长度为4 的弱密码 比如 root**
        


2. 安装MySQL数据库之后使用命令 `mysql -uroot -p` 让你输入，但是不知道密码怎么办？  
    - **方式 1.** 可直接跳过密码进行登陆   
      1. 修改 `vi /etc/my.cnf` 文件
      2. 在该文件下的 **[mysqld]模块** 添加以下代码  
      `skip-grant-tables# 忽略mysql权限问题，直接登录`  
      如图：
      
          ![绕过密码登陆](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-24/1621832433778-image.png)
          
          然后执行命令 `systemctl restart mysqld` 重启mysql服务
      再次执行`mysql-uroot -p` 回车  
      然后提示**输入密码的时候直接敲回车**即可
      
    - **方式 2.** 查看默认初始密码  
    
        **注意：**：【如果是第一次安装MySQL可以忽略】之前有安装过MySQL数据库并且再次安装MySQL的数据库的需要先将 `/var/log/mysqld.log` 这个文件删除  
        **总之就是需要保证没有这个文件 `/var/log/mysqld.log`**
    
        然后启动MySQL服务`systemctl start mysqld` 
        此时就会生成此文件 `/var/log/mysqld.log`  
        然后执行命令 `grep 'temporary password' /var/log/mysqld.log`  
        就可以看到如图所示的内容：
    
        ![显示默认密码](https://imgkr2.cn-bj.ufileos.com/33c2adc2-ab99-409d-8e64-18c4f86393fa.png?UCloudPublicKey=TOKEN_8d8b72be-579a-4e83-bfd0-5f6ce1546f13&Signature=%252BA5dfGEoYYfEDezpdgfIpHqho5w%253D&Expires=1613549719)

        `mZk=kau!p0Zq` 就是默认密码，使用命令`mysql -uroot -p`,提示输入登陆密码的时候再输入该默认密码，即可登陆成功
