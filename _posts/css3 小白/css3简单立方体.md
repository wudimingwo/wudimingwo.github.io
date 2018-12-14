
```
这次写,有一个需要注意的细节,比如
transform: translate(10px,10px);
transform: rotate(45deg);
下面的transform 会覆盖上面的,
rotate会正常表达, translate则不能.
(一定要注意覆盖问题)

正常写法是,中间一个空格 写在一起.
transform: translate(10px,10px) rotate(45deg);
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
            .wrapper{
              width: 200px;
              height: 200px;
              position: relative;
              margin: 100px auto;
              transform-style: preserve-3d;
              transform-origin: 100px 100px 100px;
              transform: rotate3d(1,1,0,45deg);
              /*perspective: 1000px;*/
              animation: move 3s ease alternate-reverse infinite;
            }
            @keyframes move{
            	from{}
            	to{transform: rotate3d(1,0,0,180deg);}
            }
            
            .wrapper div{
              width: 100%;
              height: 100%;
              font-size: 40px;
              font-weight: bold;
              color: #404040;
              position: absolute;
              line-height: 200px;
              text-align: center;
              border: 1px solid #CC2222;
            }
            
             .front{
              transform: translate3d(0,0,100px);
              background-color: #F0AD4E;
            }
            .wrapper .back{
              transform: rotate3d(0,1,0,180deg) translate3d(0,0,100px);
              background-color: #A49A90;
            }
            .left{
              transform: rotateY(-90deg) translate3d(0,0,100px);
              background-color: #D43F3A;
            }
            .right{
              transform: rotateY(90deg) translate3d(0,0,100px);
              background-color: khaki;
            }
            .up{
              transform: rotateX(-90deg) translate3d(0,0,100px);
              background-color: #204D74;
            }
            .down{
              transform: rotateX(90deg) translate3d(0,0,100px);
              background-color: #00C4A7;
            }
            .wrapper div{
              opacity: 0.5;
            }
        </style>
    </head>
    <body>
         <div class="wrapper">
           <div class="front">front</div>
           <div class="back">back</div>
           <div class="up">up</div>
           <div class="down">down</div>
           <div class="left">left</div>
           <div class="right">right</div>
         </div>
        <script type="text/javascript">
            
        </script>
    </body>
</html>

```