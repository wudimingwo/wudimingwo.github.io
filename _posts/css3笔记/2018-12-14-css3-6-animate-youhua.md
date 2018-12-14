---
layout:     post
title:      "css3笔记6 动画优化,animate"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - css3
    - Meta
---
![image.png](https://upload-images.jianshu.io/upload_images/13637909-a8e469374d04dafe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-c5d46545e4f581b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-5e493316376c7c75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
尽量用transform 因为会减少重排重绘.
董老师说, translate3d 会比 translate 的性能高? 因为 硬件加速?

![image.png](https://upload-images.jianshu.io/upload_images/13637909-976fdae723e31d26.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-e166b95e6c6d0182.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
reverse 从100% 移动到 0%
alternate 当次数多次时, 偶数次会反向移动
alternate-reverse 从100% 开始移动, 偶数次方向移动.

```
.wrapper{
    margin: 200px;
    animation: move 2s ease 2s alternate 2 ;
}

@keyframes move {
    from {
        transform: translate(50px,50px);
    }
    50%{
        transform: translate(100px,50px);
    }
    to{
        transform: translate(100px,100px);
        
    }
}
```
默认位置 translate(0px,0px)
0% 端点1 (50px,50px)
100% 端点2 (100px,100px)
animation-fill-mode:
none时, 在默认位置等待, 结束后回到默认位置
forwards时,在默认位置等待, 根据alternate 结束位置有可能是 0%,100%
结束后不会到默认位置.
backwards时, 在起始位置等待, 在0% 等待(无论是不是reverse)
结束后回到默认位置.
both : 相当于 forwards 和 backwards 结合
在起始位置等待,结束时不回到默认位置.

![image.png](https://upload-images.jianshu.io/upload_images/13637909-b4d27fd0c1cff3ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-128e134418adea7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.item{
    @include base-size(300px,300px,#ff0);
    margin: 200px;
    position: absolute;
}

.wrapper{
    @include base-size(300px,300px,#f00);
    margin: 200px;
    position: absolute;
    animation: move 2s ease 2s alternate infinite;
    &:hover{
        animation-play-state: paused;
    }
}

@keyframes move {
    from {
        transform: translate(50px,50px);
    }
    50%{
        transform: translate(100px,50px);
    }
    to{
        transform: translate(100px,100px);
    }
}
```