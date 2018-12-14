可以在组件里传html
可以用 name 来定位
可以有 默认值

```
<style type="text/css">
            .left,.right {
              display: inline-block;
              width: 100px;
              height: 100px;
              line-height: 100px;
              text-align: center;
            }
            .left {
              background-color: red;
            }
            .right {
              background-color: blue;
            }
        </style>
    </head>
    <body>
         <div id="app">
           <my-com>
             <div slot="right">right</div>
             <div slot="left">left</div>
             content
           </my-com>
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
          var myCom = {
            template : `<div>
                  <h3>myComponent</h3>
                  <div class="right">
                      <slot name="right">right slog</slot>
                  </div>
                  <div class="left">
                      <slot name="left">left slog</slot>
                  </div>
                  <div>
                       <slot>other slog</slot>
                  </div>
             </div>`
          }
          
          
            var app = new Vue({
              el : "#app",
              components : {
                myCom
              }
            })
        </script>
```

作用域插槽
```
<div id="app">
           <my-com :lists="lists">
             <li slot-scope="prop">{{prop.list2.title}}</li>
<!-- 这里可以理解为, <li>其实也是个组件.这样就好理解了, prop可以看成是这个组件的prop  -->
<!--这个地方会循环!-->
           </my-com>
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
          var myCom = {
            template : `<div>
                  <ul>
                    <slot v-for="list in lists" :list2="list"></slot>
                  </ul>
                  <div>123</div>
             </div>`,
             props : ["lists"]
          }
          
          
            var app = new Vue({
              el : "#app",
              components : {
                myCom
              },
              data : {
                lists : [
                  {title : "a"},
                  {title : "b"},
                  {title : "c"},
                  {title : "d"},
                  {title : "e"}
                ]
              }
            })
        </script>
```
你发现组件之间想要传递值, 都可以通过html结构中传递,
基本上 :son="father",son是子组件定义的,用来接收的,
father是父组件定义的,用来传值的.
插槽也看成是组件..
