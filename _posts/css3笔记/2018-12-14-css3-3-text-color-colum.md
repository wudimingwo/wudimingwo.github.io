---
layout:     post
title:      "css3笔记3 文本和颜色,报纸布局"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - css3
    - Meta
---

			.box {
				width: 400px;
				height: 300px;
				font-size: 40px;
				font-weight: bold;
				color: white;
				text-shadow: 0px 0px 6px white, 0px 0px 6px white, 0px 0px 6px white, 0px 0px 6px white, -2px -2px 6px deeppink, 2px 2px 6px gold;
				/*可以设置多个shadow，很有用*/
				white-space: nowrap;
				/*overflow: hidden;*/
				/*text-overflow: ellipsis;*/
				
			}
![image.png](https://upload-images.jianshu.io/upload_images/13637909-aa9d2b71a9236b8b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-dc4366f1efe69541.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-a3aa07a9879c470a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-f6f49f476af5131d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-9fbbdfbe1b1bf470.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-ae40e6124b3db3cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-6dd93753ceff1faa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-7b6e4a82e2840310.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-4b8b7db9f8c5eee6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-0546aaf0d21bd545.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
column-span 这个属性是设置在子元素上的.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-acc35f6e5b7c56f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-3bcb50e04650a184.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
HSL 比 RGB , 感觉做一些 颜色上的渐变时, 比如明暗调节时,会更方便一点?
![image.png](https://upload-images.jianshu.io/upload_images/13637909-74f5b20c28aaa422.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-ab5fcdb74bbcb17e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
    .item{
        width: 500px;
        height: 250px;
        background: linear-gradient(0deg , red 0%, yellow 50px,transparent 50px), 
                    linear-gradient(180deg , blue 0%, yellow 50px,transparent 50px),
                    radial-gradient(ellipse at center, red 0%, yellow 50px,transparent 50px);
                    
        font-family: 'FontName';
    }
```
```
        .box{
        	margin: 100px auto;
        	width: 300px;
        	height: 300px;
        	/*border: 1px solid black;*/
        	background-image: linear-gradient(to top right,rgba(0,66,250,0.8),rgba(250,62,0,0.8));
        	background-size: 400% 400%;
        	animation: name 1s ease  alternate-reverse infinite;
        	box-shadow: 0px 0px 5px 2px deeppink,0px 0px 5px 2px deeppink inset;
        	border-radius: 50%;
        	/*transform: scale(1,1);*/
        }
        
        /*一旦渐变，多重shadow ,以及多重背景，最后加上动画，那么出来的效果非常好。不过估计非常杀性能*/
        
        @keyframes name{
        	from{background-position: 0% 0%;box-shadow: 0px 0px 5px 2px deeppink,0px 0px 5px 2px inset;
        		transform: scale(0.5,0.5) translate(0px,500px);
        	}
        	to{background-position: 100% 0%;box-shadow: 0px 0px 5px 2px skyblue,0px 0px 5px 2px skyblue inset;
        	transform: scale(1.5,1.5) translate(0px,0px);
        	
        	}
        }
```
```
        .box{
        	width: 600px;
        	height: 300px;
        	/*margin: 100px auto;*/
        	border-radius: 50%;
        	/*border: 1px solid black;*/
        	background: radial-gradient(circle 100px at 25% center ,purple,red,yellow 99%,transparent),
        	radial-gradient(circle 100px at 75% center ,purple,red,yellow 99%,transparent),
        	repeating-radial-gradient(circle 100px at 50% center ,purple,red,yellow 99%,blue);
        	animation: name 3s ease infinite alternate;
        	/*所以可以在同一个背景图里,存在多个渐变.在背景图中,进行简单的绘画*/
        	/*background: radial-gradient(ellipse closest-side,blue,red,yellow,transparent);*/
        	/*background: radial-gradient(ellipse farthest-corner,blue,red,yellow,transparent);*/
        	/*background: radial-gradient(ellipse closest-side, red, yellow 10%, #1E90FF 50%, white);*/
        	/*background: radial-gradient(ellipse farthest-corner, red, yellow 10%, #1E90FF 50%, white)*/
        	display: flex;
        	justify-content: center;
        	align-items: center;
        }

       @keyframes name{
       	from{filter:grayscale(20%)}
       	to{filter:grayscale(80%)}
       }
```

作业1
![image.png](https://upload-images.jianshu.io/upload_images/13637909-6a34eeea2a625a56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
html
```
         <div class="item">
           <input type="text" name="" id="" value="" />
           <input type="button" name="" id="" value="GO" />
         </div>
```
scss
```
.item{
    width: 400px;
    height: 50px;
    margin: 100px auto;
    background-color: #EEEEEE;
    box-shadow: 0px 2px 2px 2px #C0C0C0;
    display: flex;
    justify-content: space-around;
    align-items: center;
    input[type=text]{
        box-sizing: border-box;
        width: 70%;
        height: 70%;
        padding: 0;
        margin: 0;
        outline: none;
        box-shadow: 0px 0px 2px 0 #C0C0C0 inset;
    }
    input[type=button]{
        box-sizing: border-box;
        height: 70%;
        width: 70px;
        background-color: slategray;
        outline: none;
        border: 0;
        color: white;
        font-weight: bold;
        box-shadow: 0px 0px 2px 2px black;
    }
    input[type=button]:active{
        background-color: sandybrown;
        box-shadow: 0px 0px 2px 2px #444444;
        color : black
    }
}
```
作业二 , 列表显示, 末尾...显示
![image.png](https://upload-images.jianshu.io/upload_images/13637909-4f49e7befa62237e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-30c2263add93767e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
html
```
         <div class="wrapper">
           <h3>最新博文</h3>
           <ol class="list">
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
             <li><span>爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国爱空间咖喱看电视剧爱国</span><span>2013-02.-19</span></li>
           </ol>
         </div>
```
scss
```
.wrapper{
    width: 500px;
    margin: 100px auto;
    
    ol{
        color: #888888;
        span{
            vertical-align: bottom;
        }
        span:first-child{
            display: inline-block;
            width: 300px;
            overflow: hidden;
            white-space: nowrap;
            text-overflow: ellipsis;
        }
    }
}

```