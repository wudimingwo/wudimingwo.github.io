
call
```
Function.prototype.myCall = function (context) {
     	var context = context || window;
     	context.fn = this;// 这就完成this指向的改变了.
     	var arr = [];
     	// arguments是个类数组,我们要想办法打开他.这个还挺不好理解的,
     	// 在eval里 字符串变成了变量.
     	// '' + arr 会打开数组
     	// 我们只要让 打开的数组的每一项都是变量就可以.
     	for(var i = 1;i < arguments.length;i++) {
     	  arr.push('arguments[' + i + ']');
     	}
     	var result = eval('context.fn(' + arr + ')');
     	delete context.fn;
     	return result;
     }
```
apply
```
Function.prototype.myApply = function (context,arr) {
     	var context = context || window;
     	context.fn = this;
     	var newArr = [];
     	for(var i = 0;i < arr.length;i++) {
     	  newArr.push('arr[' + i + ']');
     	}
     	var result = eval('context.fn(' + newArr + ')');
     	delete context.fn;
     	return result;
     }
```
有了es6的语法糖,能更轻松打开数组
```
      Function.prototype.myCall = function (context) {
        var context = context || window;
        context.fn = this;
        var args = [];
        for(var i = 1;i < arguments.length;i++) {
          args.push(arguments[i]);
        }
        var result = context.fn(...args)
        delete context.fn;
        return result;
     }

      Function.prototype.myApply = function (context,arr) {
        var context = context || window;
        context.fn = this;
        var result = context.fn(...arr);
        delete context.fn;
        return result;
     }
```
其实对比原生的我发现还是有不同的.
原生的call 可以传原始值.
