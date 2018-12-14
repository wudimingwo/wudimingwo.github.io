函数的定义形态
```
var name = function () {};
function name () {};
var name = function test () {};//test失效,为undefined
```
函数的执行形态
```
1.定义的同时执行: 立即执行函数:自执行函数
(function  () {} )();//标准1
(function () {} ());//标准2
+function () {} ();//只要有计算符号在前,就会执行

name();//一般执行方式
obj.name();//一般执行方式2
obj.name.call(obj2);//一般执行方式3
obj.name.apply(obj3);//一般执行方式4
```
函数的变量形态
```
function name () {};
var test = name;
var obj = {};
obj.test = name;

当做变量进行赋值操作.

obj.test();//与name 相比,更换了this.
```


形参,实参
```
形参
function name (a,b,c) {

}
实参
name(a,b,c);

(function (a,b,c) {})(a,b,c);

从结果上看,形参和实参的值可能一样,
但实际上,形参的值是由实参决定的.
或者说, 这里是有数据的流向的.
实参 ==> 形参
```

arguments 实参列表
```
function name () {
  console.log(arguments);
}
name(1);
name(1,2,3);
```
形参长度:记得好像在函数的柯里化有用到.
```
function name (a,b,c){};
console.log(name.length);
```

this
```
每个函数都有自己的arguments,
也都有自己的this,

function name () {
  return this//默认指向window
}

把this想象成一个参数入口.
```
return
```
每个函数都有一个return
如果不定义return 默认 return undefined

function name () {
  return this;//可以返回this
}

function name () {
  return arguments;//可以返回arguments
}

return 可以返回任何数据类型,任何东西. 并且相当于是赋值操作 =
这样就很牛逼了.
name();可以是任何数据.

function name () {
  var num = 123;
  var str = 'str';
  var boo = false;
  var fun = function () {};
  var obj = {};
  var arr = [];
  return anything
}

所以函数是有两个基本作用的.
1. 代码功能块. 一些操作的集合.
2. 赋值.

var a = (function () {return})();
用这种方式进行赋值,可以实现变量私有化(闭包的利用);
一度怀疑这才是赋值的正确方式.
```
```
有一个问题
function name (a,b) {
  var obj = {};
  obj.a = a;
  obj.b = b;
  return obj
}
var obj = name(1,2);
和
var obj = {}
function name (a,b) {
  obj.a = a;
  obj.b = b;
}
name(1,2);
从结果上看,都完成了对obj的处理.
但他们是有区别的.

第一个用ruturn的方式向外传递数据时,可以赋值给任何变量,
在赋值之前也不会污染变量.
数据的流向是清晰的.

第二个直接引入全局变量,也就是,这个函数,只能为这个变量服务.
否则数据的流向是混乱的.
所以也许应该这么写

var obj = {};
obj.name = function (a,b) {obj.a = a;obj.b = b}

类似的就是
function Name () {}
var obj = new Name();
Name.prototype.name = function (a, b) {this.a = a;this.b = b}
这种实例生成的对象,和普通的对象的区别是,
一般会把变量挂在生成的obj上,
而把方法挂在原型链上.



```


当我们考虑一个函数的时候,
要分清,是他的定义形态?还是执行形态?
他的实参是什么?
他的形参是什么?
他的this是什么?
他的return 到底是什么?
遇到每一个函数的时候,下意识的问一下,就会好很多.

