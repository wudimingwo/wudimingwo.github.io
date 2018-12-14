---
layout:     post
title:      "css3 perspective-origin 和perspective 笔记"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - bootStrap
    - Meta
---

自己研究了半天,只得出这些
```
perspective-origin是个什么属性?
发现 perspecive-origin只由 父级的决定
但 perspective 属性,
会受到 父级影响,也会受到子级影响,
两者不是 覆盖效果,而是叠加效果.
同样的数值,在父级和子级的设置效果不同.
两者的叠加不是加法.
同样的数据,子级的视距似乎比父级的视距要小,
也就是3d效果会更明显
```
还是搜索来的方便
大神果然是大神
[好吧，CSS3 3D transform变换，不过如此](https://www.zhangxinxu.com/wordpress/2012/09/css3-3d-transform-perspective-animate-transition/)
[CSS3 3D transform视角属性perspective（Y旋转角度一致）实例页面](https://www.zhangxinxu.com/study/201209/transform-perspective-same-rotate.html)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-d08306bfffbb9072.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

大概是明白了.
perspective-origin 只能设置在 父级上,并且只能影响子级,不能影响自身
perspecive: 500px 只能设置在 父级上,并且只能影响子级,不能影响自身
perspective-origin 只会影响 perspecitve:500px 而不会影响 transform:perspecitive(500px)

transform:perspective(500px) 只会影响自身,
默认的perspecive-origin 是自身的center
且该 perspecive-origin 是没有属性可以调整的.

最恶心的是,
perspecive:500px , 和 transform:perspective(500px) 是互相叠加的!
而叠加法则还不清楚.
perspecive:500px,transform:perspective(0 不设置) 和
perspecive:500px,transform:perspective(100000px) 效果很相似.
而
perspecive:0 不设置,transform:perspective(500px) 和
perspecive:100000px,transform:perspective(500px) 效果很相似.
也就是两者是互为基础,
但perspecive:500px,transform:perspective(500px) 的叠加
和perspecive:1000px 的效果不同
和transform:perspective(1000px) 的效果也不同

更恶心的是, 如果父级perspective-origin 不是默认值, 则两者叠加完全,嗯,难以理解?
难以预测?

偶然发现,这个效果是相似的.
```
.wrap1{
    perspective: 500px;
    .item1{
        transform: perspective(500px) rotateY(45deg);
    }
}
.wrap2{
    .item2{
        transform:perspective(250px) rotateY(45deg);
    }
}
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-de621731e9d33396.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
根据测试得到以下几个数据 叠加的效果和后面的效果基本一致.
pers: 500 tranper : 500 和 transper 250
pers: 500 tranper : 400 和 transper 221
pers: 500 tranper : 300 和 transper 188
pers: 500 tranper : 200 和 transper 143

pers: 800 tranper : 800 和 transper 400
pers: 800 tranper : 400 和 transper 265
从上面的数据能得出公式嘛? 哎呀,感觉好浪费时间, 
这玩意纯属靠猜, 我大概蒙出来了, 有点像小时候的发现数学规律
假设
pers:x  tranper: y transpre: z
z = y / (x + y) * x
前提条件 x < y 如果 x > y 只需要把x,y的位置换一下就可以.
或者这么写更好理解
z/max = min/(min + max);
我在想,花了3,4个小时得出这么个东西,到底值不值?
不值, 不是说该知识点没有用,(确实可能用不上)
而是说,自己这么实验加猜测,实在是太浪费时间了.
应该找教材.妈了个比的.
但上面的公式很有局限,
仅限于 perspective-origin : center的情况.
至于perspective-origin : 其他数值; 的情况,
我就不能靠测试几个模拟的方式猜了,根本无法模拟.

===========
我不想提问题,每次想回答提出来的问题,都要浪费好长时间.
可还是要问一下,大不了就不回答完事.

perspective-origin 是否和 transform-origin 一样, 随着元素转换空间位置,
一起变化?
应该会吧.
假设不会, 那么translate 会原理 perspective-origin, 会出现变形才对.
当然这是针对父级元素而言的.
如果是子级元素,如果translate 且不是靠 trans:pers 来生成景深, 则会发生明显的视觉上的变形.

哎呀,说得好不清楚,就这样吧.
这一段,另起一个文章吧.