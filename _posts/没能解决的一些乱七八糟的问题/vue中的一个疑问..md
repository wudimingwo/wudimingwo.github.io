```
var app = new Vue({
  el : '#app',
  data : {
    arr : [1,2,3],
    num : arr[1] ******* 这里是失败的.我的问题是,data里想要引用data里另一个变量要怎么做?
  }

})
```
data 里的属性都会被添加到实例上, 也就是 app 上.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-3996f2656c7bf9ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-628bd8f6a3b5d044.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
所以我这么写了一下
```
var app = new Vue({
             el : '#app',
             data : {
               arr : [1,2],
               num : app.arr[0]
             }
           });
           console.log(app);
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-3998c39a07f0efb1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
报错,这我就很丢人, 很明显这里不能用app 应该用 this
```
var app = new Vue({
             el : '#app',
             data : {
               arr : [1,2],
               num : this.arr[0]
             }
           });
           console.log(app);
```
结果
![image.png](https://upload-images.jianshu.io/upload_images/13637909-16fc55067d540407.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
还是报错,错误说,没有arr这个属性.
我只能理解为, data这个属性没有被"解析完"时,是无法在实例上访问的.
所以data里访问data里其他属性应该是不行的.

而像下面这种
```
var app = new Vue({
             el : '#app',
             data : {
               arr : [1,2],
             },
             computed : {
               num : function () {
               	return this.arr[1]
               }
             }
           });
           console.log(app);
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-dcbd56501c5d5c2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
也就是说,data里的数据是可以被其他属性所访问,
而data不能访问自己的,也不能访问其他属性的(比如computed)?

问题在于,
如果我就想在data里访问data里的其他属性怎么弄?