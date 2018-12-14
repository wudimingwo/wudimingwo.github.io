---
layout:     post
title:      "css3笔记4 盒模型,flex弹性布局,三列布局"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - css3
    - Meta
---

![image.png](https://upload-images.jianshu.io/upload_images/13637909-e9ec9ef08ea5bf27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
咦,感觉这个层次示意图,比较值钱! 单独放一下.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-90fc093d92220c70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
触发怪异模式的条件
1. 去掉<!DOCTYPE html>
2. 在ie6,以下运行
基本看不到了?
w3c: width = content-width;             box-sizing: content-box;
ie : width = content-width +  border + padding;            box-sizing: border-box;
box-sizing 模式时,如果border + padding 超过 width 则 width 会失效.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-35123606dca84065.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.item {
    box-sizing: border-box;
    width: 300px;
    height: 300px;
    background-color: #F08080;
    overflow-x: scroll;
    //垂直方向顯示滾動條
    .son {
        width: 400px;
        height: 200px;
        background: linear-gradient(to left, blue, red);
    }
}
```
如果想设置滚动条样式怎么办?


![image.png](https://upload-images.jianshu.io/upload_images/13637909-7188082ab7053a3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
    textarea {
        width: 400px;
        height: 200px;
        background: linear-gradient(to left, blue, red);
        // 只能橫向拖動
        resize: horizontal;
        //只能纵向拖动
        resize: vertical;
        // 双向
        resize: both;
    }
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-822e558460385c08.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
三列布局
第一种 绝对定位
html
```
      <div class="wrapper">
        <div class="left"></div>
        <div class="mid"></div>
        <div class="right"></div>
      </div>
```
css
```
*{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    position: relative;
    .left{
        position: absolute;
        left: 0;
        width: 300px;
        height: 100%;
        background-color: #F08080;
    }
    .mid{
        position: absolute;
        left: 300px;
        right: 300px;
        height: 100%;
        background-color: #000;
    }
    .right{
        position: absolute;
        right: 0;
        width: 300px;
        height: 100%;
        background-color: #f00;
    }
}

```
利用 vw 和 calc()?
```
*{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    font-size: 0;
    .left{
        display: inline-block;
        width: 300px;
        height: 100%;
        background-color: #F08080;
    }
    .mid{
        display: inline-block;
        width: calc(100vw - 600px);
        height: 100%;
        background-color: #000;
    }
    .right{
        display: inline-block;
        width: 300px;
        height: 100%;
        background-color: #f00;
    }
}
```
float方式,
要注意html的顺序
html
```
      <div class="wrapper">
        <div class="left"></div>
        <div class="right"></div>
        <div class="mid"></div>
      </div>
```
scss
```
*{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    .left{
        float: left;
        width: 300px;
        height: 100%;
        background-color: #F08080;
    }
    .mid{
        margin: 0 300px 0 300px;
        height: 100%;
        background-color: #000;
    }
    .right{
        float: right;
        width: 300px;
        height: 100%;
        background-color: #f00;
    }
}
```
参考[三列布局实现4种方法](https://blog.csdn.net/sinat_30443713/article/details/78078650);
双侧翼,还真是学习了.
这样能够保证先加载中间的主要内容
html
```
         <div class="wrapper">
           <div class="mid">
             <div class="mid-item">mid</div>
           </div>
           <div class="left">left</div>
           <div class="right">right</div>
         </div>
```

scss
```
*{
    margin: 0;
    padding: 0;
}
.wrapper{
    width: 100vw;
    height: 100vh;
    
    .mid{
        float: left;
        width: 100%;
        height: 100%;
        .mid-item{
            margin: 0 300px;
            height: 100%;
            background-color: #A71D5D;
        }
    }
    .left{
        float: left;
        width: 300px;
        margin-left: -100%;
        height: 100%;
        background-color: #F08080;
    }
    .right{
        float: left;
        height: 100%;
        width: 300px;
        background-color: pink;
        margin-left: -300px;
    }
}
```
不用float 用display : inline-block行不行?
这才发现 float 和 inline-block 有个挺大的区别
float 时, left 通过 margin-left 向左移动时, right 会被 mid卡主.
inline-block 时, left通过margin-left 向左移动时, right会跟着left 一起移动.
双侧翼很巧妙!
css每个单句都不怎么难, 但复合使用不太好掌握.

圣杯模式
html
```
         <div class="wrapper">
           <div class="mid">mid</div>
           <div class="left">left</div>
           <div class="right">right</div>
         </div>
```
scss
```
  .wrapper{
      padding: 0 100px 0 150px;
      .mid{
          float: left;
          width: 100%;
          height: 100px;
          background-color: #A71D5D;
          opacity: 0.3;
          text-align: center;
      }
      .left{
          float: left;
          margin-left: -100%;
          width: 150px;
          height: 100px;
          background-color: #F08080;
          opacity: 0.3;
          position: relative;
          left: -150px;
      }
      .right{
          margin-left: -100px;
          float: left;
          height: 100px;
          width: 100px;
          background-color: pink;
          opacity: 0.3;
          text-align: right;
          position: relative;
          right: -100px;
      }
  }
```
这个就更巧妙了,我真实佩服的五体投地.
首先, width 和 margin 的百分比都是 针对父级的宽度, 这个宽度是 content-width
不包括padding部分. 
所以根据padding 预留出左右的空间.
根据float 的特性, 左右会折行到下一行,
通过margin-left 可以让float元素 之间重叠, 让他们回到同一行.
但重要的是, left 的移动,right不会跟着移动,这和inline-block 不同.
最后用relative最后再调一次位置.
实在是精妙.
[css3 关于position 感觉非常坑人](https://www.jianshu.com/p/f222304b2547)
关于 百分比的基准值,这里有写.

用flex
html
```
         <div class="wrapper">
           <div class="left">left</div>
           <div class="mid">mid</div>
           <div class="right">right</div>
         </div>
```
scss
```
.wrapper{
    display: flex;
    
    .left{
        width: 200px;
        height: 50px;
        background-color: #99CDFF;
    }
    .mid{
        flex-grow: 1;
        height: 50px;
        background-color: #F08080;
    }
    .right{
        width: 300px;
        height: 50px;
        background-color: #C0A16B;
    }
    
}
```
确实很方便, 问题来了, 如果我想让mid 先加载怎么办?
利用order
html
```
         <div class="wrapper">
           <div class="mid">mid</div>
           <div class="left">left</div>
           <div class="right">right</div>
         </div>
```
scss
```
.wrapper{
    display: flex;
    
    .left{
        width: 200px;
        height: 50px;
        background-color: #99CDFF;
        order: 1;
    }
    .mid{
        order: 2;
        flex-grow: 1;
        height: 50px;
        background-color: #F08080;
    }
    .right{
        order: 3;
        width: 300px;
        height: 50px;
        background-color: #C0A16B;
    }
}
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-c0673b9178cf6ee3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-7ba7ccaf2249e96f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-1a54d5304cdd1679.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
设置在子元素,伸缩项目上.
多余的部分会进行拉伸填充,
每个子元素的默认是为0, 默认是不会拉伸填充,不变形.
如果设置,则按照比例,分割空间分配.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-a6d6a0c6b3c29e01.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
设置在子元素,伸缩项目上.
父级限定宽\高时, 子元素的宽/高之合 大于 父级时, 多出来的部分会被裁剪.
也就是会经过变形不超出父级.
默认值为 1, 按照该比例,切割子元素,
如果我们想让他们不变形且不换行,
可以把子元素的shrink 值都设置为0
![image.png](https://upload-images.jianshu.io/upload_images/13637909-8094807d11ec0124.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-5fe866abeee00340.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-8bfffad1bf4b4f78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这就是视频和文字的差异了,
因为用文字表达要准确,所以只能说的不是人话,
实际上核心逻辑非常简单.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-7beb540ed20bf678.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
刚开始,我不明白这个属性有什么用处,
后来发现三列布局时,通过html顺序和 order配合可以调整加载顺序.
默认值为 0
![image.png](https://upload-images.jianshu.io/upload_images/13637909-3f7a10c933cef6d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
baseline 值, 基线对齐, 按照第一行,第一个文字进行对齐.
后面的元素的第一行文字都保持同一线.类似 inline-block verticalaline
strech 属性, 如果元素侧轴没有设置固定值, 则会充满

如果我们想设置子元素的主轴方向的属性,
可以用 grow, shrink, base ,order,  可以调整主轴的大小和位置

如果想谁知子元素的侧轴方向的属性,
可以用aline-item, 

![image.png](https://upload-images.jianshu.io/upload_images/13637909-da4b0f6532e34841.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-eef62ff7608d67d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
父元素上的 flex-direction flex-wrap justify-content aline-item aline-content
这几个属性,都是用来进行布局的.
非常的,,嗯强大.
我们讲主轴设为 x轴, 设定多行的情况,
讨论一下 aline-item 和 aline-content的效果区别.
之前我只是笼统的知道 aline-item 作用在侧轴只有一行的情况.
aline-content 作用在侧轴多行的情况.
而实际上 aline-item 对 侧轴多行的情况也是有效果的,只是不一样.

html
```
         <div class="wrapper">
           <div class="left">left</div>
           <div class="mid">mid</div>
           <div class="right">right</div>
           <div class="left">left</div>
           <div class="mid">mid</div>
           <div class="right">right</div>
           <div class="left">left</div>
           <div class="mid">mid</div>
           <div class="right">right</div>
           <div class="left">left</div>
           <div class="mid">mid</div>
           <div class="right">right</div>
         </div>
```
1.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-9602652bb3670167.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;

    align-items: flex-start;// 如果不设置,默认值就是这个.
    .left{
        width: 200px;
        height: 50px;
        background-color: #99CDFF;
    }
    .mid{
        width: 400px;
        height: 50px;
        background-color: #F08080;
    }
    .right{
        width: 200px;
        height: 50px;
        background-color: #C0A16B;
    }
}
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-96f48fd3851f7515.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;
    align-content: flex-start;
    align-items: flex-start;
    ...后面都一样
}
```
2.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-912ed4693f1f388c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;

    align-items: center;
    ...
}
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-2d9bbe3373eae993.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;
    align-content: center;
    align-items: center;
...
}
```
3.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-a4adc729163fc752.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;

    align-items: flex-end;
...
}
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-807a8e1a3c60e575.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;
    align-content: flex-end;
    align-items: flex-end;
...
}
```
4.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-fea54d9fd5de182d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
当值为strech时, 两个效果是一样的.
注意strech 如果想要有效果, 就必须让heigth(侧轴宽度) 不是固定宽度,否则失效.
```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;
    align-content: stretch;
    align-items: stretch;
    .left{
        width: 200px;
        background-color: #99CDFF;
    }
    .mid{
        width: 400px;
        background-color: #F08080;
    }
    .right{
        width: 200px;
        background-color: #C0A16B;
    }
}
```
#综上,可以得到以下几个区别.
1. aline-content 权重比 aline-item的权重高, 会覆盖.
2. 两个在布局时最基本的行为差别是, 
    aline-item 会默认为每一行平分出同样的宽度,
    在各自的宽度内进行行为.
    而aline-content 则会在全局对所有行进行行为.
3.在子元素上的 aline-self 权重 比 父元素上的 aline-item 高
而父元素aline-content 的权重 比子元素上的 aline-item 高.
也就是说, aline-content 设置之后, aline-self 就会失效.
想要通过aline-self 比较精确控制, 那就不能在父元素上设置 aline-content

除了这三个之外, aline-content 还有两个属性,
与justify-content 非常类似,

![image.png](https://upload-images.jianshu.io/upload_images/13637909-3ad91163c5ff6169.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;
    align-content: space-around;
...
}
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-e83848bdaa313e36.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
.wrapper{
    display: flex;
    width: 800px;
    height: 800px;
    border: 1px solid black;
    flex-wrap: wrap;
    align-content: space-between;
...
}
```

如果父级 relative 子级当中有 absolute的元素, 
则该子元素不受到 flex布局的影响. 
flex布局时会排除该元素进行布局


至此,我觉得flex进行布局,那是真的强.
主轴和侧轴的各自控制属性基本就全了.
侧轴唯一比主轴差的属性,应该就是 shink 和 order属性了.

好课外思考就到这里, 继续看视频
![image.png](https://upload-images.jianshu.io/upload_images/13637909-615c2d0a12272156.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
