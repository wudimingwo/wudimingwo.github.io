
版本1.0
```
function myNew (fn) {
     	var self = Object.create(fn.prototype);
     	return function () {
     		fn.apply(self,arguments);
     		return self
     	}
     }
```
版本2.0
```
function myNew (fn) {
     	var self = {};// 实际上这里是用了new Object的
        self.__proto__ = fn.prototype;
     	return function () {
     		fn.apply(self,arguments);
     		return self
     	}
     }
```
版本3.0
```
在另一篇里也提过,这一篇似乎写重了
      function myNew(fn) {
        var self = Object.create(fn.prototype);
        return function() {
         var result = fn.apply(self, arguments);
         if (typeof result == "object") {
         	return result
         }
          return self
        }
      }

```