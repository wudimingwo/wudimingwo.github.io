```
<style type="text/css">
            
            .com-leave, .com-enter-to{
              transform: translateX(0);
            }
            .com-leave-to,.com-enter{
              transform: translateX(-150%);
            }
            .com-leave-active,.com-enter-active{
              transition: transform 0.8s ease;
            }
            
        </style>
    </head>
    <body>
         <div id="app">
           <transition mode="out-in" name="com">
             <keep-alive>
               <component :is="whichCom"></component>
             </keep-alive>
           </transition>
           
           <button @click="whichCom = (whichCom == 'user-name') ? 'pass-word' : 'user-name';">username</button>
           
           
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
              const userName = {
                template : `<div>username : <input type="text" /></div>`
              }
              const passWord = {
                template : `<div>password : <input type="password" /></div>`
              }
          
            var app = new Vue({
              el : "#app",
              components : {
                userName,
                passWord
              },
              data : {
                whichCom : "user-name"
              }
            })
        </script>
    </body>
```