解决的是一个异步问题

```
function dy (list,callback) {
            setTimeout(function () {
              var task = list.shift();
              task();
              if (list.length > 0) {
              	setTimeout(arguments.callee,1000);
              } else{
              	callback();
              }
            	
            },25);
          }
          
          dy([
            function () {
            	alert('a');
            },
            function () {
              alert('b');
            }
          ],
          function () {
          	alert('callback');
          });


```


jq提供的方法
![image.png](https://upload-images.jianshu.io/upload_images/13637909-555da96be7626944.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```
用例
var callbacks = $.Callbacks('once');
          callbacks.add(function () {
          	alert('a');
          })
          callbacks.add(function () {
          	alert('b');
          })
          
          callbacks.fire();
          callbacks.fire();
```