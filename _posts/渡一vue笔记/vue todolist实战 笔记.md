v-bind:class
```
<style type="text/css">
            .red {
              color: red;
            }
            .blue {
              color: blue;
            }
            .green{
              color: green;
            }
        </style>
    </head>
    <body>
         <div id="app">
           <div :class="show">{{msg}}</div>
           <button @click="show='red'">red</button>
           <button @click="show='blue'">blue</button>
           <button @click="show='green'">green</button>
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            var app = new Vue({
              el : "#app",
              data : {
                show : "red",
                msg : "hello everyone"
              }
            })
        </script>
```
{}语法
```
           <div :class="{'red':true,'size-18':true,'weight-800':true}">hello everyone</div>
```
```
 <div :class="styles">hello everyone</div>
....
data : {
  styles : {'red':true,'size-18':true,'weight-800':true}
}
```

[]语法
```
           <div :class="[color,size,weight]">hello everyone</div>

            data : {
                color : 'red',
                size : "size-18",
                weight : "weight-800"
              }
```
v-bind:styles
```
           <div :style="styles">hello everyone</div>
...

              data : {
                styles : {color : "red", fontSize : "18", fontWeight:"800"}
              }
```
```
           <div :style="[styles,{backgroundColor:'blue'}]">hello everyone</div>
....
              data : {
                styles : {color : "red", fontSize : "18", fontWeight:"800"}
              }
```
v-bind 控制更改其他属性值
```
<div id="app">
           
           <input :type="type" :readonly="flag" :checked="swich">hello everyone</input>
           <button @click="type='radio'">radial</button>
           <button @click="type='checkbox'">checkbox</button>
           <button @click="type='text'">text</button>
           <button @click="flag=true">只读</button>
           <button @click="flag=false">可写</button>
           <button @click="swich=true">选择</button>
           <button @click="swich=false">不选</button>
         </div>


var app = new Vue({
              el : "#app",
              
              data : {
                type : "text",
                flag : true,
                swich : true
              }
            })
```

v-if
```
         <div id="app">
           <div v-if="num%2==0">one</div>
           <div v-else-if="num==3">two</div>
           <div v-else="">three</div>
         </div>
...
var app = new Vue({
              el : "#app",
              data : {
                num : 0
              }
            })
```
v-show
与v-if不同,这相当于display: none,只是 css层面的,动作小,消耗小.
```
           <div v-show="false">123</div>
不存在else
```
v-for
数组时
```
           <li v-for="item in listArr">{{item}}</li>
            哪里放了v-for 哪个标签就会重复构建.
...
            var app = new Vue({
              el : "#app",
              data : {
                listArr : [1,2,3,4,5]
              }
            })
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-17d56906656376bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
           <li v-for="(item,index) in listArr">{{index}}:{{item}}</li>
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-3762eca4ba637d13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
对象时
```
           <li v-for="value in listArr">{{value}}</li>
...
var app = new Vue({
              el : "#app",
              data : {
                listArr : {
                  name : 'mike',
                  age : 18,
                  sex : 'male'
                }
              }
            })
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-a6c5e733c5f4ee9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
           <li v-for="value,key in listArr">{{key}}:{{value}}</li>
...var app = new Vue({
              el : "#app",
              data : {
                listArr : {
                  name : 'mike',
                  age : 18,
                  sex : 'male'
                }
              }
            })
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-1b707547dfc6b996.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在vue修改引用值,(数组,和对象),
为了让数据绑定保证生效,
需要用专门的api进行修改

