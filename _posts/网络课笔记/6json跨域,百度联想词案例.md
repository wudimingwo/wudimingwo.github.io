![image.png](https://upload-images.jianshu.io/upload_images/13637909-dd7493f5073d24d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在各自的脚本中 设置 document.domain = "58.com"
两个网页就可以互相访问资源了.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-6b2f26155fe08cb0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
简单百度联想词案例
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>dddd</title>
        <style type="text/css">
            
        </style>
    </head>
    <body>
         <input type="text" name="aaa" id="aaa" value="" />
         <ul id="ul"></ul>
        <script type="text/javascript">
            
            function jsonp (value,cb) {
              var scr = document.createElement("script");
              scr.src = "https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=" + value +"&cb=" + cb.name;
              document.body.appendChild(scr);
              document.body.removeChild(scr);// 创建完删除 script
            }
            
            function show (data) {
            	console.log(data);
            	var str = "";
            	var list = data.s;
            	list.forEach((item,index) => {
            	  str += "<li><a href='https://www.baidu.com/s?wd=" + item + "' target='_blink'>" + item + "</a></li>";
            	})
            	ul.innerHTML = str;
            }
            
            aaa.oninput = function (e) {
            	jsonp(this.value,show);
            }
        </script>
    </body>
</html>

```
加上一个搜狗
搜狗应该也是jsonp技术,
不过不必传cb字符串,
他直接锁定了字符串 window.sougou.sug
所以我们只需要把回调函数定义在这个路径上就可以.
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>dddd</title>
        <style type="text/css">
            body{
              margin: 0;
              padding: 0;
            }
            iframe {
              width: 80vw;
              height: 100vh;
              position: absolute;
              left : 20vw;
              z-index: -1;
            }
            ul, li{
              width: 200px;
            }
            
        </style>
    </head>
    <body>
      <iframe id="ifram" src="https://www.baidu.com" ></iframe>
         <span>百度</span><br />
         <input type="text" name="aaa" id="aaa" value="" />
         <ul id="ul"></ul>
         <span>搜狗</span><br />
         <input type="text" name="bbb" id="bbb" value="" />
         <ul id="ull"></ul>
        <script type="text/javascript">
            
            function jsonp (value,cb) {
              var scr = document.createElement("script");
              scr.src = "https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=" + value +"&cb=" + cb.name;
              document.body.appendChild(scr);
              document.body.removeChild(scr);// 创建完删除 script
            }
            function jsonpp (value) {
              console.log(value);
              var scr = document.createElement("script");
              scr.src = "https://www.sogou.com/suggnew/ajajjson?key=" + value + "&type=web&";
              document.body.appendChild(scr);
//            document.body.removeChild(scr);// 创建完删除 script
            }
            
            function show (data) {
            	console.log(data);
            	var str = "";
            	var list = data.s;
            	list.forEach((item,index) => {
            	  str += "<li>" + item + "</li>";
            	})
            	ul.innerHTML = str;
            }
            
            aaa.oninput = function (e) {
            	jsonp(this.value,show);
            }
            ul.onclick = function (e) {
              if(e.target.tagName == "LI") {
                ifram.src = "https://www.baidu.com/s?wd=" + e.target.innerText;
              }
            }
            
            
            var sogou = {}
            sogou.sug = function (data) {
            	console.log(data[1]);
            	var list = data[1];
            	var str = "";
            	list.forEach((item,index) => {
            	  str += "<li>" + item + "</li>"
            	});
            	ull.innerHTML = str;
            }
            
            bbb.oninput = function (e) {
              jsonpp(this.value);
            }
            
            ull.onclick = function (e) {
              if(e.target.tagName == "LI") {
                ifram.src = "https://www.sogou.com/web?query=" + e.target.innerText;
              }
            }
        </script>
    </body>
</html>

```