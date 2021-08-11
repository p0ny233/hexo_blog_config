---
title: Python 解压缩文件【只能压缩文件夹】
date: 2021-05-29 17:28:19
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
tags: Python
# 文章分类 #
categories: Python
# 文章摘要 #
description: Python_解压缩文件【只能压缩文件夹】
# 文章置顶 #
sticky: 1
---
### Python 压缩文件夹，解压文件
```python
import shutil

"""
base_name : 压缩后的压缩文件名
format : 压缩格式：如：`zip`, `tar`, `gztar`, `bztar`, or `xztar`
root_dir : 要压缩哪个文件夹就选哪个文件夹 【只能是文件夹，不可以是文件，否则会 抛出 NotADirectoryError】 
"""

# 压缩文件
shutil.make_archive('2',format='zip',root_dir='./Analyse')
# 第一个参数是 base_name
# 第二个参数是 format
# 第三个参数是 root_dir

print("压缩完成")



# 解压文件
"""
filename：压缩包文件

extract_dir：是目标目录的名称，其中包含存档文件，打开包装。如果未提供，则使用当前工作目录,
 
format：是压缩包格式，如果没有提供那么会根据文件扩展名进行解压
"""

shutil.unpack_archive('2.zip',extract_dir='2')
# 会将压缩包的内容解压出来，然后放进一个名称为 2 的文件夹中，
# 如果没有给extract_dir提供，那么会从压缩包中拿出放到当前目录下
# 建议给 extract_dir 提供存放的目录

print("解压成功")
```


![](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-5-29/1622280481947-image.png)
