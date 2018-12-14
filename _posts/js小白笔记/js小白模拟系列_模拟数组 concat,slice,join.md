concat
版本1.0  只能接收一个参数
```
Array.prototype.concat = function (arr) {
           	var self = this;
           	var newArr = [];
           	var len1 = self.length;
           	var len2 = arr.length;
           	var len = len1 + len2;
           	
           	for(var i = 0;i < len;i++) {
           	  if(i < len1) {
           	    newArr[i] = self[i];
           	  }else {
           	    newArr[i] = arr[i - len1];
           	  }
           	}
           	return newArr;
           }
```
版本2.0 用了各种数组的方法, 感觉很幸福.. 当然我们还是要试着只用for if 来写, 不过 用方法写,思路真的是比较清楚.
```
Array.prototype.concat = function() {
        var self = this;
        var newArr = [];
        var args = [].slice.call(arguments);
        self.forEach(function (item) {
        	newArr.push(item);
        });
        
        args.forEach(function (item) {
        	item.forEach(function (item1) {
        		newArr.push(item1);
        	})
        })
        
        return newArr;
      }
```
版本3.0 这是翻译2.0而来的,很快  如果不先写2.0 要写3.0可能会很慢.
```
Array.prototype.concat = function() {
        var self = this;
        var newArr = [];
        var args = [];
        var lastIndex = 0;
        
        for(var i = lastIndex; i < self.length; i++) {
          newArr[i] = self[i];
        }
        lastIndex = self.length;
        
        for(var i = 0; i < arguments.length;i++) {
          arguments[i];
          for(var j = 0; j < arguments[i].length;j++) {
            newArr[lastIndex + j] = arguments[i][j];
          }
          lastIndex += arguments.length;
        }
        return newArr;
      }
```
slice  截取是半开半闭[a,b)
```
Array.prototype.slice = function (a,b) {
        	var arr = this;
        	var newArr = [];
        	var a = a || 0;
        	var b = b || arr.length;
        	for(var i = a; i < b;i++) {
        	  newArr[i - a] = arr[i];
        	}
        	
        	return newArr;
        }
```
join 
```
 Array.prototype.join = function (str) {
        	var arr = this;
        	var newStr = '';
        	var str = str || ',';
        	var len = arr.length;
        	for(var i = 0; i < len - 1;i++) {
        	  newStr += arr[i] + str;
        	}
        	return newStr + arr[len - 1]
        }

渡一讲的是,上面这种字符串拼接的方式不好,
因为字符串是存在栈中,先进后出.
用join更好.
```
========================================
2018/11/5
重练一遍
```
        <script type="text/javascript">
          // 返回新数组
            Array.prototype.myConcat = function () {
            	var self = this;
            	var arr = [];
            	for(var ii = 0; ii < self.length; ii++) {
            	  arr[ii] = self[ii];
            	}
            	var len = arguments.length;
            	for(var i = 0; i < len; i++) {// 取出所有传进来的数组
            	  var iArr = arguments[i];
            	  var iLen = iArr.length;
            	  for(var j = 0; j < iLen; j++) {// 取出所有元素.赋值给arr
            	    // 问题: 如何更改arr 的索引? 很简单, 每次都获取自己的length 在末尾添加即可
            	    // 这样似乎从形式上更简洁.
            	    var aLen = arr.length;
            	    arr[aLen] = iArr[j];
            	  }
            	}
            	return arr
            }
            
            
            Array.prototype.mySlice = function (start, end) {
            	var self = this;
            	var arr = [];
            	// 原来的数组不改变.
            	// 截取的问题// 先考虑两个参数都有的情况.
            	// 兼容负数
            	// 默认值 start = 0; end = len
            	var len = self.length;
            	var start = start > 0 ? start : len + start; 
            	var end = end > 0 ? end : len + end; 
            	isNaN(start) && (start = 0);
            	isNaN(end) && (end = len);
            	for(var i = 0; i < len; i++) {
            	  if (i >= start && i < end) {
            	    var aLen = arr.length;
            	  	arr[aLen] = self[i]
            	  }
            	}
            	return arr;
            }
            
            
            Array.prototype.myJoin = function (str1) {
            	var self = this;
            	if (typeof str1 == "undefined") {
            		var str1 = ","
            	} else {
            	  var str1 = str1
            	}
            	console.log(str1);
            	var str = "";
            	var len = self.length;
            	for(var i = 0; i < len - 1; i++) {
            	  str += self[i] + str1
            	}
            	str += self[len - 1];
            	return str
            }
            
            
            var arr1 = [1,2,3];
            var arr2 = [11,22,33];
            var arr3 = [1111,2222,3333];
            var arr4 = [1111,2222,3333];
            var arr = arr1.myConcat(arr2,arr3,arr4);
            console.log(arr);
            var newArr = arr.mySlice();
            console.log(newArr);
            
            var str = arr.myJoin(",0,")
            var str1 = arr.join(",0,")
            console.log(str);
            console.log(str1);
            
        </script>
```