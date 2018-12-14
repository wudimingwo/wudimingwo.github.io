先把渡一公开课的拿过来
![image.png](https://upload-images.jianshu.io/upload_images/13637909-39c13473deb14382.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
先测试了一下
![image.png](https://upload-images.jianshu.io/upload_images/13637909-81203463683f61e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

事件触发顺序是这样的。

document.readyState会依次变化
1. loading  正在解析
2.interactive 解析完成   此时可以操作dom
3.complete / loaded 加载完成  此时可以操作dom

DomContentLoaded 事件在 interactive 和complete之间触发 此时可以操作dom
window.onloaded 同样是加载完成， 似乎 onloaded事件在 complete之后触发。


所以理论上来讲，我们可以在 interactive 和 DomContentLoaded 时，
就可以操作（渲染）dom是最有效率的？
解析完就可以执行 js了。



JS<script> 一定要放在 Body 的最底部吗
https://blog.csdn.net/garvisjack/article/details/71077986#t6