数组时
![image.png](https://upload-images.jianshu.io/upload_images/13637909-2038802c3920ff5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-eacb0341a7e794e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

还有这些
![image.png](https://upload-images.jianshu.io/upload_images/13637909-9a3830e9d1fa8437.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


对象时
![image.png](https://upload-images.jianshu.io/upload_images/13637909-e730011439f4a5da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/13637909-f2a72d9eaab1ab76.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

todolist 丁老师.
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>dddd</title>
        <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
        <style type="text/css">
            .isFinished{
              color: orange;
            }
        </style>
    </head>
    <body>
         <div id="app" class="container">
             <div class="row">
               <div class="col-md-7">
                 <div class="form-group">
                   <label for="">添加工作事项</label>
                   <input type="text" class="form-control" v-model="val" @keyup.enter="addItem"/>
                 </div>
                 <div class="item-group">
                   <a href="#" class="list-group-item">
                     工作清单
                   </a>
                   <a href="#" class="list-group-item" v-for="item,index in listItem">
                     <span>{{index + 1}}</span>
                     <span>{{item.title}}</span>
                     <span class="badge" @click="removeItem(index)">
                       <i class="glyphicon glyphicon-remove"></i>
                     </span>
                     <span class="badge" @click="toggleFinished(item)">
                       <i class="glyphicon glyphicon-ok" :class="{isFinished : item.isFinished}"></i>
                     </span>
                     
                   </a>
                 </div>
               </div>
               
             </div>
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            var LBS = (function () {
            	return {
            	  addItem (type,value) {
            	    window.localStorage.setItem(type,JSON.stringify(value));
            	  },
            	  getItem (type) {
            	   return JSON.parse(window.localStorage.getItem(type));
            	  },
            	  removeItem (type) {
            	    window.localStorage.removeItem(type);
            	  }
            	}
            })();
          
          
            var app = new Vue({
              el : "#app",
              data : {
                val : "",
                listItem : LBS.getItem('todolist') || []
              },
              methods : {
                addItem () {
                  var newItem = {
                    id : this.listItem.length + 1,
                    title : this.val,
                    isFinished : false
                  }
                  this.listItem.push(newItem);
                  LBS.addItem(this.listItem);
                  this.val = ""
                },
                toggleFinished (item) {// 這裡不能通過 this來獲得,因為數據沒有定义在data上,但我们可以传.
                  item.isFinished = !item.isFinished;
                  LBS.addItem('todolist',this.listItem);
                },
                removeItem (index) {
                  this.listItem.splice(index,1);
                  LBS.addItem('todolist',this.listItem);
                }
              }
            })
        </script>
    </body>
</html>

```
这里曾经有过疑问,
```
item.isFinished = !item.isFinished;
```
这里我刚开始觉得不应该会引起渲染刷新,因为是引用值的改变.
后来我发现设置成
```
item.isFinished.isFinished = !item.isFinished.isFinised
```
还是会引起渲染刷新

我觉得只要
```
:class="isFinshed : item.isFinshed.isFinished"
```
可能就会被注册? 也许应该看源码?

稍微变形
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>dddd</title>
        <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
        <style type="text/css">
            .finished {
              color: orange;
            }
        </style>
    </head>
    <body>
         <div id="app" class="container">
           
           <div class="row">
             <div class="col-md-7">
                <div class="form-group input-group">
                  <label for="todo" class="input-group-addon">添加待办事项</label>
                  <input type="text" class="form-control" name="todo" id="todo" @keyup.enter="addItem" v-model="val" />
                </div>
                
                <div>
                  <span class="list-group-item">工作清单</span>
                  <span class="list-group-item" v-for="item,index in listItem">
                    <span>{{index + 1}}</span>
                    <span>{{item.title}}</span>
                    
                    <span class="badge" @click="removeItem(index)">
                      <i class="glyphicon glyphicon-remove"></i>
                    </span>
                    <span class="badge" @click="toggleFinished(item,index)">
                      <i class="glyphicon glyphicon-ok" :class="{finished : item.isFinished.isFinished}"></i>
                    </span>
                  </span>
                  
                  <div v-show="this.compoletArr.length">
                    <span class="list-group-item">已完成列表</span>
                    <span class="list-group-item" v-for="item,index in compoletArr">
                    <span>{{index + 1}}</span>
                    <span>{{item.title}}</span>
                    
                    <span class="badge" @click="removeItem(index)">
                      <i class="glyphicon glyphicon-remove"></i>
                    </span>
                    <span class="badge" @click="toggleFinished(item,index)">
                      <i class="glyphicon glyphicon-ok" :class="{finished : item.isFinished.isFinished}"></i>
                    </span>
                  </span>
                  </div>
                </div>
             </div>
           </div>
           
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            const LBS = (function () {
            	return {
            	  addItem (type,value) {
            	    window.localStorage.setItem(type,JSON.stringify(value));
            	  },
            	  getItem (type) {
            	    return JSON.parse(window.localStorage.getItem(type));
            	  },
            	  removeItem (type) {
            	    window.localStorage.removeItem(type);
            	  }
            	}
            })();
          
          
            var app = new Vue({
              el : "#app",
              data : {
                listItem : LBS.getItem('list') || [],
                compoletArr : LBS.getItem('completed') || [],
                val : ""
              },
              methods : {
                addItem () {
                  var item = {
                    id : this.listItem.length + 1,
                    title : this.val,
                    isFinished : {
                      isFinished : false
                    }
                  }
                  this.listItem.push(item);
                  LBS.addItem('list',this.listItem);
                  this.val = "";
                },
                toggleFinished (item,index) {
                  item.isFinished.isFinished = !item.isFinished.isFinished;// 理论上讲,这里应该不会触发数据刷新吧? 因为item 是 用 for进行注册的? 所以会刷新?
                  if (item.isFinished.isFinished) {
                    this.listItem.splice(index,1);
                    this.compoletArr.push(item);
                  } else{
                  	this.compoletArr.splice(index,1);
                    this.listItem.push(item);
                  }
                  LBS.addItem('list',this.listItem);
                  LBS.addItem('completed',this.compoletArr);
                },
                removeItem (index) {
                  this.listItem.splice(index,1);
                  LBS.addItem('list',this.listItem);
                }
              }
            })
        </script>
    </body>
</html>

```
然后就发现,两个列表结构非常相似,
有必要抽象成组件?
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewprot" content="width=device-width, initial-scale=1.0"/>
        <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
        <title>dddd</title>
        <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
        <style type="text/css">
            .finished {
              color: orange;
            }
        </style>
    </head>
    <body>
         <div id="app" class="container">
           
           <div class="row">
             <div class="col-md-7">
                <div class="form-group input-group">
                  <label for="todo" class="input-group-addon">添加待办事项</label>
                  <input type="text" class="form-control" name="todo" id="todo" @keyup.enter="addItem" v-model="val" />
                </div>
                
                <my-com :listarr="listitem" :headtitle="'工作清单'"    @taileme="update"></my-com>
                <my-com :listarr="compoletarr" :headtitle="'完成清单'"   @taileme="update"></my-com>
                
             </div>
           </div>
           
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
            const LBS = (function () {
            	return {
            	  addItem (type,value) {
            	    window.localStorage.setItem(type,JSON.stringify(value));
            	  },
            	  getItem (type) {
            	    return JSON.parse(window.localStorage.getItem(type));
            	  },
            	  removeItem (type) {
            	    window.localStorage.removeItem(type);
            	  }
            	}
            })();
            
            const myCom = {
              template : `</div>
                  <div v-show="listArr1.length">
                    <span class="list-group-item">{{headtitle}}</span>
                    <span class="list-group-item" v-for="item,index in listArr1">
                    <span>{{index + 1}}</span>
                    <span>{{item.title}}</span>
                    
                    <span class="badge" @click="removeItem(index)">
                      <i class="glyphicon glyphicon-remove"></i>
                    </span>
                    <span class="badge" @click="toggleFinished(item,index)">
                      <i class="glyphicon glyphicon-ok" :class="{finished : item.isFinished.isFinished}"></i>
                    </span>
                  </span>
                  </div>
             </div>`,
             props : {
               listarr : {
                 type : Array,
                 required : true
               },
               headtitle : {
                 type : String,
                 default : "工作清单"
               }
             },
             data () {
               return {
                 listArr1 : this.listarr// 但这是引用值,不知道有没有效果.
               }
             },
             methods : {
               // 我需要在子组件中修改数据, 同步到父级数据中.怎么办? 还是要用tailme?
               removeItem(index) {
                 this.listArr1.splice(index,1);
                 // 把数组传递给父级
                 this.$emit("taileme",this.listArr1,this.headtitle);
               },
               toggleFinished (item,index) {
                 item.isFinished.isFinished = !item.isFinished.isFinished;// 理论上讲,这里应该不会触发数据刷新吧? 因为item 是 用 for进行注册的? 所以会刷新?
                    this.listArr1.splice(index,1);
                    this.$emit("taileme",this.listArr1,this.headtitle,item);
                 }
             }
             }
          
          
          
          
            var app = new Vue({
              el : "#app",
              data : {
                listitem : LBS.getItem('list') || [],
                compoletarr : LBS.getItem('completed') || [],
                val : ""
              },
              methods : {
                addItem () {
                  var item = {
                    id : this.listitem.length + 1,
                    title : this.val,
                    isFinished : {
                      isFinished : false
                    }
                  }
                  this.listitem.push(item);
                  LBS.addItem('list',this.listitem);
                  this.val = "";
                },
                update (arr,type,item) {
                  if (type == "工作清单") {
                  	this.listitem = arr;
                  	item && this.compoletarr.push(item);
                  }else if (type == "完成清单") {
                  	this.compoletarr = arr;
                  	item && this.listitem.push(item);
                  }
                  console.log(123);
                  LBS.addItem('list',this.listitem);
                  LBS.addItem('completed',this.compoletarr);
                }
              },
              components : {
               myCom
             }
            })
        </script>
    </body>
</html>

```
总是要到了自己试着改进一下的时候,
才会觉得还是差很多,
写得时候,思路混乱,
写完感觉代码很丑,
不过好歹写了一下,真的是,思路弄清楚是最重要的.