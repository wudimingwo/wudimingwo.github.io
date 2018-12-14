用的基本都是
```
parentNode// 父元素,到头是 document
            childNodes// 子节点们 第一层,包含文本节点
            firstChild//第一个节点
            lastChild//最后一个节点
            nextSibling//下一个节点
            previousSibling//前一个节点.
```

模仿children
```
Element.prototype.myChildren = function () {
           	var dom = this;
           	var arr = [];
           	var myChildNodes = dom.childNodes;
           	var len = myChildNodes.length;
           	for(var i = 0 ; i < len; i++) {
           	  if(myChildNodes[i].nodeType === 1) {
           	    arr.push(myChildNodes[i]);
           	  }
           	}
           	return arr;
           }
```
模仿parentElement
```
Element.prototype.myParentElement = function () {
            var dom = this;
            var myParent = dom.parentNode;
            if(myParent.nodeType === 1 && myParent !== document) {
              return myParent
            }else {
              return null
            }
           }
```
获取所有dom元素的父级 返回数组
```
Element.prototype.allParent = function () {
           	var dom = this;
            var arr = [];
            function recurse (dom) {
              var myParent = dom.parentNode;
            	if(myParent && myParent.nodeType === 1 && myParent !== document) {
            	  arr.push(myParent);
            	  recurse(myParent);
            	}
            }
            recurse(dom);
            return arr;
           }
```
返回祖宗
```
Element.prototype.TopParent = function () {
            var dom = this;
            var top;
            function recurse (dom) {
              var myParent = dom.parentNode;
              if(myParent && myParent.nodeType === 1 && myParent !== document) {
                top = myParent;
                recurse(myParent);
              }
            }
            recurse(dom);
            return top;
           }
```
返回第一个子元素
```
Element.prototype.firstChildE = function () {
            var dom = this;
            var myChildNodes = dom.childNodes;
            var len = myChildNodes.length;
            for(var i = 0 ; i < len; i++) {
              if(myChildNodes[i].nodeType === 1) {
                return myChildNodes[i];
              }
            };
            return null;
           }
```
返回最后一个子元素
```
Element.prototype.lastChildE = function () {
            var dom = this;
            var myChildNodes = dom.childNodes;
            var len = myChildNodes.length;
            for(var i = len - 1 ; i >= 0; i--) {
              if(myChildNodes[i].nodeType === 1) {
                return myChildNodes[i];
              }
            };
            return null;
           }
```
返回后兄弟元素
```
Element.prototype.nextSibE = function () {
            var dom = this;
            var next = dom.nextSibling;
            while (next !== null){
              if(next.nodeType === 1){
                return next;
                break
              }
              next = next.nextSibling;
            }
            return null
           }
```
返回前兄弟元素
```
Element.prototype.previousSibE = function () {
            var dom = this;
            var pre = dom.previousSibling;
            while (pre !== null){
              if(pre.nodeType === 1){
                return pre;
                break
              }
              pre = pre.previousSibling;
            }
            return null
           }
```
返回后兄弟数组
```
Element.prototype.allNextSibE = function () {
            var dom = this;
            var arr = [];
            var next = dom.nextSibling;
            while (next !== null){
              if(next.nodeType === 1){
                arr.push(next);
              }
              next = next.nextSibling;
            }
            return arr
           }
```
返回前兄弟数组
```
Element.prototype.allPreSibE = function () {
            var dom = this;
            var arr = [];
            var pre = dom.previousSibling;
            while (pre !== null){
              if(pre.nodeType === 1){
                arr.push(pre);
              }
              pre = pre.previousSibling;
            }
            return arr
           }
```
遍历返回所有子元素,数据结构有点丑.
```
Element.prototype.allChild = function () {
           	var dom = this;
           	var arr = [];
           	function rucurse (dom,arr) {
           	    var arr = arr || [];
           		  var chi = dom.childNodes
           		  var len = chi.length;
           		  for(var i = 0;i < len;i++) {
           		    if(chi[i].nodeType === 1) {
           		      var obj = {
           		        ele : chi[i],
           		        children : []
           		      }
           		      arr.push(obj);
           		      rucurse(chi[i],obj.children);
           		      if(obj.children.length < 1){delete obj.children}
           		    }
           		  }
           		  return arr;
           	}
           	return rucurse(dom,arr);
           }
```


-----------------------------------------------
模拟 parent.insertAfter(a,b);
版本1.0
```
Element.prototype.insertAfter = function (a,b) {
            	this.insertBefore(b,a);
            }
这是有缺陷的
1. 我想剪切的是a,但实际上剪切的是b
2.创建的div,会报错.
```
版本2.0
```
          Element.prototype.insertAfter = function (a,b) {
              if(b.nextElementSibling) {
                this.insertBefore(a,b.nextElementSibling);
              }else {
                this.appendChild(a);
              }
            }
```
模拟 jq before
```
Element.prototype.before = function (a) {
                a.parentElement.insertBefore(this,a);
                return this;
            }
```
模拟 jq after
```
Element.prototype.after = function (a) {
              if(a.nextElementSibling) {
                a.parentElement.insertBefore(this,a.nextElementSibling);
              } else {
                a.parentElement.appendChild(this);
              }
                return this;
            }
```
模拟 jq append
```
Element.prototype.append = function (a) {
              this.appendChild(a);
              return this;
            }
```
模拟 jq appendTo
```
Element.prototype.appendTo = function (a) {
              a.appendChild(this);
              return this;
            }
```
模拟 jq prepend
```
Element.prototype.prepend = function (a) {
              if(this.firstElementChild) {
                this.insertBefore(a,this.firstElementChild);
              } else {
                this.appendChild(a)
              }
              return this;
            }
//说实话 像这种firstElementChild 应该用兼容性更好的, 
//但上面已经有这个的模拟了,在这里以及下面就都偷懒一下
```
模拟 jq prependTo
```
Element.prototype.prependTo = function (a) {
              if(a.firstElementChild) {
                a.insertBefore(this,a.firstElementChild);
              } else {
                a.appendChild(this);
              }
              return this;
            }
```
节点内的标签逆序(第一层子元素)
```
Element.prototype.reverseChild = function () {
              var childs = this.children;
              var len = childs.length;
              for(var i = 1;i < len; i++) {
                this.insertBefore(childs[i],childs[0]);
              }
            }
```