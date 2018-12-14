![image.png](https://upload-images.jianshu.io/upload_images/13637909-96084d654b542e3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
组件化和模块化 百度搜索出来的
[组件化开发和模块化开发概念辨析](https://blog.csdn.net/blog_jihq/article/details/79191008)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-19dba801929ab9a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
说明
组件：最初的目的是代码重用，功能相对单一或者独立。在整个系统的代码层次上位于最底层，被其他代码所依赖，所以说组件化是纵向分层。
模块：最初的目的是将同一类型的代码整合在一起，所以模块的功能相对复杂，但都同属于一个业务。不同模块之间也会存在依赖关系，但大部分都是业务性的互相跳转，从地位上来说它们都是平级的。
--------------------- 
作者：奇风 
来源：CSDN 
原文：https://blog.csdn.net/blog_jihq/article/details/79191008 


```

<div id="app">
           <my-com></my-com>// 注意这里不是大驼峰
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            
            //全局组件
            Vue.component("myCom",{
              template : "<div>hello</div>"
            });
            //局部组件
            var myCom = {
              template : "<div>hello12</div>"
            }
          
            var app = new Vue({
              el : "#app",
              components : {
                myCom
              }
            });
            
        </script>
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-87ee3e3e97a610dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

data 与 根实例不同
目的,组件复用时, 变量不会共享, 每个被使用的组件,都拥有独自的data
```
var myCom = {
              template : "<div>hello12</div>",
              data () {
                show : "hello world"
              }
            }


```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-c8a26b7b54c024f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

计算属性
想改变computed 里的值 就需要 改变data里的值
要么直接改data, 要么 给 computed定义时留出set,
在set里改data里的值.
```
<div id="app">
           <my-com></my-com><!--// 注意这里不是大驼峰-->
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            
            var myCom = {
              template : `<div>
              <div>{{show}}</div>
              <div>{{myShow}}</div>
              <button @click="change">changeMyShow</button>
              </div>`,
              data () {
                return {
                    show : "hello world"
                  }
              },
              computed : {
                myShow : {
                  get () {
                    return this.show + "    sasdfasdfasdf"
                  },
                  set (newVal) {
                    this.show = newVal
                  }
                }
              },
              methods : {
                change () {
                  this.myShow = "im not good" 
                }
              }
            }
          
            var app = new Vue({
              el : "#app",
              components : {
                myCom
              }
            });
            
           
            
            
        </script>
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-d5c88ae2aba9bab5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
父子组件通信 基本就靠这个了.
子 通过prop 获取 父 里的 数据
原则:单向传递

传原始值时, 子组件里修改prop 不会影响 父级里的数据
传引用值时, 会影响父级里的数据, 数据流向会混乱, 需要注意
```
尽量不要直接修改props传进来的值.
先放进data里,可读可写.
<div id="app">
           <my-com :son="father"></my-com><!--// 注意这里不是大驼峰-->
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            
            var myCom = {
              template : `<div>
              <div>{{mySon}}</div>
              <button @click="change">change</button>
              </div>`,
              props : ["son"],
              data () {
                return {
                    mySon : this.son
                  }
              },
              methods : {
                change () {
                  this.mySon = "peter"
                }
              }
            }
          
            var app = new Vue({
              el : "#app",
              data : {
                father : 'mike'
              },
              components : {
                myCom
              }
            });
```
父级如果想从子组件中获取数据,
            首先,要在父级当中定义方法,可接受参数
            第二,在子组件标签结构上定义事件
            第三,在子组件中 用this.$emit(type,some) 触发事件,传递参数,传数据给父级.
```
<div id="app">
           <div>father is {{father}}</div>
           <my-com :son="father" @tailme="changeVal"></my-com>
           
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            var myCom = {
              template : `<div>
             <div>{{mySon}}</div>
             <input type="text" v-model="mySon"/>
           </div>`,
           props : ["son"],
              data () {
                return {
                  mySon : this.son
                }
              },
              methods : {
                changeSon () {
                  this.mySon = 'mike'
                }
              },
              watch : {
                mySon () {
                  this.$emit('tailme',this.mySon)
                }
              }
            }
          
            var app = new Vue({
              el : "#app",
              components : {
                myCom
              },
              data : {
                father : "peter"
              },
              methods : {
                changeVal (val) {
                  this.father = val;
                }
              }
            })

```
上面的例子,也告诉我们,可以用 this.$emit方法,触发父级给的事件?d

表单验证组件案例
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>dddd</title>
        <style type="text/css">
            
        </style>
    </head>
    <body>
      <div id="app">
        <my-com v-bind="giveSon">
          <!--<div>
            <span>请输入邮箱</span>
            <input type="text" />
            <span>错误信息</span>
          </div>-->
        </my-com>
      </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            
            var myCom = {
              template : `<div>
            <span>{{title}}</span>
            <input v-model="val" type="text" />
            <span>{{msg}}</span>
          </div>`,
              data () {
                return {
                  val : ''
                }
              },
              props : {
                title : {
                  type : String,
                  default : "请输入"
                },
                sucmsg : {
                  type : String,
                  default : "正确"
                },
                errmsg : {
                  type : String,
                  default : "错误"
                },
                rexexp : {
                  type : RegExp,
                }
              },
              computed : {
                msg () {
                  if (this.val == "") {
                  	return ""
                  }
                  return this.rexexp.test(this.val) ? this.sucmsg : this.errmsg;
                }
              }
              
            }
            
            var app = new Vue({
              el : "#app",
              components : {
                myCom
              },
              data : {
                giveSon : {
                  title : "请输入QQ邮箱",
                  sucmsg : "格式正确",
                  errmsg : "格式错误",
                  rexexp : /@qq.com$/
                }
              }
            })
        </script>
    </body>
</html>

```
确实vue编码感觉更轻松,
            先写html,在考虑数据,考虑数据源,考虑事件,基本上,看着html结构,就能把思路捋顺,
不需要考虑,dom元素,
            更重要的是,不需要考虑怎么去组织数据,基本不用考虑什么太深的设计模式.
而且能够定义高复用的组件,完成大型项目,,
vue真的是厉害...