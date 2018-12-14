![太极图](https://upload-images.jianshu.io/upload_images/13637909-a89cf3eb7255b90a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

看到群里讨论的.

第一种,利用伪元素,和渐变
▪html
```
<div></div>
```
▪css
```
div{
              width: 100px;
              height: 100px;
              
              margin: 200px auto;
              
              border-radius: 50%;
              border: 1px solid #CCCCCC;
              background-image: linear-gradient(to bottom,white 50%,black 50%,black);
              
              position: relative;
            }
            
            div:before,div:after{
              content: '';
              display: block;
              width: 50px;
              height: 50px;
              border-radius: 50%;
              position: absolute;
              top: 50%;
              transform: translateY(-50%);
              box-sizing: border-box;
            }
            div:before {
              left: 0;
              background-image: radial-gradient(circle at 25px 25px,black 6.5px,white 7.5px);
            }
            div:after {
              right: 0;
              background-image: radial-gradient(circle at 25px 25px,white 6.5px,black 7.5px);
            }
```
第二种用伪元素 和 box-shadow
▪html
```
<div></div>
```
▪css
```
div{
              width: 100px;
              height: 100px;
              
              margin: 200px auto;
              
              border-radius: 50%;
              border: 1px solid #CCCCCC;
              background-image: linear-gradient(to bottom,white 50%,black 50%,black);
              
              position: relative;
            }
            
            div:before,div:after{
              content: '';
              display: block;
              width: 50px;
              height: 50px;
              border-radius: 50%;
              position: absolute;
              top: 50%;
              transform: translateY(-50%);
              box-sizing: border-box;
            }
            div:before {
              left: 0;
              background-color: black;
              box-shadow: 0px 0px 0px 18px #fff inset;
            }
            div:after {
              right: 0;
              border: 1px solid black;
              background-color: white;
              box-shadow: 0px 0px 0px 18px #000 inset ;
            }
```
这个是有问题的, 利用box-shadow后会有一个类似边框的东西出现,
我暂时想不出怎么消除.
![出现一个边框](https://upload-images.jianshu.io/upload_images/13637909-975869d8adeb361e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

