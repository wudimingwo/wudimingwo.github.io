---
layout:     post
title:      "css3作业 导航条的响应式布局"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - css3
    - Meta
---
好烂,没写完
html
```
<!DOCTYPE html>
<html>

  <head>
    <meta charset="UTF-8">
    <meta name="viewprot" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>dddd</title>
    <link rel="stylesheet" type="text/css" href="css/test.css" />
    <style type="text/css">

    </style>
  </head>

  <body>
      <div class="wrapper">
        <div class="navlist">
          <ul class="nav">
            	<li><a href="#">Bootstrap</a></li>
            	<li><a href="#">起步</a></li>
            	<li><a href="#">全局CSS样式</a></li>
            	<li><a href="#">组件</a></li>
            	<li><a href="#">JavaScript插件</a></li>
            	<li><a href="#">定制</a></li>
            	<li><a href="#">网站实例</a></li>
            	<li><a href="#">BootStrap中文网</a></li>
          </ul>
        </div>
        <div class="content">
          <div class="logo">
            B
          </div>
          <div class="describe">
            Bootstrap 是最受欢迎的 HTML、CSS 和 JS 框架，用于开发响应式布局、移动设备优先的 WEB 项目。
          </div>
          <div class="download">
            <a href="#">下载 BootStrap</a>
          </div>
          <div class="versionDes">
            当前版本： v3.3.7 | 文档更新于：2018-11-07
          </div>
          <div class="hr"></div>
          <div class="shequ">
            <a href="#">访问前端社区</a>
          </div>
          <div class="juejin">
            <a href="#">来掘金，和更多前端开发者交流</a>
          </div>
        </div>
      </div>
      
  </body>

</html>
```
scss
```
:root,body{
    margin: 0;
    padding: 0;
}
.wrapper{
    display: flex;
    flex-direction: column;
    width: 100vw;
    height: 100vh;
    align-items: center;
    .navlist{
        width: 90%;
        height: 50px;
        display: flex;
        justify-content: center;
    .nav{
        box-sizing: border-box;
        width: 100%;
        height: 50px;
        background-color: #fff;
        
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        
        line-height: 50px;
        padding: 0;
        margin: 0;
        align-content: flex-start;
        position: relative;
        li{
            list-style: none;
            height: 100%;
            padding: 0 20px;
            a{
                color: #563d7c;
                text-decoration: none;
                font-weight: 500;
                font-size: 16px;
            }
            &:hover{
                background-color: rgb(249,249,249);
            }
        }
        
        li:nth-last-of-type(1){
            position: absolute;
            right: 0;
        }
        
    }
        @media screen and (max-width:1000px) and (min-width:800px) {
            .nav{
                width: 700px;
            min-width: 700px;
            align-content: space-around;
            li{
                padding: 0 10px;
                a{
                    font-size: 14px;
                }
            }
            li:nth-last-of-type(1){
                position: static;
            }
        }
        }
        @media screen and(max-width:800px) {
            
            .nav{
                width: 100%;
                flex-direction: column;
                flex-wrap: nowrap;
                li{
                    background-color: #fff;
                }
                li:not(:nth-of-type(1)){
                    height: 0;
                    transition: height .5s;
                    a{
                        font-size: 0;
                    }
                }
                li:nth-of-type(1)::after{
                    content: "aaa";
                    display: inline-block;
                    margin-right: 10px;
                    float: right;
                }
                li:nth-last-of-type(1){
                    position: static;
                }
                &:active{
                    li{
                        display: inline-block;
                        height: 100%;
                        a{
                            font-size: 16px;
                        }
                    }
                }
            }
            
        }
    }
            @media screen and(max-width:800px) {
            .navlist{
                width: 100%;
            }
            }
    .content{
        width: 100%;
        height: calc(100vh - 50px);
        background-color: #6f5499;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        .logo{
            width: 144px;
            height: 144px;
            border: 2px solid #fff;
            border-radius: 20px;
            font-size: 108px;
            font-weight: bold;
            text-align: center;
            line-height: 144px;
            color: white;
            font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
            
            margin-bottom: 50px;
        }
        .describe{
            font-size: 30px;
            font-weight: 300;
            color: white;
            width: 1000px;
            min-width: 753px;
            text-align: center;
            margin-bottom: 50px;
        }
        @media screen and (max-width:1000px) and (min-width:800px) {
            .describe{
                width: 600px;
                font-size: 25px;
            }
        }
        @media screen and (max-width:800px) {
            .describe{
                width: 70%;
                font-size: 20px;
            }
        }
        
        .download{
            border: 1px solid white;
            border-radius: 15px;
            padding: 15px 35px;
            margin-bottom: 15px;
            a{
                font-size: 20px;
                color: white;
                text-decoration: none;
            }
        }
        .versionDes{
            color: #9783b9;
            font-size: 14px;
            margin-bottom: 30px;
        }
        .hr{
            width: 90%;
            border-bottom: 1px solid #444444;
            margin-bottom: 30px;
        }
        .shequ{
            padding: 15px 35px;
            border: 1px solid white;
            border-radius: 15px;
            a{
                text-decoration: none;
                font-size: 20px;
                color: white;
            }
        }
        .juejin{
            a{
                text-decoration: none;
                font-size: 15px;
                color: #bdb0d4;
                &:hover{
                    color: #dcd2ef;
                }
            }
        }
    }
}



```