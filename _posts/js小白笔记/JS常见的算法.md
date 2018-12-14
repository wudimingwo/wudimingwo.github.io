原文链接:
https://www.cnblogs.com/lvmylife/p/7208541.html
http://www.jackpu.com/qian-duan-mian-shi-zhong-de-chang-jian-de-suan-fa-wen-ti/
当然还有渡一的一些内容

抄写一遍练习,放在自己的地方好查阅嘛~

Q1.判断是否是回文
```
function huiwen (str) {
      	return str == str.split('').reverse().join('');
      }
```
Q2.数组去重
版本1.0 对象方法
```
var arr = [1,1,1,2,2,2,3,3,3];
      function unique (arr) {
      	var obj = {};
      	var newArr = [];
      	for(var i = 0;i < arr.length;i++) {
      	  if(!obj[arr[i]]){
      	    obj[arr[i]] = 1;
      	    newArr.push(arr[i]);
      	  }
      	}
      	return newArr;
      }
      console.log(unique(arr));

放原型链上
Array.prototype.unique = function () {
             var arr = this;
          	var obj = {};
          	var newArr = [];
          	var len = arr.length;
          	for(var i = 0;i < len ; i++) {
          	  if(!obj[arr[i]]) {
          	    obj[arr[i]] = 1
          	    newArr.push(arr[i]);
          	  }
          	}
          	return newArr
          }
```
版本2.0 indexof?
```
      var arr = [1,1,1,2,2,2,3,3,3];
      function unique (arr) {
      	var newArr = [arr[0]];
      	for(var i = 1; i < arr.length;i++){
      	  if(newArr.indexOf(arr[i]) === -1) {
      	    newArr.push(arr[i]);
      	  }
      	}
      	return newArr
      }
      console.log(unique(arr));
```
版本3.0 先排序后比较?
```
var arr = [1,5,9,6,3,5,87,,,5,71,1,2,2,2,3,3,3];
      function unique (arr) {
      	var arr = [].concat(arr.sort(function (a,b) {
      		return a - b;
      	}));
      	var newArr = [arr[0]];
      	for(var i = 1;i < arr.length; i++) {
      	  if(arr[i] !== arr[i - 1]) {
      	    newArr.push(arr[i]);
      	  }
      	}
      	return newArr
      }
      console.log(unique(arr));
```
Q3 求一组数组中,每个元素出现的次数. 来自 Q1版本1.0的启示
当然这个也可以用在字符串,只需要split('')就变成数组了
```
var arr = [1,5,9,6,3,5,87,,,5,71,1,2,2,2,3,3,3];
      function times (arr) {
      	var obj = {};
      	
      	for(var i = 0; i < arr.length; i++) {
      	  if(!obj[arr[i]]){
      	    obj[arr[i]] = {
      	      time : 1,
      	      value : arr[i],
      	      place : [i]
      	    }
      	  }else {
              obj[arr[i]].time += 1;
              obj[arr[i]].place.push(i);
            }
      	}
      	return obj;
      }
      console.log(arr);
      console.log(times(arr));

这个启示是,我们可以把一个数据,变成另一个数据,
这要怎么说呢,
如果一个数据的处理,需要提供跟这个数据相关的数据的时候,
我们可以把这个数据和相关数据都打包成一个对象,
这样就好处理?

或者另一个启示是, 我们可以用创建对象的方式, 给任何一个数据进行不同的标记?
```
Q4统计一个字符串出现最多的字母
版本1.0
```
      var str = 'akgjaljdglasjg';
      function findMaxDuplicateChar (str) {
        var arr = str.split('');
      	var obj = {};
      	for(var i = 0; i < arr.length;i++) {
      	  if(!obj[arr[i]]) {
      	    obj[arr[i]] = 1;
      	  }else {
      	    obj[arr[i]] += 1;
      	  }
      	}
      	var strChar = '';
      	var max = 1;
      	for(var key in obj) {
      	  if(obj[key] >= max) {
      	    strChar = key;
      	    max = obj[key];
      	  }
      	}
      	return strChar;
      	
      }
      console.log(findMaxDuplicateChar(str));

这个版本是有缺点的,如果存在出现次数相同的字母,他只会返回一个,而不是全部
```
版本2.0
```
var str = 'akgjaljdglasjg';
      function findMaxDuplicateChar (str) {
        var arr = str.split('');
      	var obj = {};
      	for(var i = 0; i < arr.length;i++) {
      	  if(!obj[arr[i]]) {
      	    obj[arr[i]] = 1;
      	  }else {
      	    obj[arr[i]] += 1;
      	  }
      	}
      	var strChar = [];
      	var max = 1;
      	for(var key in obj) {
      	  if(obj[key] > max) {
      	    strChar = [key];
      	    max = obj[key];
      	  }else if(obj[key]  ==  max) {
      	    strChar.push(key);
      	  }
      	}
      	return strChar;
      	
      }
      console.log(findMaxDuplicateChar(str));
```
Q排序算法,算法那一篇有写一点,这里先不重复了.

