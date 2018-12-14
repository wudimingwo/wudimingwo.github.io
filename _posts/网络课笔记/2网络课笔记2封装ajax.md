ajax : aysnchronous javascript and xml
特点: 异步,局部的发送网络请求, 不必刷新页面.
![image.png](https://upload-images.jianshu.io/upload_images/13637909-318ab47540689916.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/13637909-4e48eeec6dcee7ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-4d92db977a7b8e8b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

封装:
```
function ajaxFun (method, url, data, callback, flag) {
           	var xhr = null;
           	var flag = typeof flag == "undefined" ? true : flag;
           	if (window.XMLHttpRequest) {
           		xhr = new XMLHttpRequest();
           	} else{
           		xhr = new ActiveXObject("Microsoft.XMLHttp");// 兼容 ie
           	}
           	method = method.toUpperCase();
           	if (method == "GET") {
           		xhr.open(method,url + "?" + data,flag);
           		xhr.send();
           	} else{
           		xhr.open(method, url, flag);
           		xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
           		xhr.send(data);
           	}
           	
           	xhr.onreadystatechange = function () {
           		if(xhr.readyState == 4 && xhr.status == 200) {
           		  callback(xhr.responseText);
           		}
           	}
           }
```
简单案例
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
         <form action="#" method="post">
         	<input type="text" name="" id="username" value="" />
         	<input type="text" name="" id="age" value="" />
         	<input id="aaa" type="submit" value="提交"/>
         	<input id="bbb" type="submit" value="获取" />
         </form>
         <ul id="ul"></ul>
        <script type="text/javascript">
            
            function ajaxFun (method, url, data, callback, flag) {
            	var xhr = null;
            	if (window.XMLHttpRequest) {
            		xhr = new XMLHttpRequest();
            	} else {
            	  xhr = new ActiveXObject("Microsoft.XMLHttp");
            	}
            	method = method.toUpperCase();
            	if (method == "GET") {
            		xhr.open(method,url + "?" + data,flag);
            		xhr.send();
            	} else if (method == "POST" ){
            		xhr.open(method,url,flag);
            		xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded")
            		xhr.send(data);
            	}
            	
            	xhr.onreadystatechange = function () {
            		if(xhr.readyState == 4 && xhr.status == 200) {
            		  callback(xhr.responseText);
            		}
            	}
            }
            
            const showlist = (data) => {
              console.log(JSON.parse(data));
              var list = JSON.parse(data);
              let str = "";
              list.forEach((item,index) => {
                str += "<li>" + item.title + "---" + item.date + "</li>"
              })
              ul.innerHTML = str;
            }
            
            bbb.onclick = function (e) {
            	e.preventDefault();
            	ajaxFun('GET','./getNews.php',null,showlist,true);
            }
            
            const showName = (data) => {
              alert(data);
            }
            
            aaa.onclick = function (e) {
            	e.preventDefault();
            	var name = username.value;
            	var agedata = age.value;
            	var data = "username=" + name + "&age=" + agedata;
            	ajaxFun('POST','./post.php',data,showName,true);
            }
            
            
        </script>
    </body>
</html>
```
下面这俩php我是不太懂的.
不过大概能看懂.
post.php
```
<?php
	header('content-type:text/html;charset="utf-8"');
	error_reporting(0);
	
	$username = $_POST['username'];
	$age = $_POST['age'];

	echo "名字：{$username},年龄：{$age}";

```
getNews.php
```
<?php
	header('content-type:text/html;charset="utf-8"');
	error_reporting(0);
	
	
	$news = array(
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6'),
	array('title'=>'的空间发几块的价格卡减肥的恐 惧感','date'=>'2014-1-6')
	
	);
	

	echo json_encode($news);

```