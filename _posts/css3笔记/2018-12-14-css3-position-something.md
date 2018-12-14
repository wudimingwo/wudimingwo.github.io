---
layout:     post
title:      "css3笔记 关于 position 感觉非常坑人"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - css3
    - Meta
---
1. position 定位基准问题,从父级的哪里,从子级的哪里?
2.position 如果 加了 absolute 没加 left,right 会怎么样?
3.position left 百分比 的 计算是 基于 父级的 contentWidth 还是  contentWidth + padding?
4.position 和 width margin border 的一种计算, 以及 据此而完成居中的一种方式.

以上几个知识点,之前有碰到过,但一直很模糊, 这次整理一下.

1. position 定位基准问题,从父级的哪里,从子级的哪里?
基准是 从父级的padding和border的边界 开始算,
从子级的margin外侧开始算.

```
  .wrapper{
      width: 300px;
      height: 300px;
      border: 100px solid black;
      padding: 100px;
      background-color: red;
      background-clip: content-box;
      position: relative;
      .son{
          width: 50px;
          height: 50px;
          position: absolute;
          background-color: #00f;
          left: 0;
          top: 0;
      }
  }
```

2.position 如果 加了 absolute 没加 left,right 会怎么样?
此时针对有定位的父子关系作答.
如果有 left,right 值, 包括0, 则子级不受父级padding 影响
如果没有设置left,right值, 则子级受到父级padding影响

```
  .wrapper{
      width: 300px;
      height: 300px;
      border: 100px solid black;
      padding: 100px;
      background-color: red;
      background-clip: content-box;
      position: relative;
      .son{
          width: 50px;
          height: 50px;
          position: absolute;
          background-color: #00f;
//        left:0; 可以进行对比
//        right:0;
      }
  }
```


3.position left 百分比 的 计算是 基于 父级的 contentWidth 还是  contentWidth + padding?

left ,right 的基准值是 contentWdith + padding ;
top,bottom的基准值是 contentHeight + padding;

但这里有个大坑.
当父子都没有定位时,
width,margin,padding 的百分比的基准值都是 父级的 contentWidth
height 的百分比基准值是 父级的contentHeight

而当父有 relative 子有 absolute 时,
计算发生改变.....!
width,margin,padding 的百分比的基准值 都与 left,的基准值相同,
均为 contentWidth + padding左+右;
height 的百分比基准值与top相同,
为 contentHeight + padding 上+下.

这尼玛,今天不是我偶然发现,我上哪知道这个坑啊.

```
  .wrapper{
      width: 300px;
      height: 300px;
      border: 100px solid black;
      padding: 100px 350px;
      background-color: red;
      background-clip: content-box;
      position: relative;
      .son{
          width: 50px;
          height: 50px;
          position: absolute;
          background-color: #00f;
          left: 10%;// left值为 100px
          top: 10%;// top 值为 50px
      }
  }
```


4.position 和 width margin border 的一种计算, 以及 据此而完成居中的一种方式.
绝对定位的其中一种居中方式
```
  .wrapper{
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      width: 100px;
      height: 100px;
      margin: auto;// 这个必须要设上
      
      background-color: #f00;
  }
```
他这里似乎是这么算的,只说x轴的
right 和 left 之间的 距离 = margin-left + margin-right + width
如果确定 right,left, 以及确定 width, 并且设置 margin = auto ,则 会自动计算出margin

如果
```
  .wrapper{
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      width: 100px;
      height: 100px;
      margin: auto;
      margin-left: 100px;
      
      background-color: #f00;
  }
```
会自动计算出 margin-right;
```
  .wrapper{
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      width: auto;
      height: 100px;
      margin: auto;
      margin-left: 100px;
      margin-right: 300px;
      
      background-color: #f00;
  }
```
会扣除margin-left 和 margin-right ,自动算出 width

```
  .wrapper{
      position: absolute;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      width: auto;
      height: 100px;
      margin: auto;
      margin-left: 100px;
      margin-right: 300px;
      border: 1px solid black;
      border-left: 50px solid black;
      border-right: 80px solid black;
      padding-left: 50px;
      padding-right: 80px;
      background-color: #f00;
      background-clip: content-box;
  }
```
如果有border,padding, 则扣除之后,计算width
![image.png](https://upload-images.jianshu.io/upload_images/13637909-7e81052f02af810c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

其实我对css没多少兴趣,不太喜欢这个,
感觉这东西易学难精, 
关键是,看到源码什么的可能性比较少,
我不知其然, 很多东西都感觉是瞎猫碰死耗子.

你麻痹,本来学编程, 以为能掌握信息操作的本领,能节省大量时间精力,
没想到,是我做过的事情中最耗费时间的,
光写这么一篇笔记,就能耗费我两三个小时,你敢信?
我感觉时间流逝速度比之前快太多了,
一天很快就过去, 声明被缩短了.

解决的办法应该是, 学会更快的把思路展示出来, 有没有比敲字更快的文字输出方式?