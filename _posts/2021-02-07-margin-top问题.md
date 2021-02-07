---
layout:     post
title:      margin-top问题
subtitle:    "\"制作一个自己想要的功能的应用\""
date:       2021-02-07
author:     Rick
header-img: img/2021-02-07/title.jpg
catalog: true
tags:
    - 前端
	- css
---

> 做为后端程序员，难免会有一些开发前端页面的工作。所以本文记录了作者在实际工作中遇到的问题和解决方法，相较于专业的前端开发人员来说会比较基础，但是适用于后端开发人员，但是平时工作中会略带前端开发工作的程序员。

## 前言

由于公司的业务需求，需要移动端做几个页面，但是移动端工作已经排满，所以最后决定这几个页面由H5实现。这个工作最后落到的我的头上。既然派发了任务，那就一定要完成，虽然一直在做Java的开发工作，但是也会接触VUE的开发工作，只是前端开发并没有专业前端那么熟练。本文记录了在工作中实际遇到的问题以及解决方案。

## margin-top会从子元素转移到父元素

在开发过程中，遇到了一个非常诡异的事情。



![](https://ren88122246.github.io/img/2021-02-07/01.png)

这样也许看的不清楚，我把body的background调整为红色。

![](https://ren88122246.github.io/img/2021-02-07/02.png)

很奇怪啊，我的margin-top标记的地方是4个卡片元素，为什么下面三个卡片显示正常，而第一个卡片显示的却是有问题的呢？

![](https://ren88122246.github.io/img/2021-02-07/03.png)

![](https://ren88122246.github.io/img/2021-02-07/04.png)

所以为什么第一张卡片的margin-top就好像作用在了entrance这个class上呢？

于是上网查找资料，找到了原因：**父元素的第一个子元素的上边距margin-top如果碰不到有效的border或者padding.就会不断一层一层的找自己“领导”(父元素，祖先元素)的麻烦。**

例如：我们现在有一个页面



<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>margin-top的问题</title>
    <style type="text/css">
        *{
            margin:0px;
            padding: 0px;
        }
        .outside{
            width:200px;
            height:200px;
            background-color: blue;

        }
        .inside{
            /*margin-top:20px;*/
            width:100px;
            height:100px;
            background-color: #000;
        }
    </style>
</head>
<body>

   <div class="outside">
       <div class="inside">
       </div>
   </div>
</body>
</html>



```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>margin-top的问题</title>
    <style type="text/css">
        *{
            margin:0px;
            padding: 0px;
        }
        .outside{
            width:200px;
            height:200px;
            background-color: blue;

        }
        .inside{
            /*margin-top:20px;*/
            width:100px;
            height:100px;
            background-color: #000;
        }
    </style>
</head>
<body>
   <div class="outside">
       <div class="inside">
       </div>
   </div>
</body>
</html>
```

