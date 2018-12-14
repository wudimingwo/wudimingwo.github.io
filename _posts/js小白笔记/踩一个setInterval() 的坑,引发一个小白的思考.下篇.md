下面这篇文章都是刚接触js不久学习时写下的.
我都有点看不懂自己写的是啥,
虽然逻辑混乱,概念不清,
但总归有思考过的痕迹,

=========
上篇里最后说,一般我们不会把监听器封装起来,我看到的很少,
但下面这个可能你见过类似的.
```
function movex (target,ele,callback) {
              var icur;
              clearInterval(ele.timer);
              ele.timer = setInterval(function () {
                icur = ele.offsetLeft;
              	var speed = (target - icur) / 7;
              	ele.style.left = icur + speed + 'px';
              	if(Math.abs(icur - target) <= 3) {
              	  clearInterval(ele.timer);
              	 ele.style.left = target + 'px';
              	 callback();
            	}
              },30);
            }
            movex(500,div);

这个是用setInterval 来实现运动的.
从形式上讲,是把setInterval封装进函数里的.

当然,这里是没有return什么值的.特别是没有return setInterval 里面的值.
用了一个 callback() 回调函数.
```
那么类似的,是不是可以这样?
```
function movex (target,ele,callback) {
            	var icur;
            	ele.onclick = function (e) {
            		icur = ele.offsetLeft;
            		var speed = (target - icur) / 7;
            		ele.style.left = icur + speed + 'px';
            		if(Math.abs(icur - target) <= 3) {
            		  ele.onclick = null;
            		  console.log(111);
            		  ele.style.left = target + 'px';
            		  callback();
            		}
            	}
            }
            movex(500,div);
```
知识系统碰到天花板了,

看一下这个
版本1.0
```
         function conlog (something) {
          	console.log(something);
          }
          function getNumber () {//return 出去
          	return 123;
          }
          var a = getNumber()
          conlog(a);
```
也可以这样
版本2.0
```
          function conlog (something) {
          	console.log(something);
          }
          function getNumber () {//调用其他函数
          	conlog(123);
          }
//          getNumber();
```
版本3.0
```
          function conlog (something) {
          	console.log(something);
          }
          
          function getNumber (callback) {// 以回调函数的方式弄了进来.
          	callback(123)
          }
          getNumber(conlog);
```
版本4.0


脑残分析
```
从数据的流向来看,
一定是getNumber 执行完,获得数据后,再执行conlog

如果像版本1.0里一样,所有的数据都可以return 出去,
我觉得语义化倒是真的好.而且结构还很清晰.

如果像2.0里这样,我就觉得结构不是很清晰.而且依赖性也不太好.
像3.0,应该算是回调函数的形式,依赖性虽然好,但总感觉语义化似乎也不是那么好.

问题是,什么时候考虑用return 什么时候考虑用回调?

像有些函数,比如说渲染,他已经到头了,可能也就不需要return了.
像setInterval 我们是无法return的,只能进行回调.
也就是说不是所有函数都能return 
那么是不是所有函数都能用callback的形式?
```
那么是不是所有函数都能用callback的形式?
比如说这样.
```
function conlog (something,callback) {
            	console.log(something);
            	if(typeof(callback) == 'function'){
            	  callback();
            	}
            }
            
            function getNumber (callback) {
            	if(typeof(callback) == 'function'){
                callback(123);
              }
            }
            getNumber(conlog);

尽管conlog似乎不需要什么回调函数.
```
我个人觉得,回调函数最大的作用不是用来去有数据的地方获取数据.
最大的作用是,控制执行顺序.
```
控制执行顺序,起码在两个地方很有用,
1.异步执行代码时,
比如有什么网络请求时,
比如用setIterval的时候
严格来讲,监听器的回调函数也是为了控制执行顺序.?

2.有需要用到循环的时候.
比如说最简单的是,我自身回调,那就是递归函数了.
又比如说,两个函数互相是对方的回调函数,那么这两个函数就会循环.
又比如说,不只是两个函数,而是多个函数,或者一个长链条的函数,
每个函数都可有可能调用上层函数?
这个我得怎么解释呢?
```
我刚开始认为的执行顺序是这样的.
```
1.从上到下,哪个先读取就先执行哪个,这个应该到哪里都是合理的.
            var a = 1;
            var b = 2;
            var c = a + b;
            console.log(c);
2.后来发现有了函数之后,执行顺序取决于函数.
            function conloga () {
            	console.log('a');
            }
            function conlogb () {
              console.log('b');
            }
            function conlogc () {
              console.log('c');
            }
            
            conlogc();
            conlogb();
            conloga();
        这么看的时候感觉也没啥,
        但一旦有了某种条件判断,再加上一些循环,再加上一些嵌套,就有感觉了,这里先不展开.

3.再后来发现,有了dom,有了监听器之后,执行顺序这方面又有点乱了.

4.然后就是刚才想的那个问题,我们想象假设每个函数默认都有一个(多个)回调函数,
那我们是不是就稍微好理解这个执行顺序了?
        
首先,代码确实是有执行顺序的,因为有数据的流向嘛.必须有顺序.
但我之前认为代码执行是一种单向的流动.
现在我觉得如果想成是一种循环的流动,可能更好理解.

每次循环根据不同条件,不同数据状态,路径不同,进行循环.
就好像其他循环一样,我们留一条出口就可以.

然后监听器的作用就可以看成是,每次都能重新启动这个循环?
```
可能是异想天开
```
这样的看待方式,好处是,稍微好理解.
但问题是,数据不好处理.每次回调的时候,如果不是为了数据,而是为了顺序,
那数据要怎么跟过去?数据也要同时传过去?
``` 