Q5,不借助变量,进行两个整数的交换
```
function swap (a,b) {
      	a = a - b;
      	b = a + b;
      	a = b - a;
      	return [a,b]
      }
      var a = 5,
          b = 4;
      console.log(swap(a,b));

类似的
 a = a * b;
 b = a / b;
 a = a / b;

其实第一次接触的时候,觉得很神奇,
两个容器可以存放着 3个值?

```
Q6  使用canvas 绘制一个有限度的斐波那契数列的曲线？ 返回一个数组
版本1.0
```
function getFibonacci (a, b, n) {
      	var c;
      	var arr = [a,b];
      	if(n == 1) {return [a]};
      	if (n == 2) {return [b]};
      	if (n > 2) {
      	  for(var i = 3; i <= n; i++) {
      	    c = a + b;
      	    a = b;
      	    b = c;
      	    arr.push(c);
      	  }
      	}
      	return arr;
      }
      
      console.log(getFibonacci (0, 1, 1));
for循环版本,感觉挺丑的.
```
版本2.0
```

function getFibonacci(n) {  
  var fibarr = [];
  var i = 0;
  while(i<n) {
    if(i<=1) {
      fibarr.push(i);
    }else{
      fibarr.push(fibarr[i-1] + fibarr[i-2])
    }
    i++;
  }

  return fibarr;
}
还是和for循环一样
这个是那位博主的版本,确实比我的妙. 

能不能有个递归版本? 

```
版本3.0 递归版//非常粗糙,性能很差,但还是挺练人的.
```
根据2.0 改造而来
function getFibonacci(a,b,n) {
        var fibarr = [];
          if(n == 1) {
            fibarr.push(a);
            return fibarr;
          } else if(n == 2){
            fibarr.push(b,a);
            return fibarr;
          } else {
            fibarr.push(getFibonacci(a,b,n - 1)[0] + getFibonacci(a,b,n - 2)[0]);
            fibarr = fibarr.concat(getFibonacci(a,b,n - 1));
          }
        return fibarr;
      }

      console.log(getFibonacci(0,1,1));

我相信递归一定还有比这个更简洁的...
```
后来又写了下,,
```

            function fibonaci2 (n) {
              
              var a = 1;
              var b = 1;
            	if (n == 1) {
            		return a
            	}else if (n == 2) {
            		return b
            	}
            	return fibonaci2(n - 1) + fibonaci2(n - 2);
            }
            console.log(fibonaci2(8))


            function fibonaci3 (n) {
              var arr = arr || [1,1];
              if (n == 1) {
              	return [1]
              }else if(n == 2) {
                return arr;
              }
              n = n - 2;
              while (n--){
              	arr.unshift(arr[0] + arr[1]);
              }


            function fibonaci4 (n) {
            	if (n == 1) {
            		return [1]
            	}else if (n == 2) {
            	  return [1,1]
            	}
            	var arr = fibonaci4(n - 1)
            	var temp = arr[0] + arr[1];
            	arr.unshift(temp);
            	return arr
            	
            }


         function fibonaci (n) {
           var arr = [];
           var a = 1;
           var b = 1;
           arr.push(a);
           arr.push(b);
           
         	while (n--){
         	  var c = a + b;
         	  arr.push(c);
         	  a = b;
         	  b = c;
         	}
         	console.log(arr);
         	return arr
         }
```



Q7 找出下列正数组的最大差值
版本1.0
```

var arr = [1,2,3,4,5,6,7,8,9,10];
      function getMaxProfit (arr) {
      	var arr = [].concat(arr);
      	var maxNum = arr[0];
      	var minNum = arr[0];
      	for(var i = 1; i < arr.length;i++) {
      	  maxNum = Math.max(maxNum,arr[i]);
      	  minNum = Math.min(minNum,arr[i]);
      	}
      	return maxNum - minNum;
      }
      console.log(getMaxProfit(arr));

      用api确实省事,一个Math.max(),Math.min() 能省去很多判断语句,语义化还好.
```
版本2.0
```

var arr = [1,2,3,4,5,6,7,8,9,10];
      function getMaxProfit (arr) {
      	var arr = [].concat(arr);
      	
      	var minPrice = arr[0];
      	var maxProfit = 0;
      	
      	for(var i = 1,len = arr.length; i < len;i++) {
      	  var currentPrice = arr[i];
      	  minPrice = Math.min(minPrice,currentPrice);
      	  
      	  var potentialProfit = currentPrice - minPrice;
      	  
      	  maxProfit = Math.max(maxProfit,potentialProfit)
      	}
      	return maxProfit;
      	
      }
      console.log(getMaxProfit(arr));

博主写的真是服了,
我刚接触js的时候, 觉得把变量名取的很长,用的英文单词用的很溜,
就感觉很高大上.让我感觉很高深,很难.
其实就是语义化的问题, 要告诉自己, 这个只不过就是变量名而已.
你敢相信,我刚开始遇到类似 $dom ,_this  变量名的时候,心理觉得那么高深,
其实只不过是个变量而已啊..
所以诸位小白, 你们不要被这些所谓长英文单词给吓住了.


过了两个多月,重新看,这个版本是有问题的.
var arr = [55,2,21,3,4,5,1,7,8,9,10,11,12,13];
无法找出最大差值.
```
可以用排序api
```
            function chazhi (arr) {
            	// 排序 // 第一个和最后一个相减
            	var newArr = [].concat(arr);
            	var len = arr.length - 1;
            	newArr.sort(function (a,b) {
            		return a - b
            	});
            	
            	console.log(newArr[len] - newArr[0]);
            	return newArr[len] - newArr[0];
            }
```

