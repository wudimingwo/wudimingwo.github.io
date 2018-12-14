版本1.0 for循环
```
      var arr = [123,456,79,456,79,13,46,8798];
      function theMax (arr) {
        var len = arr.length;
        var bigNum = arr[0];
        for(var i = 0;i < len; i ++){
          if(bigNum < arr[i]){bigNum = arr[i]}
        }
        return bigNum
      }
      console.log(theMax(arr));
```
版本2.0 api sort()
```
      function theMax (arr) {
      	arr.sort(function (a,b) {
      		return b - a//降序
      	});
      	return arr[0];
      }
      
      
      console.log(theMax(arr));
```