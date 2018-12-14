![出现边框.png](https://upload-images.jianshu.io/upload_images/13637909-14312f518e7a3498.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

▪html
```
         <div></div>
```
▪css
```
div{
              width: 100px;
              height: 100px;
              
              margin: 200px auto;
              
              border-radius: 50%;
              border: 1px solid #CCCCCC;
              background-image: linear-gradient(to bottom,white 50%,black 50%,black);
              
              position: relative;
            }
            
            div:before,div:after{
              content: '';
              display: block;
              width: 50px;
              height: 50px;
              border-radius: 50%;
              position: absolute;
              top: 50%;
              transform: translateY(-50%);
              box-sizing: border-box;
            }
            div:before {
              left: 0;
              background-color: black;
              box-shadow: 0px 0px 0px 18px #fff inset;
            }
            div:after {
              right: 0;
              border: 1px solid black;
              background-color: white;
              box-shadow: 0px 0px 0px 18px #000 inset ;
            }
```