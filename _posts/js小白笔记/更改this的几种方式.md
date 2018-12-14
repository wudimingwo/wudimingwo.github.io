```
function print () {
      	var marty = {
      	  name : 'marty',
      	  printName:function(){console.log(this.name);}
      	}
      	var test1 = {name:'test1'};
      	var test2 = {name:'test2'};
      	var test3 = {name: 'test3'};
      	test3.printName = marty.printName;
      	var printName2 = marty.printName.bind({name:123});
      	marty.printName.call(test1); //test1
      	marty.printName.apply(test2);//test2
      	marty.printName();//marty
      	printName2();//123
      	test2.printName2 = printName2;
      	test2.printName2();//123
      	test3.printName();//test3;
        
      }
      print();

这道题包含了常用的.
1.fun()  this默认指向window
2.obj.fun() this指向obj
3.obj.fun.call(obj1) this指向obj1
4.obj.fun.apply(obj1) this指向obj1
5.var fun1 = fun.bind(obj)  返回一个函数 , 绑定this, 固定指向obj.  2,3,4方法都失效
      如果执行时硬要改,有个笨方法  fun1.bind(obj1)(); 用bind再绑定一次
      new 的时候,this会指向实例,绑定失效.

6.还有一个new fun(); this 指向一个生成的实例对象.
```
---------------------------
上面有地方写错了.
通过bind绑定的this , 再次使用bind 也无法改变.
[js小白模拟系列:模拟bind](https://www.jianshu.com/p/eba8f966bfbb)
通过模拟可以看出, bind通过嵌套一层函数来固定原来函数的this指向,
嵌套的函数的this指向怎么改变都无法影响 this指向, 除了new
