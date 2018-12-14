模仿来源
http://www.17sucai.com/pins/demo-show?id=26380

```
在pc端的大致模仿了出来.
有一点之前没注意的知识,
子元素设置 width:100%;height:100%;
则这个width 只会是父级的content区域,
不包括padding和border区域.
```
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
            background-color: #494A5F;
          }
            .list{
              display: flex;
              width: 100vx;
              height: 600px;
              justify-content: space-around;
              align-items: center;
              
            }
            .list .item{
              position: relative;
              display: flex;
              flex-direction: column;
              width: 212px;
              height: 350px;
              justify-content: space-around;
              align-items: center;
              overflow: hidden;
              background: white;
            }
            .list .item .up-circle{
              width: 300px;
              height: 500px;
              border-radius: 50%;
              position: absolute;
              left: -45px;
              top: -520px;
              transition: top 0.5s ease;
              display: block;
              background-color: #eb1768;
              opacity: 0.2;
              /*z-index: -1;*/
            }
            .list .item:hover .up-circle{
              top: -351px;
            }
            .list .item:hover .up-circle{
              display: block;
            }
            .list .item .contain{
              position: relative;
              z-index: 1;
              width: 130px;
              height: 130px;
              box-sizing: border-box;
              background-color: navajowhite;
              border-radius: 50%;
              background-repeat: no-repeat;
              background-size: 100%;
              background-origin: content-box;
              border: 0px solid salmon;
              transition: all 0.5s ease;
            }
            .list .item .contain img{
              border-radius: 50%;
              display: block;
              width: 100%;
              height: 100%;
            }
            
            .list .item:hover .contain{
              transition: all 0.5s ease;
              border: 10px solid darkred;
              background-color: white;
              /*为什么border 没有渡过效果?*/
              /*必须在变化前后都要设置*/
              padding: 10px;
            }
            
            .list .item .user{
              display: flex;
              flex-direction: column;
              justify-content: center;
              align-items: center;
              text-transform: capitalize;
              margin-top: -60px;
            }
            .list .item .user .name{
              font-family: "微软雅黑";
              font-size: 22px;
              font-weight: 700;
              color: #4e5052;
              letter-spacing: 1px;
            }
            .list .item .user .job{
              font-family: "微软雅黑";
              font-size: 15px;
              color: #4e5052;
            }
            .list .item .down{
              display: flex;
              position: absolute;
              bottom: -37px;
              left: 0px;
              width: 100%;
              height: 37px;
              background-color: #eb1768;
              justify-content: center;
              transition: bottom 0.5s ease;
            }
            .list .item:hover .down{
              display: flex;
              bottom: 0px;
              transition: bottom 0.5s ease;
            }
            .list .item .down a{
              display: inline-block;
              width: 42px;
              height: 100%;
              font-size: 17px;
              text-align: center;
              line-height: 37px;
              text-decoration: none;
              font-weight: 700;
              color: white;
            }
            .list .item .down a:hover{
              color: #eb1768;
              background-color: white;
              text-decoration: underline;
            }
        </style>
    </head>
    <body>
         <ul class="list">
         	<li class="item">
         	  <div class="up-circle"></div>
         	  <div class="contain">
         	    <img src="img/test1.jpg"/>
         	  </div>
         	  <div class="user">
         	    <div class="name">angelia</div>
         	    <div class="job">web developer</div>
         	  </div>
         	  <div class="down">
         	    <a href="#">f</a>
         	    <a href="#">T</a>
         	    <a href="#">G</a>
         	    <a href="#">In</a>
         	  </div>
         	</li>
         	<li class="item">
         	  <div class="up-circle"></div>
         	  <div class="contain">
         	    <img src="img/2test.jpg"/>
         	  </div>
         	  <div class="user">
         	    <div class="name">angelia</div>
         	    <div class="job">web developer</div>
         	  </div>
         	  <div class="down">
         	    <a href="#">f</a>
         	    <a href="#">T</a>
         	    <a href="#">G</a>
         	    <a href="#">In</a>
         	  </div>
         	</li>
         	<li class="item">
         	  <div class="up-circle"></div>
         	  <div class="contain">
         	    <img src="img/3test.jpg"/>
         	  </div>
         	  <div class="user">
         	    <div class="name">angelia</div>
         	    <div class="job">web developer</div>
         	  </div>
         	  <div class="down">
         	    <a href="#">f</a>
         	    <a href="#">T</a>
         	    <a href="#">G</a>
         	    <a href="#">In</a>
         	  </div>
         	</li>
         	<li class="item">
         	  <div class="up-circle"></div>
         	  <div class="contain">
         	    <img src="img/4test.jpg"/>
         	  </div>
         	  <div class="user">
         	    <div class="name">angelia</div>
         	    <div class="job">web developer</div>
         	  </div>
         	  <div class="down">
         	    <a href="#">f</a>
         	    <a href="#">T</a>
         	    <a href="#">G</a>
         	    <a href="#">In</a>
         	  </div>
         	</li>
         </ul>
        <script type="text/javascript">
              
        </script>
    </body>
</html>

```