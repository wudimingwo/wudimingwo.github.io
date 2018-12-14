首先应该怎么看待this? this是什么?
下面我说的不是定义, 而是一种理解方式.

第一种理解方式:
this就是告诉你谁调用了方法.
```
var obj = {};
obj.test = function (){console.log(this)}
obj.test();//指向obj
obj['test']();//一样是obj
上面这种情况好理解.谁看都知道是obj调用的.
重点不是,test定义在了哪里,而是谁调用了test

var obj2 = {};
obj2.test = obj.test;
obj2.test()// 指向obj2 
到这里也简单.


function test () {
      	console.log(this); 指向window
  }
  test();
在全局当中
test() 就相当于 window[test]();
所以也好理解.

(function () {
      	function test () {
      		console.log(this);// 指向window
      	}
      	test();
      })();
这就不对了,按照理解,应该是指向立即执行函数的AO或者[[scope]]这种东西才对吧?
这个时候,我们只能这么理解,
每个函数 预编译的时候, this默认指向window.

(function () {
      	function test () {
      		console.log(this[test.name]);// test.name 返回'test' this指向window 
      	}// 所以 this[test.name] 相当于 window['test'] ,test没在全局定义,自然是undefined;
      	test();
      })()

上面说了个废话,但我就是想要理解成,谁调用就指向谁.
所以我故意理解成这样. 

我们假设 test 定义在 AO这个我们无法访问的对象中.
test();运行的时候,
window.test = AO.test;
window.test();
delete window.test;

上面这段话什么用都没有,你只需要记住函数预编译的时候,this默认指向window就可以了.
千万别跟人说浏览器就是这么运行的.
我这么理解的原因是,我想让--谁调用这个方法,this就指向谁--这个逻辑完全说得通.
```
第二种理解方式:
this就是一个函数的传参入口.
```
这是从函数的角度上来说的.

function test () {}
实际上他是有两个传参入口的.
一个是()传给arguments
一个是.前面的对象, 传给this;

一般来讲,通过this传进来的都是一个对象,或者包装类,(当然也可以是任何数据类型.)
这个好理解,调用嘛,想要调用一个函数,通常就是个对象.

所以为什么好多方法要定义在原型链上?
因为实例可以调用原型链上的方法,
谁调用方法,this就指向谁,
this就是个参数,
所以,谁调用方法,就把自己当做参数传了进去.


比如说,我们要返回一个数组最后一位的元素.
function returnLast(arr){
    return arr[arr.length - 1];
}
这里我们传参是通过()这个参数入口的.
我们想把arr放在this入口,
那么应该是这种形式,
arr.returnLast();
有两个办法可以达到,
第一种,
arr.returnLast = function () {
    return this[this.length - 1]
}
arr.returnLast();
但这样太low了,你更改了arr本身,
(而且我刚开始以为会出问题,因为arr添加了returnLast length可能会改变的吧?
结果没变.. 这里我就不展开了.)

第二种,放在原型上

var arr = [1,2,3,4,5,6];
      Array.prototype.returnLast = function () {
         return this[this.length - 1]
       }
    arr.returnLast();

```
