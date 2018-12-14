```
<div id="app">
           <keep-alive>
             <component :is="whichCom"></component>
           </keep-alive>
           
           <button @click="whichCom = 'user-name'">username</button>
           <button @click="whichCom = 'pass-word'">password</button>
           
           
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
```