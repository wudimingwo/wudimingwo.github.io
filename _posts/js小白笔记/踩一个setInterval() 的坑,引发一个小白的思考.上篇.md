先说结论:setInterval 是无法return的

我们先假定基本需求是这样的
版本1.0
```
            var speed = 50;
            var timer = null;
            function conlog (a) {
              console.log(a);
            }
            
            function minuse (speed) {// 重点讨论这个部分
            	while (1){
            	  speed--;
            		if(speed <= 10){
            		  return speed;
            		}
            	}
            }

            conlog(minuse(speed));

            
```
我们也可以这样
版本2.0
```
function minuse (speed) {// 够小白吧, 我都觉得自己蠢.
            	while (1){
            	  speed--;
            		if(speed <= 10){
            		  break;
            		}
            	}
            return speed;
            }

conlog(minuse(speed));
```
最蠢的是这个,我想setInterval 是不是也可以看成一个循环.
版本3.0
```
function minuse (speed) {
            	setInterval(function () {
            		speed--;
            		if (speed <= 10) {
            			return speed;
            		}
            	},1000);
            }
conlog(minuse(speed));
够蠢吧? 这能行吗?这根本不行好嘛.
因为 那个return 对应的是 setInterval 里的回调函数, 根本不是 函数minuse的return
也就是说,回调函数中的return 很多时候都是传不出去的,因为函数定义的时候就没有设置接收.

```
比如说forEach
```
var arr = [1,2,3,4,5,6];
function returnNum (arr) {
            	arr.forEach(function (item,index) {
            		if(item <= 5){
            		  return item;
            		}
            	})
            }
 returnNum (arr); 
这能返回嘛? 根本返回不了好嘛.. (关于forEach的源码模拟可以出门左拐看一下js小白模拟系列.)
因为forEach 在数组原型链上定义的时候,根本就没有设置接收.
或者说,只要function 有嵌套的(有回调函数) 那么就要小心你的return 有可能失效.

如果用reduce应该可以,但这跟我要想说的没关系,就不说了.

这个时候有没有解决的办法? 有,比如这么写.

function returnNum (arr) {
      var num;
            	arr.forEach(function (item,index) {
            		if(item <= 5){
            		  num = item;
            		}//
            	})//
          return num;
            }// 
其实这里也有问题,假设我的需求是返回第一个满足要求的数字,
而用forEach ,num返回的是最后一个满足要求的数字
可以这样
function returnNum (arr) {
      var num;
      var flag = true;
            	arr.forEach(function (item,index) {
            		if(item <= 5 && flag == true){
            		  num = item;
                          flag = false;
            		}
            	})
          return num;
            }
反正这样勉强也算完成需求了.


```
我们回到setInterval,我立刻犯了第二个足够蠢的错误.
```
function minuse (speed) {
      var speed1,flag = true;
                setInterval(function () {
                    speed--;
                    if (speed <= 10 && flag == true) {
                         speed1 = speed;
                        flag = false;
                    }
                },1000);
              return speed1;
            }
conlog(minuse(speed));

这行吗?这还是不行,估计有人已经笑掉牙了,
这个跟setInterval 执行顺序有关,(可以自己搜一下百度)
简单讲就是,setInterval里的代码会等主线程的代码执行完再执行,
也就是说 return speed1 会比setInterval里的代码先执行,也就是会 return 一个undefined
```
然后你就发现一个问题,
那就是,setInterval里的变量,你是return 不出去的!
```
你先不要笑我.
实际上我目前的阶段,正在思索练习怎么写一些基本的结构的问题.

我目前的总结是,
一个函数里面所有的变量,尽量通过参数来引入.
我是这么想的,
一个函数里的变量,引入的方式,无非是两种,
一种是通过参数来引入,另一种是直接引用全局变量.
很明显第一种比第二种,数据的流向更清晰一点,
(但有时,不用全局变量会很痛苦)

假设我在一个函数里,要调用另一个函数,如果可能,
让这个函数也通过参数的形式传进来(也就是回调函数)
当然尽量能不调用,就不调用.降低依赖性嘛.

然后还有一个小练习就是,如果一个函数的执行,最后确定是要返回一个数据的话,
那么最好是return 出去. 而不是在 这个函数里调用另一个函数.

上面这几个总结,其实还蛮有用的.
我还驾驭的不太好,
特别是,遇到setInterval就会出问题,思维很容易混乱.
```
其实是这样的.
```
学完dom之后,有这样一种总结,
先写一段很蠢的代码

function minuse (speed) {
              var speed = speed;
            	div.onclick = function (e) {
            		speed--;
            		if(speed <= 5) {
            		  return speed;// 要么这里
            		}
            	}
            	return speed;// 要么这里
            }

基本上正常人是不会这么写的.因为永远都不会达到需求.

这个总结是:监听器,执行代码之后,无法return数据, 只能调用函数来处理数据?
或者说,监听器只能成为数据的源头?

一般是这么写的吧?
var speed;
div.onclick = function () {
    speed--;
    if(speed <= 5){
   conlog(speed);// 而不是把 speed return出去.
}

}


而setInterval其实是个监听器.
```
所以一般是这么写的吧?
```
timer = setInterval(function () {
                    speed--;
                    if (speed <= 10) {
                        clearInterval(timer);
                        conlog(speed);
                    }
                },1000);
```
但是我发现还有另外一种用法,看下篇.