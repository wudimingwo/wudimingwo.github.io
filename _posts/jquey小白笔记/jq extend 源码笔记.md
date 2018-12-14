```
jQuery.extend = jQuery.fn.extend = function() {
	var options, name, src, copy, copyIsArray, clone,
		target = arguments[0] || {},
		i = 1,
		length = arguments.length,
		deep = false;

	// Handle a deep copy situation
	if ( typeof target === "boolean" ) {
		deep = target;
		target = arguments[1] || {};
		// skip the boolean and the target
		i = 2;
	}

	// Handle case when target is a string or something (possible in deep copy)
	if ( typeof target !== "object" && !jQuery.isFunction(target) ) {
		target = {};
	}

	// extend jQuery itself if only one argument is passed
	if ( length === i ) {
		target = this;
		--i;
	}

	for ( ; i < length; i++ ) {
		// Only deal with non-null/undefined values
		if ( (options = arguments[ i ]) != null ) {
			// Extend the base object
			for ( name in options ) {
				src = target[ name ];
				copy = options[ name ];

				// Prevent never-ending loop
				if ( target === copy ) {*这里为什么不能写 option === copy呢? 因为一次赋值操作都不执行?
					continue;
				}

				// Recurse if we're merging plain objects or arrays
				if ( deep && copy && ( jQuery.isPlainObject(copy) || (copyIsArray = jQuery.isArray(copy)) ) ) {
					if ( copyIsArray ) {
						copyIsArray = false;
						clone = src && jQuery.isArray(src) ? src : [];

					} else {
						clone = src && jQuery.isPlainObject(src) ? src : {};
					}

					// Never move original objects, clone them
					target[ name ] = jQuery.extend( deep, clone, copy );

				// Don't bring in undefined values
				} else if ( copy !== undefined ) {
					target[ name ] = copy;
				}
			}
		}
	}

	// Return the modified object
	return target;
};
```

https://www.jianshu.com/p/1ba5fb099407
extend和那个深度克隆两相比较所看到的一些缺陷,
以及思考补充写在了上面的笔记中.


extend精彩的地方不仅仅在于深度克隆,
我觉得最神奇的地方是他的参数处理.
```
一般的函数,
function normal (a,b,c,d) {
            if(d){
              console.log(a - b * c);
            }
          }
他的参数的位置以及类型是严格限制的.
有时候一个函数参数一多起来,我们很难记得顺序.
比如ajax(method,url,data,callback,flag);
一个顺序不对,就会出现问题.

为了对抗顺序,我们可以传对象的形式来传参.
 function normal (opition) {
            
            if(option.d){
              console.log(optioan.a - optian.b * opitoan.c);
            }
          }
          normal({a : 8,c: 9,b : 7,d : 16});
这样我们就不用太担心顺序,
不过缺点是,我们必须要把 a,b,c,d这些名字记清楚.
我们定义时,就要让a,b,c,d 更加语义化.

而且对象的形式,也更容易进行默认值的设置.
function normal (option1) {
            var option = {a : 1,b : 1,c : 1,d : true};
              for(var key in option1) {// 这一块可以用 类似深度克隆,$.extend等来代替.
                if(option1.hasOwnProperty(key)){
                  option[key] = option1[key];
                }
              }
            console.log(option.a,option.b,option.c,option.d);
          }
          normal({a : 8,c: 9,b : 7});


但extend 采取的传参形式依然是原来那种,
只不过在函数里面对参数进行了各种判断,
然后调用时就拥有了多种传参方式.
说起来简单,但我估计打破脑袋,目前阶段也很难写出来.
因为这里还涉及一个递归问题.

我们还是试着捋一遍思路.
extend的基本需求是,把不限数量的对象,赋值(深度克隆)到target对象.
所以应该有深度克隆,还要用到arguments.

然后要判断第一个参数是不是 布尔值,
还要判断是不是要把this当做 target.(调用时只传一个参数,就会把this当做target)

如果是我按照这个需求写的话,
可能会出现一堆嵌套if(){}else{}
我们回过头来看的时候,就会发现,
extend前面几个都只有 if没有else
也就是不会嵌套很多个if,else

这是怎么做到的?
设置数据有默认情况, 只需要考虑if?
不太懂.
```
怎样才能更少的嵌套if,else? 这个挺有用的,
网上搜了一下,虽然跟extend没啥太大关系,

避免if语句的深层次嵌套https://blog.csdn.net/qq_34986769/article/details/62041345
怎样避免“if”嵌套 https://blog.csdn.net/wssg3620625/article/details/37397581
第二篇感觉是大神,后面一堆都没怎么看懂.

```
我来找一下,接触过的隐藏的if,else
1.三木运算符:这个就不算是隐藏的.
var target = target > 3 ? target - 1 : target + 1;
2.逻辑运算符  && ||
var target = condition && b 相当于 if(condition) {target = b} 
多层if嵌套的时候可以用这个?
var target = condition || b 相当于 if(!condition){target = b}

3.函数 return
function stop (flag){
if(!flag){
return
}
//goto
相当于省略 else 而且 goto 不用写在if里面.
}
4.循环中的break,说是什么假循环.没怎么这么用过啊
while(flag){
if(flag){
  break;
}
break;
} 
goto()
5.对象(哈希?)
function switch (key) {
  var option = {
  name : 'mike',
  age : 18
}
return option[key]
}
对象的键值对形式,天然的就拥有if,switch
我觉得能用 这种形式代替if,switch 就尽量用.
无法实现范围条件的模拟.
```
