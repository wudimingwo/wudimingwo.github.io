
异步对象传统写法?
```
        function aaa (callback) {
        	setTimeout(function () {
        		callback(5);
        	},1000);
        }
        
        function done (value) {
        	console.log(value);
        }
        
        aaa(function (value) {
        	done(value)
        });
```
疑问? 为什么不这么写
```
function aaa (callback) {
        	setTimeout(function () {
        		callback(5);
        	},1000);
        }
        
        function done (value) {
        	console.log(value);
        }
        
        aaa(done);
```
jq上的写法
```
var defer = $.Deferred();
        setTimeout(function () {
        	defer.resolve(5);
        },1000);
        var filtered = defer.then(function (value) {
        	return value * 2;
        });
        filtered.done(function (value) {
        	console.log('打印值',value);
        })

减少回调函数的嵌套?逻辑扁平化?
```