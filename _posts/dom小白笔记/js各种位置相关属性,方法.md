# [js中的各种“位置”——“top、clientTop、scrollTop、offsetTop……”，你知道多少](https://www.cnblogs.com/youziclub/p/4811069.html)

![image.png](https://upload-images.jianshu.io/upload_images/13637909-5e236ffc160c5644.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

//          dom.offsetparent  有定位的父级father,父级 display:none时 null
//          dom.offsetLeft      father padding 外侧 --- son border 外侧
//          dom.offsetTop      father padding 外侧 --- son border 外侧
//          dom.offsetHeight  包含scroll尺寸 包含border尺寸 不包含 被隐藏的部分
//          dom.offsetWidth   包含scroll尺寸 包含border尺寸 不包含 被隐藏的部分
//          dom.scrollLeft      往右滚动的距离.
//          dom.scrollTop    往下滚动的距离
//          dom.scrollWidth  包含scroll尺寸 包含隐藏的部分, 不包含border 不包含scroll
//          dom.scrollHeight  包含scroll尺寸 包含隐藏的部分, 不包含border 不包含scroll
//          dom.clientLeft   左边的border尺寸
//          dom.clientTop   上边的border尺寸
//          dom.clientWidth  不包括border 不包括 scroll 可视区 不包含隐藏部分
//          dom.clientHeight  不包括border 不包括 scroll 可视区 不包含隐藏部分

我没校验,可能写错.我已懵逼.

获取整页滚动条的滚动的距离

封装版
```
function getScrollOffset () {
      	if(window.pageXOffset) {
      	  return {
      	    x : window.pageXOffset,
      	    y : window.pageYOffset
      	  }
      	}else {
      	  return {
      	    x : document.body.scrollLeft + document.documentElement.scrollLeft,
      	    y : document.body.scrollTop + document.documentElement.scrollTop
      	  }
      	}
      }
```
其中,scrollLeft,scrollTop 跟上面的图比较发现,这是每个dom元素都有可能访问的属性
而 pageXoffset,pageYoffset 这个属性是window才有的属性,
应该算是BOM里的内容.


window.innerWidth/innerHeight 可视区域的宽高 （加上 滚动条宽度 / 高度）
```
function getViewportOffset () {
      	if(window.innerWidth) {//BOM,也就是window独有的属性
      	  return {
      	    w : window.innerWidth,
      	    h : window.innerHeight
      	  }
      	}else {
      	  if(document.compatMode === "BackCompat") {
      	    return {// 所有 dom元素都有的属性
      	      w : document.body.clientWidth,
      	      h : document.body.clientHeight
      	    } 
          } else {
      	      return {
      	        w : document.documentElement.clientWidth,//documentElement指向的就是html
      	        h : document.documentElement.clientHeight
      	      }// 根据最上面的图片,clientHeight应该是不包括滚动条的
      	    }
      	  }
      	}
      
```

![image.png](https://upload-images.jianshu.io/upload_images/13637909-ddf5d93731832449.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


domEle.getBoundingClientRect(); //这是 es5.0 的方法,
留心观察就会发现,
第一张图所有的top 都无法返回 元素到窗口的绝对距离.
offsetLeft 返回的是相对于有定位的父级
scrollLeft 返回的是滚动条滚过的距离
clientLeft 返回的是border的宽度.

而getBoundingClientRect() 返回的top left bottom right则是相对于html 的距离.
返回的 width height 则和 offsetWidth offsetHeight是一样的.

当然我们也可以用offsetTop来模拟封装一个到body的距离.
offset + 父级border(父级clientTop) + 循环针对于上级的这些量, 直到body,
(offsetTop 是子元素border外侧到 父元素 border内侧之间的距离)

封装版,到body的距离
```
Element.prototype.offsetToTop = function () {
      	var dom = this;
      	var top = 0;
      	while(dom.offsetParent) {
      	  top += dom.offsetTop + dom.offsetParent.clientTop;
      	  dom = dom.offsetParent;
      	}
      	return top;
      }
      
      Element.prototype.offsetToLeft = function () {
        var dom = this;
        var left = 0;
        while(dom.offsetParent) {
          left += dom.offsetLeft + dom.offsetParent.clientLeft;
          dom = dom.offsetParent;
        }
        return left;
      }

```
```
window.getComputedStyle(ele,null).width;  ie8 以下不兼容
获取的是css上的属性.width就是width border就是border
所有css属性值都能获取,包括没有设置的.
当然有些会返回 aotu
em 等相对单位都会换算成 px展示

null 可以改写 before,after 等伪元素
```
```
ele.currentStyle  // ie版 获取 css属性值.
```
兼容封装版本 
```
版本1.0
  function getStyle (ele,prop) {
          	if(window.getComputedStyle) {
          	  return window.getComputedStyle(ele,null)[prop];
          	}else {
          	  return ele.currentStyle[prop];
          	}
          }
版本2.0 定义在原型链上
Element.prototype.getStyle = function (prop) {
          	if(window.getComputedStyle) {
              return window.getComputedStyle(this,null)[prop];
            }else {
              return this.currentStyle[prop];
            }
          }
          
        
          版本3.0 惰性函数练习版
          function getStyle (ele,prop) {
          	if(window.getComputedStyle) {
              getStyle = function (ele,prop) {
              	 return window.getComputedStyle(ele,null)[prop];
              }
            }else {
              getStyle = function (ele,prop) {
                 return ele.currentStyle[prop];
              }
            }
            return getStyle(ele,prop);
          }
          
        版本4.0  立即执行函数版.
          var getStyle = (function () {
          	if(window.getComputedStyle) {
              return function (ele,prop) {
                window.getComputedStyle(ele,null)[prop];
              }
            }else {
              return function (ele,prop) {
              	ele.currentStyle[prop];
              }
            }
          })();
```
```

ele.getBoundingClientRect().top // 返回到body的距离
window.getComputedStyle(ele,null)[top] // 返回css上 top值
ele.offsetTop //返回距离最近定位父级的距离   子border 外 到 父border内侧(包含父padding,子margin)
你会发现3个都是不一样的.
用哪个就要看情况.
```

事件对象上的与位置相关的属性,参考
# [e.pageX、e.clientX、e.screenX、e.offsetX的区别以及元素的一些CSS属性](https://www.cnblogs.com/zhaixr/p/7026320.html)
```
e.pageX，e.pageY：返回的值是相对于文档的定位，文档的左上角为(0,0)，向右为正，向下为正，IE不支持；

e.clientX，e.clientY：返回的值是相对于屏幕可见区域的坐标，
如果页面有滚动条，呗滚动条隐藏的那部分不进行计算，
也可以说是相对于屏幕的坐标，但是不计算上方的工具栏；

e.screenX，e.screenY：返回的是相对于屏幕的坐标，浏览器上面的工具栏；

e.offsetX，e.offsetY：返回的是相对于文档的坐标，和e.pageX，e.pageY作用相同，但是只有IE支持。
$(window).scrollTop()：返回的是浏览器右边的滚动条滚动的距离；

所以：e.pageY=e.pageY||e.clientY+$(window).scrollTop();  //兼容性的写法
```