---
layout:     post
title:      "css3笔记 元素居中的几个方法"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - css3
    - Meta
---
原文参考 [纯CSS实现垂直居中的几种方法](https://www.cnblogs.com/hutuzhu/p/4450850.html)


html
```
         <div class="wrapper">
           <div class="item"></div>
         </div>
```
当元素为 block时
1. position
```
.wrapper{
    width: 400px;
    height: 400px;
    background-color: #F08080;
    position: relative;
    .item{
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -25px;
        margin-top: -25px;
        
        
        width: 50px;
        height: 50px;
        background-color: #000000;
    }
}

```
2. position + translate : 当 width height 是自动撑开,不是固定值时,有用
```
.wrapper{
    width: 400px;
    height: 400px;
    background-color: #F08080;
    position: relative;
    .item{
        position: absolute;
        left: 50%;// absolute 时, 百分比是父级的 contentWidth + padding
        top: 50%;
        transform: translate(-50%,-50%);
        // 这里的百分比 是自身的宽度和自身高度
        
        width: 50px;
        height: 50px;
        background-color: #000000;
    }
}

```
3. position 的一些算法的应用,
[css3 关于position 感觉非常坑人](https://www.jianshu.com/p/f222304b2547)
```
.wrapper{
    width: 400px;
    height: 400px;
    background-color: #F08080;
    position: relative;
    .item{
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        
        width: 50px;
        height: 50px;
        background-color: #000000;
    }
}
```
4flex
```
.wrapper{
    width: 400px;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #F08080;
    
    .item{
        width: 50px;
        background-color: #000000;
        height: 50px;
    }
}
```
原文参考# [纯CSS实现垂直居中的几种方法](https://www.cnblogs.com/hutuzhu/p/4450850.html)

当元素为 inline或 inline-block 时
5.table-cell 这个是真的不熟悉,压根没用过
```
.wrapper{
    
    display: table-cell;
    vertical-align: middle;
    text-align: center;
    .item{
        display: inline-block;

    }
}
```
6.vertical-aline 和 text-aline 
说实话,这个是真的没弄懂
想理解参考,[CSS深入理解vertical-align和line-height的基友关系](https://www.zhangxinxu.com/wordpress/2015/08/css-deep-understand-vertical-align-and-line-height/)
```
.wrapper{
    width: 400px;
    height: 400px;
    background-color: #F08080;
    font-size: 0;
    text-align: center;
    .item{
        display: inline-block;
        vertical-align: middle;
        width: 100px;
        height: 100px;
        color: white;
        background-color: #000000;
    }
    &::after{
        content: "";
        width: 0;
        height: 100%;
        display: inline-block;
        vertical-align: middle;
    }
}
```
flex 当然也能居中,不过我头一个想到的肯定是这个.
```
.wrapper{
    display: flex;
    justify-content: center;
    align-items: center;
    .item{
    }
}
```
没想到 flex + marigin:auto 也能实现
```
.wrapper{
    display: flex;
    .item{
        margin: auto;
    }
}

```
display:-webkit-box 还有这种属性? 没啥兴趣啊,先记录一下
```
.box9{
    display: -webkit-box;
    -webkit-box-pack:center;
    -webkit-box-align:center;
    -webkit-box-orient: vertical;
    text-align: center
}
```

=======================
复习一下
```
//1.1 中间mid 结构放最下面
//用margin调整边界, width 自动撑大
// 缺点,mid必须放最下面
:root,body{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    position: relative;
    div{
        box-sizing: border-box;
        border: 1px solid black;
        height: 100%;
        position: absolute;
        text-align: center;
        font-size: 40px;
        font-weight: bold;
    }
    .left{
        width: 300px;
        left: 0;
    }
    .right{
        width: 200px;
        right: 0;
    }
    .mid{
        position: static;
        margin-left: 300px;
        margin-right: 200px;
    }
}
//1.2 三个全absolute
:root,body{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    position: relative;
    div{
        box-sizing: border-box;
        border: 1px solid black;
        height: 100%;
        position: absolute;
        text-align: center;
        font-size: 40px;
        font-weight: bold;
    }
    .left{
        width: 300px;
        left: 0;
    }
    .right{
        width: 200px;
        right: 0;
    }
    .mid{
        left: 300px;
        right: 200px;
    }
}
//2.1 float + margin mid 缺点结构必须放最下面,
:root,body{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    div{
        box-sizing: border-box;
        border: 1px solid black;
        height: 100%;
        text-align: center;
        font-size: 40px;
        font-weight: bold;
    }
    .left{
        float: left;
        width: 300px;
    }
    .right{
        float: right;
        width: 200px;
    }
    .mid{
        margin-left: 300px;
        margin-right: 200px;
    }
}

3.双飞翼
:root,body{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    div{
        box-sizing: border-box;
        border: 1px solid black;
        height: 100%;
        text-align: center;
        font-size: 40px;
        font-weight: bold;
        
        float: left;
    }
    .left{
        width: 300px;
        margin-left: -100%;
    }
    .right{
        width: 200px;
        margin-left: -200px;
    }
    .mid{
        width: 100%;
        .mid-item{
            float: none;
            margin-left: 300px;
            margin-right: 200px;
        }
    }
}

圣杯模式

:root,body{
    margin: 0;
    padding: 0;
}
.wrapper{
    height: 100vh;
    padding: 0px 200px 0 300px;
    div{
        box-sizing: border-box;
        border: 1px solid black;
        height: 100%;
        text-align: center;
        font-size: 40px;
        font-weight: bold;
        
        float: left;
    }
    .left{
        width: 300px;
        margin-left: -100%;
        position: relative;
        left: -300px;
    }
    .right{
        width: 200px;
        margin-left: -200px;
        position: relative;
        right: -200px;
    }
    .mid{
        width: 100%;
    }
}

flex
:root,body{
    margin: 0;
    padding: 0;
}
.wrapper{
    display: flex;
    width: 100vw;
    height: 100vh;
    div{
        box-sizing: border-box;
        border: 1px solid black;
        height: 100%;
        text-align: center;
        font-size: 40px;
        font-weight: bold;
    }
    .left{
        order: 1;
        width: 300px;
    }
    .right{
        order: 3;
        width: 200px;
    }
    .mid{
        order: 2;
        flex-grow: 1;
    }
}

```