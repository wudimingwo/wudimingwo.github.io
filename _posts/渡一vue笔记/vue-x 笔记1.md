名字不重要,
为什么要用这个? 解决什么问题?
他是怎么解决这个问题的? 什么设计? 什么思想?

为什么用vue-x?
怎么用vue-x?

当我们碰到一个新的工具或框架时,

首先我们要知道这是干什么,解决了什么问题
第二我们要知道怎么用这个工具,
第三,我们要知道这个工具具体都干了什么
第四,我们要知道这个工具出于什么思想,以什么样的方式解决了问题.

回到正题

vue组件是个树形结构
![image.png](https://upload-images.jianshu.io/upload_images/13637909-d26d088a1686f925.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
现在我想实现 BB 和 CC之间的传递 要怎么做?

父子间组件可以用 props 和自定义事件, 可以传递信息,
所以BB和CC需要找到公共父组件,逐级上传,逐级下传.


所以vue-x 是用来解决组件之间的通信的?

具体步骤

1.安装依赖包
```
$ cnpm install vuex --save
```
2. 引入
```
import Vuex from "vuex"
```
3.激活? 注册? 所有vue插件都需要这个,router也是
```
Vue.use(Vuex);
```
4.配置项
```
// 我们发现 只需要在根实例上, 引入store,
// 所依赖的所有组件都会自动添加 $store属性
// 所有组件都共享的一个数据空间?
export default new Vuex.Store({
  state : {// 类似组件中的 date?
    msg : "我是state"
  },
// 这里是主要储存数据的地方
// $store.state.msg 或者 this.$store.state.msg 可以在任何组件获取数据.
  mutations : {// 定义方法 ,类似methods?
    //payload
    setVal (state,val) {
      state.val = val;
// 定义的时候,state必须要留出来, 这里不像组件可以用this.state.
    }
// 这里跟methods稍微不同,主要是针对修改 state 中的数据的.
// 换言之,在各个组件中, 不可以用$store.state.msg = "sga"的方式修改数据
// 不过不知道, v-model="$store.state.msg ",这种双向绑定能不能更改,
//视频课上说不行, 我自己试的时候似乎是可以的.
//$store.commit("setVal","everyone");
// 这里要注意,setVal 是 选择要调用 哪个函数
// "everyone" 对应的是 val,
// state 实际上是不用传的, 默认传的.
  }
})
```
vuex 和 普通组件其实还是比较相似的.
但老实说这不是组件,
确实跟组件不同,这里没有html,没有样式,
主要就是用来存放数据的.
然后留出各个接口让各个组件可以
改查

主要的用处就是,非父子之间的数据共享?数据通信?

联想设计模式课里陈老师说的,
如果这不算是个模块,组件,而就是个数据块,
组件跟这个数据块产生的联系不算是增加耦合度,
那么这应该就是依赖倒置原则的应用体现了吧?

看到网上说, vue-x 主要是状态的共享,,
我们看字段, 也是 state
是不是可以理解为,
跟组件本身相关的数据,最好还是放在组件内部的data里
或者组件跟组件的依赖,最好是限于一些状态?

状态这种数据概念,理解程度似乎不够啊.


```

```

