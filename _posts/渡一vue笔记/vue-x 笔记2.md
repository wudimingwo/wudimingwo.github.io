写的一手烂笔记之后发现
其实vuex 官网写得真的挺好的，
感觉相比其他官网，写得还算是人话。
[vuex](https://vuex.vuejs.org/zh/guide/state.html)官网

除了引用 store.js
用 $store.state 和 $store.commit()
这两种以外

还可以有另外一种引用方式.
可读性更好一点

先记下来...
```
import vue from "vue";
import Vuex from "vuex";

vue.use(Vuex);

export default new Vuex.Store({
  state : {
    info : "欢迎来到课堂"
  },
  mutations : {
    changeInfo (state) {
      state.info = "welcome to class"
    }
  }
});

```
App.vue
```
<template>
  <div id="app">
    <div class="wrapper">
      <div>{{myInfo}}</div>
    </div>
    <button @click="change">change</button>
  </div>
</template>

<script>
  
  import {mapState,mapMutations} from "vuex"
  
    export default {
      name : "App",
      computed : {
        ...mapState({
          myInfo : state => state.info
        })
      },
      methods : {
        ...mapMutations({
          change : 'changeInfo'
        })
      }
    }
</script>

<style>
  
</style>

```