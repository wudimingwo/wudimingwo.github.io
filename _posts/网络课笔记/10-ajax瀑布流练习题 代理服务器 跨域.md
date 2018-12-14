![图片.png](https://upload-images.jianshu.io/upload_images/13637909-198bc9173c27a966.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这里图片资源用的是
http://www.wookmark.com/api/json/popular?page=
通过用自家的服务器(代理服务器)的方式进行了跨域.
用的是wampserver, 搭建的服务器.

css
```
*{
	margin: 0;
	padding: 0;
	list-style: none;
}

.wrapper{
	width: 80%;
	min-width: 930px;
	margin: 0 auto;
	text-align: center;
}

.wrapper ul{
	display: inline-block;
}

.wrapper li{
	/*vertical-align: top;*/
	/*display: inline-block;*/
	float: left;
}

.wrapper li .item{
	width: 200px;
	padding: 10px;
	border: 1px solid #ccc;
	margin: 0px 5px 10px;
}

.wrapper li .item .image{
	width: 100%;
}

.wrapper li .item img{
	width: 100%;
}


.load {
	font: 30px  "微软雅黑";
	font-weight: bolder;
	color: #CCCCCC;
	text-align: center;
	display: none;
}

```
js
```
(function ($) {
	//第一步发送ajax请求,获取图片数据
	var oLi = document.getElementsByTagName('li'),
		flag = false,
	    num = 1;
	    
	getData();
	function getData() {
		if(!flag){
			flag = true;
			$.ajax({
				type:"GET",
				url:"http://localhost/water/js/getPic.php?cpage" + num,
				async:true,
				beforeSend:function () {
					$('.load').show();
				},
				success:addDom,
				error: function () {
					console.log('error');
				}
			
		});
		};
	
		num++;
		
		}
		function addDom (data) {
			var dataList = JSON.parse(data);
			console.log(dataList);
				$('.load').hide();
		if(dataList.length > 0){
			dataList.forEach(function (ele,index) {
				var iDiv = $("<div class='item'></div>");
				var imgBox = $("<div class='image'></div>");
				var oImg = new Image();
				var oP = $('<p></p>');
				oP.text(ele.title);
				oImg.src = ele.preview;
				oImg.onload = function () {
					imgBox.append(oImg);
					iDiv.append(imgBox).append(oP);
					var index = getMinList(oLi);//判断哪个li是最短的
					$(oLi[index]).append(iDiv);
				}
			})
		}
		flag = false;
	}
	
		function getMinList (dom) {
			var minHeight = parseInt($(dom[0]).css('height'));
			var index = 0;
			for (var i = 1; i < dom.length; i++){
				var height = parseInt($(dom[i]).css('height'));
				if(height < minHeight){
					minHeight = height;
					index = i;
				}
			}
//			console.log(index);
			return index;
		}
		
//		$(window).scrollTop() + $(window).height() > (oLi[getMinList(dom)]).css('height')
$(window).scroll(function () {
	var clientHeight = $(window).height();
	var scrollHeight = $(window).scrollTop();
	var minLiH = parseInt($(oLi[getMinList(oLi)]).css('height'));
	if(scrollHeight + scrollHeight > minLiH){
		getData();
	}
//	console.log(clientHeight,scrollHeight,minLiH);
})
})(jQuery)
```
html
```
<!DOCTYPE HTML>
  <html>
  <head>
    <meta charset="UTF-8">
    <title>practice</title>
    <link rel="stylesheet" type="text/css" href="css/index.css"/>
    <style type="text/css">
        *{
        }
    </style>     
  </head>
  <body>
  	<div class="wrapper">
  		<ul>
  			<li>
  				<div class="item">
  					<div class="image">
  						<img src="img/1.jpg" alt="" />
  						<p>描述1</p>
  					</div>
  				</div>
  			</li>
  			<li>
  				<div class="item">
  					<div class="image">
  						<img src="img/2.jpg" alt="" />
  						<p>描述2</p>
  					</div>
  				</div>
  			</li>
  			<li>
  				<div class="item">
  					<div class="image">
  						<img src="img/3.jpg" alt="" />
  						<p>描述3</p>
  					</div>
  				</div>
  			</li>
  			<li>
  				<div class="item">
  					<div class="image">
  						<img src="img/4.jpg" alt="" />
  						<p>描述4</p>
  					</div>
  				</div>
  			</li>
  		</ul>
  	</div>
    <div class="load">loading...</div>
    <script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
    <script src="js/main.js" type="text/javascript" charset="utf-8"></script>
    <script type="text/javascript">
    </script>
  </body>
  </html>
  
```
php
```
<?php
header('Content-type:text/html;charset="utf-8"');
	
$cpage = isset($_GET['cpage']) ? $_GET['cpage'] : 1;

$url = 'http://www.wookmark.com/api/json/popular?page=' . $cpage;

$content = file_get_contents($url);
$content = iconv('gbk','utf-8',$content);

echo $content;
?>
```