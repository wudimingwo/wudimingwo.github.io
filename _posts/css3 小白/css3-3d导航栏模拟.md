```

<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>3d导航案例</title>
        <style type="text/css">
            html,body{
              width: 100%;
              margin: 0;
              padding: 0;
            }
            .wrapper{
              width: 100%;
              height: 37px;
              border: 1px solid black;
              box-sizing: border-box;
              display: flex;
              justify-content:space-between;
              align-items: stretch;
              perspective: 1000px;
              transform-style: preserve-3d;
            }
            .wrapper div{
              position: relative;
              flex-grow: 1;
              text-align: center;
              border: 1px solid black;
              line-height: 37px;
              background-color: #F08080;
              transition: all 0.5s ease;
              /*transform-origin: center center -18.5px;*/
              transform: rotateX(0deg);
              transform-style: preserve-3d;
            }
            .wrapper div::before{
              content: 'item';
              position: absolute;
              display: block;
              width: 100%;
              height: 100%;
              background-color: #A71D5D;
              transform-origin: top;
              border: 1px solid black;
              /*这里关键在于,不能把transform origin 设置在父级上*/
             /*景深也应该每个子级自己独立设置.*/
              transform-origin: center center -18.5px;
              transform:perspective(1000px) rotateX(90deg);
            }
            .wrapper div:hover{
              background-color: #f00;
              transform-origin: center center -18.5px;
              transform:perspective(1000px) rotateX(-90deg);
            }
            
            
        </style>
    </head>
    <body>
         <div class="wrapper">
           <div class="item1">item1</div>
           <div class="item2">item2</div>
           <div class="item3">item3</div>
           <div class="item4">item4</div>
           <div class="item5">item5</div>
           <div class="item6">item6</div>
         </div>
        <script type="text/javascript">
            
        </script>
    </body>
</html>


```