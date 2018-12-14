```
<div id="app">
           <input type="text" v-focus:abc.first.last="val"  v-model="val"/>
           <div>{{val}}</div>
         </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
        <script type="text/javascript">
              Vue.directive('focus',{
                bind (el,binding,vnode,oldVnode) {
                  console.log(el,binding,vnode,oldVnode);
                  console.log("bind");
                },
                inserted(el,binding,vnode,oldVnode) {
                  console.log(el,binding,vnode,oldVnode);
                  console.log("inserted");
                  el.focus();
                },
                update (el,binding,vnode,oldVnode) {
                  console.log(el,binding,vnode,oldVnode);
                  console.log("update");
                  
                },
                componentUpdated (el,binding,vnode,oldVnode) {
                  console.log(el,binding,vnode,oldVnode);
                  console.log("componentUpdated");
                  
                },
                unbind (el,binding,vnode,oldVnode) {
                  console.log(el,binding,vnode,oldVnode);
                  console.log("unbind");
                  
                }
              })
          
            var app = new Vue({
              el : "#app",
              data : {
                val : "a"
              }
            })
```

![image.png](https://upload-images.jianshu.io/upload_images/13637909-95cf27c8cd36d8e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
