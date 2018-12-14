三种方法
1.defer
```
<script src="demo.js" defer="defer" type="text/javascript" charset="utf-8"></script>
ie专用
```
2.asyinc
```
<script src="demo.js" async="async" type="text/javascript" charset="utf-8"></script>
ie9以上都可以
只能加载外部js文件。
```
3.用src, 封装版
```
function ａsync (url,callback) {
            	var oScript = document.createElement('script');
            	oScript.type = 'text/javascript'
            	
            	if(oScript.readyState){//IE
            	  oScript.onreadystatechange = function (e) {
            		  if(oScript.readyState == 'complete' || oScript.readyState == 'loaded') {
            		    window[callback]();
            		  }
            	  }
            	} else {
            	  oScript.onload = function () {//非IE
            		    window[callback]();
            	  }
            	}
            	oScript.src = url;
            	document.head.appendChild(oScript);
            }
            
            async('demo.js','test');

```
我们比较一下ajax和 async
先贴一下ajax的封装
```
function ajax (method,url,data,callback,flag) {
            	var xhr;
            	if(typeof(flag) === undefined){flag = true};
            	if(window.XMLHttpRequest){
            	  xhr = new XMLHttpRequest();
            	}else {
            	  xhr = new ActiveXObject('Microsoft.XMLHtml');
            	}
            	method = method.toUpperCase();
            	if(method == "GET"){
            	  xhr.open(method,url + '?' + data,flag);
            	  xhr.send();
            	}else if(method == "POST") {
            	  xhr.open(method,url,flag);
            	  xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded');
                xhr.send(data);
            	}
            	
            	xhr.onreadystatechange = function () {
            		if(xhr.readyState == 4 && xhr.status == 200) {
            		  callback(xhr.responseText);
            		}
            	}
            }

那能不能用ajax来动态获取js？
ajax('GET','demo.js','ss',fn,true);
            
            function fn (x) {
              var text = document.createTextNode(x);
              var oScript = document.createElement('script');
              oScript.appendChild(text);
            	document.head.appendChild(oScript);
            	test();
            }
似乎是可以，但用ajax对象获取的数据是字符串，不能直接append进head里。
想讨论的不是这个
```
```
async 这种方式，如果稍微改一下就可以是jsonp了，就需要后台稍微配合。
重点是，这两种异步执行的形式，我们抽取一下共同的元素。

1.异步
2.监听
3.状态
4.回调

作为一个小白，我感觉大多数跟异步相关的代码，
都涉及 监听，状态，回调。
（话说jsonp似乎是省略了监听和状态？）
```
然后是关于 这个onreadystatechange,onload,readyState的问题。
```
以下的文字只是推测，未经检测

ie的所有dom元素都有 onreadystatechange 监听器 都有readyState属性
非ie只有document有 onreadystatechange 监听器，有readyState属性的



ajax对象（XMLHttpRequest()对象，ActiveXObject()）是有onreadystatechange 监听器，有readyState 属性的。


关键这同样的属性名，返回的数据是不一样的。

document.readyState 返回值有
1.loading... 正在解析？
2.interacive  解析完成？
3.complete // loaded 加载完成？

xhr.readyState 返回值有
1.1  正在加载
2.2  加载完毕
3.3  正在处理
4.4  处理完毕
```