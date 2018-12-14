![image.png](https://upload-images.jianshu.io/upload_images/13637909-8a00f77d05632c99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-75bbff497eeb0a29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-0db2cc20db4e3045.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
想要获取子窗口的变量,
必须满足同源条件.

父级
test.html
```
 <iframe src="son.html" width="" name="son" height=""></iframe>
        <script type="text/javascript">
            var ifr = document.getElementsByTagName("iframe")[0];
            // 父级拿到子级的变量.
            ifr.onload = function () {// 因为iframe 异步加载,所以要等到onload 才能获取数据.
              console.log(window.frames["son"].a);
              console.log(ifr.contentWindow.a);
              }
            
        </script>
```
子级
son.html
```
    <body>
         demo
        <script type="text/javascript">
            var a = 123;
            // 子级拿到父级的变量
            console.log(window.parent.ifr);
        </script>
    </body>
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-7da5e014e9c8c86c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-73c4efb0d24650be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


iframe 跨域
1. src里添加哈希值
子级通过 location.hash 取值. 父传子.
test.html
```
<body>
         <iframe src="https:// 不同源/son.html" width="" name="son" height=""></iframe>
        <script type="text/javascript">
            var ifr = document.getElementsByTagName("iframe")[0];
            var age = 50;
            var oSrc = ifr.src;
            document.onclick = function () {// 按需传值.
              age++;
              ifr.src = oSrc + "#" + age;
            }
            
        </script>
    </body>
```
son.html
```
<body>
         demo
        <script type="text/javascript">
            var a = 123;
            // 子级拿到父级的变量
            // 必须进行监听
            var lastHash = location.hash;
            
            setInterval(function () {
              if (lastHash != location.hash) {// 当值不变时,
                console.log(location.hash.slice(1));
              	lastHash = location.hash;
              }
            },50);
            // 因为setInterval 要一直监听,太过耗费性能
            // 所以这种跨域方式不怎么用了.

            // 刚才发现有一个监听 哈希值的事件 // 用这个应该也可以
          document.body.onhashchange = function () {
          	console.log(location.hash);
          }
                  
        </script>
    </body>
```
2.window.name
完成 子传父
window.name 是可以跨域的.
同一个窗口的不同源的网页,都共享一个 window.name
都可以操作window.name

我们设置一个中间页面, uncle
test 和 uncle 是 父子,且同源, 可以通过 contentWindow 完成子传父
uncle 和 son 不是同源, 但同一个iframe 共享同一个 window.name
可以完成 互相之间的值传递.
所以test 就能通过 uncle 来获取 son给他的数据.

test.html
```
    <body>
         <iframe src="son.html" width="" name="son" height=""></iframe>
        <script type="text/javascript">
            var ifr = document.getElementsByTagName("iframe")[0];
            
            
            var flag = true;// 这是为了只执行一次.// 否则会无休止的刷新.因为 ifr.src 会一直触发 onload
            ifr.onload = function () {
              if (flag) {
                flag = false;
                ifr.src = "./uncle.html";
              } else{
                // 如果这里 flag = true 就变成了 类似 toggle 的功能.
                console.log(ifr.contentWindow.name);
              }
            }



            // 假设我们希望, 获取完值后,页面返回到 son
            
            function cb (data) {
            	console.log(data);
            }
            
            function getName (ifr, callback) {
              var src = ifr.src;
            	ifr.src = "./uncle.html";
            	var flag = true;
            	ifr.onload = function () {
            	  if (flag) {
            	    flag = false;
            	    callback(ifr.contentWindow.name);
            	    ifr.src = src;
            	  }
            	}
            }
            
            getName(ifr, cb);
        </script>
    </body>
``` 
uncle.html
这个什么都可以没有
son.html
```
<body>
         demo
        <script type="text/javascript">
          window.name = "son is hansom";
        </script>
    </body>
```
这个过程完成了子传父.


无论是 用哈希值方式, 还是 window.name 的方式
都必须有传值的情况下,才能获取值.
不能在没传的情况下获取值.

![image.png](https://upload-images.jianshu.io/upload_images/13637909-4f3e9b4a74d473fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-de49438ba4b6ad5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
> 第三种方法, 实现子传父 利用 postMe
son.js
```
          window.parent.postMessage(obj,"http://localhost/");
// 第二个参数很重要, 写父级的域名,表示能访问?
```
father.js
```
      window.onmessage = function (e) {
      	console.log(e.data);// 这里能够获取到 obj
      }
```
> 

