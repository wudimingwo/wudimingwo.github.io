![生命周期](https://upload-images.jianshu.io/upload_images/13637909-9cfd46b508d75270.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

生命周期图
![lifecycle.png](https://upload-images.jianshu.io/upload_images/13637909-115716c1df0a59ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
var app = new Vue({
             el : "#app",
             beforeCreate () {
               console.log(Object.keys(this));
             }
           })
```
我勒个去,竟然还有 Object.keys(obj) 这种好用的api存在..........
```
var app = new Vue({
             el : "#app",
             beforeCreate () {
               console.log(Object.entries(this));
             }
           })
```
没完,还有一个好用的api Object.entries(obj),,,,,