```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>商品移动案例</title>
        <style type="text/css">
            .wrapper{
              width: 100vw;
              height: 100vh;
              
              display: flex;
              justify-content: space-around;
              align-items: center;
            }
            .wrapper>div{
              width: 200px;
              height: 300px;
              border: 1px solid #CCCCCC;
              
              display: flex;
              flex-direction: column;
              justify-content: space-around;
              align-items: center;
              
              transition: transform 0.5s ease;
            }
            
            .wrapper>div>img{
              width: 150px;
              height: 150px;
              margin-bottom: -20px;
              transition: transform 0.5s ease;
            }
            .wrapper>div:hover{
              transform:translateY(-10px);
            }
            .wrapper>div:hover>img{
              transform: translateY(-50px);
            }
            .wrapper>div>.name{
              transition: font-size 0.5s ease,font-weight 0.5s ease;
            }
            .wrapper>div:hover>.name{
              font-size: 30px;
              font-weight: 800;
            }
            
        </style>
    </head>
    <body>
         <div class="wrapper">
           <div class="item1">
             <img src="img/test1.jpg" alt="" />
             <div class="name">商品1</div>
           </div>
           <div class="item2">
             <img src="img/2test.jpg" alt="" />
             <div class="name">商品2</div>
           </div>
           <div class="item3">
             <img src="img/3test.jpg" alt="" />
             <div class="name">商品3</div>
           </div>
           <div class="item4">
             <img src="img/4test.jpg" alt="" />
             <div class="name">商品4</div>
           </div>
         </div>
        <script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script type="text/javascript">
            
        </script>
    </body>
</html>

```