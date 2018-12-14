```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>dddd</title>
        <style type="text/css">
            
            .wrapper{
              position: relative;
              
              transform-style: preserve-3d;
              transform-origin: center;
              perspective: 700px;
              
              width: 200px;
              height: 200px;
              margin: 150px auto;
            }
            .wrapper div{
              position: absolute;
              
              width: 100%;
              height: 100%;
              border-radius: 15px;
              
              font: 30px/200px "微软雅黑";
              font-weight: bold;
              color: #545652;
              text-align: center;
            }
            
            .top{
              background-color: lightblue;
              transform-origin: bottom left;
              transition: all 0.5s ease;
              /*backface-visibility: hidden;*/
            }
            .bottom{
              background-color: rgba(240,128,128,0.8);
            }
            
            .wrapper:hover .top{
              transform: rotate3d(1,1,0,-180deg);
              opacity: 0.3;
            }
        </style>
    </head>
    <body>
         <div class="wrapper">
           <div class="bottom">bottom</div>
           <div class="top">top</div>
         </div>
        <script type="text/javascript">
                
        </script>
    </body>
</html>

```