版本1.0 用new模拟
```
Object.myCreate = function (obj) {
     	function F () {};
     	F.prototype = obj;
     	return new F();
     }
```
版本2.0
```
Object.myCreate = function (obj) {
       var newObj = {} // 实际上用了 new Object
     	newObj.__proto__ = obj;
     	return new F();
     }
```