Q8 随机生成指定长度的字符串
版本1.0
```
function makeStr (n) {
      	
      	var str = '';
      	for(var i = 0; i < n; i++) {
      	  str += String.fromCharCode(Math.floor((Math.random()*(123 - 65) + 65)));
      	}
      	return str;
      }
      
      console.log(makeStr(3));

```
版本2.0
```
 function makeStr (n) {
      	
      	var str = 'abcdefghijklmnopqrstuvwxyz9876543210';
        var temp = '',
            i = 0,
            l = str.length;
           for(var i = 0; i < n;i++){
            temp += str.charAt(Math.floor(Math.random() * l));
        }
           return temp;
         }
      console.log(makeStr(3));
```
版本3.0
```
            function makeStr (n) {
              var str = "abcdefghijklmnopqrstuvwxyz";
              var str1 = str.toUpperCase();
              var strArr = (str + str1).split("");
              var len = strArr.length;
              var newStr = "";
              while (n--){
              	newStr += strArr[parseInt(Math.random() * len)]
              }
              console.log(newStr);
              return newStr;
              
            }
// 但其实这也是违反开闭原则的. 如果我们想 增加随机返回的字符串的范围.

            function MakeStr () {
            	var str = "abcdefghijklmnopqrstuvwxyz";
              var str1 = str.toUpperCase();
              this.strArr = (str + str1).split("");
              this.newStr = function (n) {
              	var newStr = "";
              	var len = this.strArr.length;
                while (n--){
                  newStr += this.strArr[parseInt(Math.random() * len)]
                }
                return newStr;
              };
              
              this.addStr = function (str) {
                
                var arr = str.split("");
                for(var i = 0; i < arr.length;i++) {
                  if (this.strArr.indexOf(arr[i]) == -1) {
                  	this.strArr.push(arr[i]);
                  }
                }
              }
            }
            
            var makestr = new MakeStr();
            makestr.addStr("1234567890");
            makestr.addStr("1234567890|");
            makestr.newStr(8);
// 最近刚学设计模式, 一有机会就练一练 面向对象
```

Q9 实现类似getElementsByClassName 的功能
版本1.0
```
HTMLDocument.prototype.getEleByClassName = function (str) {
      	var allEle = document.body.getElementsByTagName('*');
      	var len = allEle.length;
      	var arr = [];
      	for(var i = 0; i < len ; i++) {
      	  var classlist = allEle[i].className.split(' ');
      	  var clen = classlist.length;
      	  for(var j = 0; j < clen;j++) {
      	    if(classlist[j] == str) {
      	      arr.push(allEle[i]);
      	    }
      	  }
      	}
      	// 本来直接返回 arr 就可以, 但我们转换成一个类数组 再返回,模拟的逼真一点..
      	var obj = {};
      	for(var key in arr) {
      	  obj[key] = arr[key];
      	}
      	obj.length = arr.length;
      	return obj;
      };
      
      console.log(document.getEleByClassName('box'));
```
版本2.0
```
function queryClassName(node, name) {  
  var starts = '(^|[ \n\r\t\f])',
       ends = '([ \n\r\t\f]|$)';
  var array = [],
        regex = new RegExp(starts + name + ends),个人觉得 这一句很牛逼,我们可以用变量随意制造正则了.
        elements = node.getElementsByTagName("*"),
        length = elements.length,
        i = 0,
        element;

    while (i < length) {
        element = elements[i];
        if (regex.test(element.className)) {
            array.push(element);
        }

        i += 1;
    }

    return array;
}

这位博主的是正则表达式版本,
555,正则还需要练习啊
```
Q10 二叉树待理解之后再抄写