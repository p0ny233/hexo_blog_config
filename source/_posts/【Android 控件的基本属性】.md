---
title: 【Android】控件的基本属性
date: 2021-06-02 20:58:01
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
tags: Android Studio
# 文章分类 #
categories: Android
# 文章摘要 #
description: Empty Application
# 文章置顶 #
sticky: 1
---

# Android First Empty Application
#### 控件的基本属性
|属性名|作用|
|--|--|
|android:layout_width|控件的宽度【match_parent、123dp】|
|android:layout_height|控件的高度【match_parent、123dp】|
|android:text|控件文本内容|
|android:textColor|字体颜色【#00000000】|
|android:textSize|字体大小 【40sp】|
|android:textStyle|字体样式【粗体(blod)、italic(斜体)】|
|android:gravity|该控件对象的内容对齐方式【center_vertical(垂直居中)】|

![展示下拉框选项](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-2/1622616032232-image.png)


![下拉框各个选项](https://gitee.com/coder_p0ny/md-nice-markdown_pic/raw/master/2021-6-2/1622616086067-image.png)





### 创建一个 Empty Application 项目

将 路径 `...\项目名\app\src\main\java\com\example\myfirstapp`下的 `MainActivity.java`文件的内容，替换以下内容

`MainActivity.java`

```java
package com.example.myfirstapp;

import androidx.appcompat.app.AppCompatActivity;

import android.annotation.SuppressLint;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        TextView tv_one = findViewById(R.id.tv_one);
        tv_one.setText("Hello World");
        // 使用 Java代码获取控件对象，然后给该对象设置文本内容，
        // 若在xml文件中设置了该控件的文本，运行java代码后会覆盖xml 中的内容
    }
}
```

<br>
<br>



将路径 `...\项目名\app\src\main\res\layout\` 下的 `activity_main.xml` 文件的内容  替换成  以下内容

`activity_main.xml`
```xml
<?xml version="1.0" encoding="utf-8"?><!--<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"-->
<!--    xmlns:app="http://schemas.android.com/apk/res-auto"-->
<!--    xmlns:tools="http://schemas.android.com/tools"-->
<!--    android:layout_width="match_parent"-->
<!--    android:layout_height="match_parent"-->
<!--    tools:context=".MainActivity">-->

<!--    <TextView-->
<!--        android:layout_width="wrap_content"-->
<!--        android:layout_height="wrap_content"-->
<!--        android:text="Hello World!"-->
<!--        app:layout_constraintBottom_toBottomOf="parent"-->
<!--        app:layout_constraintLeft_toLeftOf="parent"-->
<!--        app:layout_constraintRight_toRightOf="parent"-->
<!--        app:layout_constraintTop_toTopOf="parent" />-->

<!--</androidx.constraintlayout.widget.ConstraintLayout>-->
<!--此 XML 文件定义了 activity 界面 (UI) 的布局。它包含一个 TextView 元素，其中具有“Hello, World!”文本-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:gravity="center_vertical"
        android:id="@+id/tv_one"
        android:layout_width="843dp"
        android:layout_height="400dp"
        android:text="看不到我"
        android:textColor="#FF000000"
        android:textSize="90sp"
        android:textStyle="bold">
        <!--
        android:layout_width="match_parent"
            TextView 控件 的宽度 由 LineLayout容器决定，LineLayout容器多宽，TextView控件就有多宽

        android:layout_width="wrap_content"
            TextView 控件 的宽度 由 TextView控件的内容决定。
        同理 高度也是一样的

        android:id="@+id/tv_one"
                该属性的作用是，让 java 代码可以根据 id 属性值 获取 控件对象


        android:layout_width="200dp"
            该属性值可以使用数字来 赋值

                参数 的值 按住 ctrl 不放 鼠标左键点击
                可以看到有三个参数值，其中一个【fill_parent】已经被弃用的

                剩余两个参数值分别是：
                    1. wrap_content : 根据 TextView里面控件的内容 分配
                    2. match_parent ： 大小根据取决于 LinearLaout 容器
                    3. fill_parent ： 已经过时


        android:textColor="#00000000"
            设置字体颜色
            前面两个 零含义：颜色的透明度 ，00 为纯透明 FF为 不透明
            依次往后两个 零：代表 R(00)G(00)B(00) 红绿蓝

        android:textStyle="bold"
            设置字体
            normal ：无效果
            bold ：  粗体
            italic ：斜体

        android:gravity="center_vertical"
            该控件对象的内容的对齐方式
        -->

    </TextView>

</LinearLayout>
```


