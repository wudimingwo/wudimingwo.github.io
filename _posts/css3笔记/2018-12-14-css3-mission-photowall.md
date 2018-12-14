---
layout:     post
title:      "css3作业1 旋转照片墙"
subtitle:   " \"css3笔记\""
date:       2018-12-14 12:00:00
author:     "wudimingwo"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - css3
    - Meta
---
html
```
    <div class="wrapper">
      <div>1</div>
      <div>2</div>
      <div>3</div>
      <div>4</div>
      <div>5</div>
      <div>6</div>
    </div>
```
main.scss
最近刚开始练习scss, 虽然还不太会用,但确实方便很多
```
@import "./new_file.scss";
:root{
    width: 100%;
    height: 100%;
}
body{
    margin: 0;
    padding: 0;
    @include base-size(100%,100%, #323232);
    position: relative;
    perspective: 1000px;
    
    .wrapper{
        transform-style: preserve-3d;
        transition: transform 10s;
        width: 400px;
        height: 250px;
        position: absolute;
        left: 50%;
        top: 50%;
        margin-left: -250px;
        margin-top: -125px;
        div{
            position: absolute;
            width: 100%;
            height: 100%;
            background-color: #F08080;
            background-size: cover;
            background-repeat: no-repeat;
        }
        @for $i from 1 through 6 {
            div:nth-of-type(#{$i}){
                background-image: url(../img/#{$i}.jpg);
                transform: rotateY(#{($i - 1) * 60}deg) translateZ(400px);
            }// 这里这种运算感觉就能省很多代码
        }
        &:hover{
            transform: rotateY(720deg);
        }
    }
}

```
new_file.scss
```
@mixin base-size($width,$height,$color){
    width: $width;
    height: $height;
    border: 1px solid black;    
    background-color: $color;
}
```