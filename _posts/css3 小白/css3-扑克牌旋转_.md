```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>旋转扑克牌</title>
        <style type="text/css">
            .wrapper{
              width: 100vw;
              height: 100vh;
              position: relative;
              
              display: flex;
              justify-content: space-around;
              align-items: center;
            }
            .wrapper .wrapperImg {
              position: relative;
              width: 250px;
              height: 400px;
            }
            .wrapper img{
              position: absolute;
              display: block;
              width: 100%;
              height: 100%;
              border-radius: 15px;
              border: 1px solid #CCCCCC;
              transform-origin: center 500px;
              transition: all 0.5s ease;
              transform: rotate(0deg);
            }
            .wrapperImg img:hover{
              width: 300px;
              height: 450px;
              z-index: 1;
            }
            
            .wrapperImg:hover .item1{
              transform: rotate(60deg) translateY(-100px);
            }
            .wrapperImg:hover .item2{
              transform: rotate(30deg) translateY(-100px);
              
            }
            .wrapperImg:hover .item3{
              transform: rotate(0deg) translateY(-100px);
            }
            .wrapperImg:hover .item4{
              transform: rotate(-30deg) translateY(-100px);
              
            }
            .wrapperImg:hover .item5{
              transform: rotate(-60deg) translateY(-100px);
              
            }
        </style>
    </head>
    <body>
         
         <div class="wrapper">
           <div class="wrapperImg">
             <img src="img/2test.jpg" alt="" class="item1" />
             <img src="img/3test.jpg" alt="" class="item2" />
             <img src="img/4test.jpg" alt="" class="item3" />
             <img src="img/test1.jpg" alt="" class="item4" />
             <img src="img/2test.jpg" alt="" class="item5" />
           </div>
         </div>
         
        <script type="text/javascript">
            
        </script>
    </body>
</html>

```