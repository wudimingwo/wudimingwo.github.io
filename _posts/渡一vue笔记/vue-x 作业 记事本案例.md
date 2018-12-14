[模仿的是这个](https://coligo-io.github.io/notes-app-vuejs-vuex/#)

确实放在github上可能更好，
不过我得用手机端多看两遍，
还是先放这里吧

用的是vue-cli
构建 webpack

App.vue
```
<template>
  <div class="wrapper">
    <left></left>
    <middle></middle>
    <right></right>
  </div>
</template>

<script>
  
  import store from "./components/store.js"
  import Left from "./components/Left.vue"
  import Middle from "./components/Middle.vue"
  import Right from "./components/Right.vue"
 
  
    export default {
      store,
      name : "App",
      components : {
        Left,
        Middle,
        Right
      }
    }
</script>

<style>
    *{
      margin: 0;
      padding: 0;
    }
  .wrapper{
    display: flex;
    width: 100vw;
    height: 100vh;
  }
</style>

```
Left.vue
```
<template>
  <div class="wrapperl">
    <div class="add" @click="add">+</div>
    <div class="favor" :class="{orange : flag}" @click="favor">★</div>
    <div class="delete" @click="del">×</div>
  </div>
</template>

<script>
  
  
    export default {
      name : "Left",
      computed : {
        id () {
         return this.$store.state.id
        },
        flag () {
         return this.$store.state.listItem.find(item => item.id == this.id).fav
        }
        
      },
      methods : {
        add () {
          this.$store.commit('add')
        },
        favor () {
          this.$store.commit('favor')
        },
        del () {
          this.$store.commit('del')
        }
      }
      
    }
</script>

<style scoped="scoped">
  .wrapperl{
    width: 90px;
    box-sizing: border-box;
    background : rgb(48,65,77);
  }
  .wrapperl div{
    width: 100%;
    height: 90px;
    line-height: 90px;
    text-align: center;
    font-size: 30px;
    font-weight: bold;
    color : rgb(102,106,109);
    cursor: pointer;
    transform: scale(1.5);
  }
  .wrapperl div.orange.favor{
    color: orange;
  }
  .wrapperl div:nth-of-type(2) {
    transform: scale(1.3);
  }
  .wrapperl div:hover{
    color: rgb(150,150,150);
  }
  
</style>

```
Middle.vue
```
<template>
  <div class="wrapperm">
    <div class="title">NOTES | COLIGO</div>
    <div class="btn">
      <div class="allbtn" :class="{alive : flag == true}" @click="changetrue">All Notes</div>
      <div class="Favorbtn" :class="{alive : flag == false}" @click="changefalse">Favorites</div>
    </div>
    <div class="listItem">
      <template  v-if="flag == true">
        <div v-for="item in listItem" class="listItem-item"  :class="{active : item.id == id}" @click="pick(item)">{{item.textTitle}}</div>
      </template>
      <template  v-else>
        <div v-for="item in listFav" class="listItem-item"  :class="{active : item.id == id}" @click="pick(item)">{{item.textTitle}}</div>
      </template>
    </div>
  </div>
</template>

<script>
  
    export default {
      name : "Middle",
      computed : {
        listItem () {
          return this.$store.state.listItem;
        },
        id () {
          return this.$store.state.id;
        },
        listFav () {
          return this.$store.state.listItem.filter(item => item.fav == true)
        },
        flag () {
          return this.$store.state.toggle.flag
        }
      },
      methods : {
        pick (item) {// 更改 id
          this.$store.commit('pick',item);
        },
        changetrue () {
          this.$store.commit('changelist',true);
        },
        changefalse () {
          this.$store.commit('changelist',false);
          console.log(this.listFav);
        }
      },
    }
</script>

<style>
  .wrapperm{
    width: 300px;
    box-sizing: border-box;
    background-color: rgb(245,245,245);
  }
  .wrapperm .title{
    height: 90px;
    text-align: center;
    line-height: 90px;
    font-size: 25px;
    color: rgb(80,80,80);
  }
  .wrapperm .btn{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding-bottom: 30px;
  }
  .wrapperm .btn div{
    width: 40%;
    border: 1px solid #ccc;
    text-align: center;
    height: 30px;
    line-height: 30px;
    color: #555;
    border-radius: 5px;
    background-color: white;
    cursor: pointer;
    user-select:none;
  }
  .wrapperm .btn div:hover{
    background-color: #bbb;
  }
  .wrapperm .btn .alive{
    background-color: #ccc;
    
  }
  .wrapperm .listItem{
    width: 100%;
  }
  .wrapperm .listItem-item{
    width: 100%;
    height: 40px;
    padding-left: 10px;
    line-height: 40px;
    background-color: white;
    cursor: pointer;
  }
  .wrapperm .active{
    background-color: rgb(51,122,183);
    color: white;
  }
  
</style>

```
Right.vue
```
<template>
  <div class="wrapperr">
    <textarea class="text-title" @input="changeTitle($event)" :value="title" >{{title}} </textarea>
    <textarea class="text-area" @input="changeText($event)" :value="textArea" >{{textArea}} </textarea>
    
  </div>
</template>

<script>
     import { mapState } from "vuex";
    export default {
      name : "Right",
      computed : {
        ...mapState({
          id : state => state.id,
          title : function (state) {
           return state.listItem.find(item => item.id == this.id).textTitle
          },
          textArea : function (state) {
           return state.listItem.find(item => item.id == this.id).textArea
          },
        })
      },
      methods : {
        changeTitle (e) {
          this.$store.commit('changeTitle',e.target.value)
        },
        changeText (e) {
          this.$store.commit('changeText',e.target.value)
        }
      }
      
    }
</script>

<style>
  .wrapperr{
    flex-grow: 1;
  }
  .wrapper input, .wrapper textarea{
    display: block;
    width: 100%;
    outline: none;
    border: none;
    box-sizing: border-box;
  }
  .wrapperr .text-title{
    height: 40px;
    line-height: 40px;
    padding-left: 20px;
    font-size: 22px;
    font-weight: bold;
    color: orange;
    background-color: #555;
  }
  .wrapperr .text-area{
    font-size: 20px;
    line-height: 30px;
    text-indent: 1em;
    padding-left: 20px;
    color: #424242;
    height: calc(100vh - 600px);
  }
  
</style>

```
store.js
```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex);

const LBS = (function () {
	return {
	  setItem (type,val) {
	    window.localStorage.setItem('type',JSON.stringify(val));
	  },
	  getItem (type) {
	    return JSON.parse(window.localStorage.setItem('type'));
	  },
	  removeItem (type) {
	    window.localStorage.removeItem(type)
	  }
	  
	}
})();

export default new Vuex.Store({
  
  state : {
    count : 0,// 用来生成唯一 id
    listItem : [{
      id : 0,
      textTitle : "new note",
      textArea : "something",
      fav : false
    }],
    id : 0,
    toggle : {
      flag : true
    }
  },
  mutations : {
    add (state) {
      state.count++;
      var item = {
        id : state.count,
        textTitle : state.count,
        textArea : "something"
      }
      state.listItem.push(item);
      state.id = item.id;
    },
    favor (state) {// 不需要更新id
      Vue.set(state.listItem.find(item => item.id == state.id),'fav',!state.listItem.find(item => item.id == state.id).fav);
    },
    del (state) {// 要根据id 从列表中删除，相应的数据， 并且更新id 为最后一个数据的id
      state.listItem = state.listItem.filter(item => item.id != state.id);
      var len = state.listItem.length;
      if (len) {
        state.id = state.listItem[state.listItem.length - 1].id;
      }
    },
    pick (state, item) {
      state.id = item.id;
    },
    changelist (state,flag) {// 切换列表， 更新 id
      state.toggle.flag = flag;
      console.log(state.listItem[0].fav);
    },
    changeText (state,tex) {
      var item = state.listItem.find(item => item.id == state.id);
      Vue.set(item,'textArea',tex);
    },
    changeTitle (state,tex) {
      var item = state.listItem.find(item => item.id == state.id);
      Vue.set(item,'textTitle',tex);
    }
  }
  
  
  
});

```
感觉 用这个id 为核心， 搞得整个代码很臃肿。
不过好歹，也算是建立了用vue的基本意识。

其实我很想知道，有没有办法用localStorage 把数据储存起来，
因为一刷新就没了。