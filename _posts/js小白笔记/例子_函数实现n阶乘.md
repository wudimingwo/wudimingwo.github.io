版本1.0
```
var fun = (function() {

        return function(n) {
          var num = 1;
          for(var i = 1;i <= n;i++) {
            num *= i;
          }
          return num
        }
      })();
```