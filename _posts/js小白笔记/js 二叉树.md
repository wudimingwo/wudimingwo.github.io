百度搜索 二叉树
头两个链接就是这俩
# [JavaScript二叉树深入理解](https://www.jianshu.com/p/61f75e0f549f)


# [javascript实现数据结构： 树和二叉树,二叉树的遍历和基本操作](https://www.cnblogs.com/webFrontDev/p/3865719.html)

第二个博客的内容应该算第一个博客的基础知识.
第一个比较好懂,第二个比较难,代码量也多.
```
function Node (data,left,right) {
      	this.data = data;
      	this.left = left;
      	this.right = right;
      }
      function BST () {
      	this.root = null;
      	this.insert = insert;
      	this.find = find;
      	this.remove = remove;
      }
      
      function insert (data) {
      	var node = new Node(data,null,null);
      	if(this.root == null) {
      	  this.root = node;
      	} else {
      	  var current = this.root;
      	  while(true) {
      	    if(current.data > data) {
      	      if(current.left === null) {
      	        current.left = node;
      	        break;
      	      }
      	      current = current.left;
      	    }else {
      	      if(current.right === null) {
      	        current.right = node;
      	        break;
      	      }
      	      current = current.right;
      	    }
      	  }
      	}
      }
      
      
      //二叉树查节点
      function find (data) {
      	var current = this.root;
      	while (true){
      		if(data == current.data) {
      		  return current;
      		}
      		current = data < current.data ? current.left : current.right;
      		if(current === null) {
      		  return null;
      		}
      	}
      }
      
      //二叉树删除节点(只删除叶子节点, 只有一个子节点的Node)
      
      function remove (data) {
      	this.root = removeNode(this.root,data);
      }
      
      function removeNode (node, data) {
      	if(node === null) {
      	  return null;
      	}
      	
      	if(data === node.data) {
      	  if(node.left == null && node.right == null) {
      	    return null;
      	  }
      	  if(node.left === null) {
      	    return node.right;
      	  }
      	  if(node.right === null) {
      	    return node.left;
      	  }
      	  //这里有疑问, 如果node.left !== null && node.right !== right 这种情况怎么处理?
      	  //怪不得 上面说,只删除只有一个子节点的Node
      	  //逻辑上来讲, 可以把左子树 return 给 右子树, 
          //右子树 return 给 删除节点的 parent 是不是就可以保持结构了? 
      	}else if (data < node.data) {
      	  node.left = removeNode(node.left,data);
      	  return node;
      	}else {
      	  node.right = removeNode(node.right,data);
      	  return node;
      	}
      }
      抄写第二遍时,感觉 remove() removeNode() 这个递归用得实在是太巧妙了, 
      当初第一人到底是怎么想到这个结构的?

      第一个感觉是,每次递归的执行,不依赖递归返回的值?
      第二个感觉是,递归的过程当中,他的返回值很自然的又形成了一个对象,
      一个二叉树.怎么去的就怎么返回?

      也许我应该问, 如果 remove 和 removeNode 非要写在一个函数,是不是会变得很复杂?
      他是怎么想到要分离开的?

      或者我应该问,写这个的核心逻辑出发点在哪里?
      需求是: 删除节点,返回子节点,没有就返回自身?
      因为我没看懂,所以是我想复杂了吗?
      


      var bst = new BST();
      bst.insert(5);
      bst.insert(8);
      bst.insert(9);
      bst.insert(1);
      bst.insert(3);
      console.log(bst);
      // 这个二叉树,根节点取决于,头一个放谁进去.
      // 同样的一组数据,根据根节点放谁, 二叉树的结构也可能不同
```

在抄第二篇博客之前,发现,
第二篇博客和第一篇博客的内容完全不一样,
应该是第一篇的基础内容, 

 
        树状结构可以有很多种, 二叉树是其中一种.

        二叉树结构的数据存储有三种

      1.一种是数组.数组当中的顺序,反映二叉树中的位置.
          具体这个顺序和位置的关系,看博客,我也不是很清楚.
          (这个叫顺序存储结构)

      2.一种是二叉链表,
          每个节点有三个存储结构? 一个放left,一个放data,一个放right
          没错博客一,实际上就是二叉链表的形式.
          (这个叫链式存储结构)          

      3.一种是三叉链表,
          在left,data,right,之外放一个parent,用来指向parent.


    

下面是第二个博客的完整版代码.

```
(function () {
      	// 顺序存储结构的遍历
      	var tree = [1,2,3,4,5,,6,,,7];
      	// 先序遍历
      	console.log('preOrder');
      	void function preOrderTraverse (x, visit) {
      		visit(tree[x]);
      		tree[2 * x + 1] && preOrderTraverse(2 * x + 1,visit);
      		tree[2 * x + 2] && preOrderTraverse(2 * x + 2,visit);
      	}(0, function (value) {
      		console.log(value);
      	})
      	 
      	 //中序遍历
      	 console.log('inOrder:');
      	 void function inOrderTraverse (x, visit) {
          tree[2 * x + 1] && inOrderTraverse(2 * x + 1,visit);
          visit(tree[x]);
          tree[2 * x + 2] && inOrderTraverse(2 * x + 2,visit);
      	 }(0, function (value) {
          console.log(value);
        })
      	 
      	 console.log('postOrder:');
      	 void function postOrderTraverse (x, visit) {
          tree[2 * x + 1] && postOrderTraverse(2 * x + 1,visit);
          tree[2 * x + 2] && postOrderTraverse(2 * x + 2,visit);
          visit(tree[x]);
      	 }(0, function (value) {
          console.log(value);
        })
      })()
      
      
      var Stack = require('../Stack/stack');// 这就很尴尬了, 我不知道具体 Stack,Queue 怎么写的
      var Queue = require('../Queue/Queue').Queue;
      
      
      function BinaryTree (data, leftChild, rightChild) {
      	this.data = data || null;
      	// 左右孩子节点
      	this.leftChild = leftChild || null;
      	this.rihgtChild  rightChild || null;
      }
      
      exports.BinaryTree = BinaryTree;// 这是为了导出?
      
      BinaryTree.prototype = {// 这个跟 博客一上的区别是,把函数定义在原型链上, 调用方式是一样的.
        constructor : BinaryTree,
        // 判断两棵树是否相似
        
        isSimilar : function (tree) {// tree 是另一个节点数,也就是一个二叉树对象.假定是跟 this相同的结构就好理解
        	return tree && 
        	   this.leftChild && isSimilar.call(this.leftChild,tree.leftChild) && this.rightChild &&
        	   isSimilar.call(this.rightChild,tree.rightChild);
        	   // 真是各种递归用得太巧妙了. 
        	   // 想到一个题目, 如何比较两个 地址不同的 对象的内容是否相同? 回头想一下,
        },
        
        // 把一个数组,变成二叉树链式存储结构
        createBinaryTree: function (tree) {// 在一个函数里面递归另一个函数? 真是各种秀
          // 这尼玛,这个tree 很明显跟上面那个 tree 的数据类型应该不一样, 这个应该是个 数组,顺序存储结构.
        	void function preOrderTraverse (node, x, vist) {
        		visit (node,tree[x]);
        		tree[2 * x + 1] && preOrderTraverse(node.leftChild = new BinaryTree(), 2 * x + 1,visit);
        		tree[2 * x + 2] && preOrderTraverse(node.rightChild = new BinaryTree(), 2 * x + 2,visit); 
        	}(this,0,function (node,value) {
        		node.data = value;
        	})
        },
        //上面这段代码,能读懂, 但一时很难熟悉这种结构, 练习到后面,真的有可能随手就能写出这种结构?
        
        //先序遍历二叉树的非递归算法
        
        preOrder_stack: function  (visit) {// 所以我们可以把visit 看成是一个回调函数.
        	var stack = new Stack();// 这就懵逼了,他没具体写 Stack
        	//https://www.npmjs.com/package/stackjs 网上说这是个第三方 js
        	stack.push(this);
        	
        	while (stack.top) {// stack.js 没有top 属性或方法啊
        	  var p;
        	  // 向左走到尽头
        	  while ((p = stack.peek())){// stack.peek() 返回的应该是 stack 中 最后一个push进来的元素.
        	  	p.data && visit(p.data);// 放进一个stack,遍历一个,
        	  	stack.push(p.leftChild);
        	  }
        	  
        	  stack.pop();// 把上面循环之后的 最后一个 leftChild 清空.
        	  
        	  if (stack.top) {// top 依然不知道是什么东西 应该是指 跟节点, 或者头一个 push 进去的节点.
        	    p = stack.pop();// 把 最后倒数第二个 leftChild删除的同时拿出来, 因为一定会有 rightChild
        	    stack.push(p.rightChild);// 把rightChild拿出来.放进stack里.
        	    //这个循环的出口在哪里? 出口就是, stack.pop() 把this也给 删除的时候, stack.pop 就会false;
        	  }
        	}
        },
        // 勉强看懂了, 真是天秀. 程序员世界里,没有最装逼的, 只有更装逼的.
        preOrder_stack2: function (visit) {
        	var stack = new Stack();
        	var p = this;
        	// 用了一个类似数组的 stack ,不止能遍历一个 if 还能遍历 else 
        	// 也就是 能遍历两个方向?
        	while (p || stack.top){
        		if (p) {
        		  stack.push(p);
        		  p.data && visit(p.data);
        		  p = p.leftChild;
        		}else {
        		  p = stack.pop();
        		  p = p.rightChild;
        		}
        	}
        },
        // 能不能直接用两个循环进行遍历? 不用 stack
        preOrder_stack3 : function (visit) {
        	var p = this;
        	while (p){
        		p.data && visit(p.data);
        		p = p.leftChild;
        	}
        	
        	p = this.rightChild;
        	while (p){
        		p.data && visit(p.data);
        		p = p.rightChild;
        	}
        	// 写到一半我就知道这个不行了, 因为这样只能遍历最左一条链,和最右的一条链,中间的就遍历不了.
        	// 也就是必须要两个循环嵌套..
        },
        
        //中序排序 非递归方法.
        inOrder_stack1: function (visit) {
        	var stack = new Stack();
        	stack.push(this);
        	
        	while (stack.top){
        		var p;
        		// 向左走到尽头
        		while ((p = stack.peek())){
        			stack.push(p.leftChild);
        		}
        		stack.pop();
        		
        		if(stack.top) {
        		  p = stack.pop();
        		  p.data && visit(p.data);
        		  stack.push(p.rightChild);
        		}
        	}
        },
        inOrder_stack2: function (visit) {
        	var stack = new Stack();
        	var p = this;
        	
        	while (p || stack.top){
        		if (p) {
        		  stack.push(p);
        		  p = p.leftChild;
        		}else {
        		  p = stack.pop();
        		  p.data && visit(p.data);
        		  p = p.rightChild;
        		}
        	}
        },
        // 为了区分两次过栈的不同处理方式, 在堆栈中增加一个mark域,
        // mark = 0 表示刚刚访问此节点, mark = 1 表示左子树处理结束返回,
        // mark = 2 表示右子树处理结束返回. 每次根据栈顶的mark域决定做何动作
        
        postOrder_stack: function (visit) {
        	var stack = new Stack();
        	stack.push([this,0]);
        	
        	while (stack.top){
        		var a = stack.pop();
        		var node = a[0];
        		
        		switch (a[1]){
        			case 0:
        			  stack.push([node,1]);// 修改 mark 域
        			  if(node.leftChild) stack.push([node.leftChild,0]);
        				break;
        			case 1:
        			  stack.push([node,2]);
        			  if (node.rightChild) stack.push([node.rightChild,0]);
        			  break;
        			case 2:
        			   node.data && visit(node.data);
        			  break;
        			default:
        				break;
        		}
        	}
        },
        // 还是很秀..消化困难.
        
        
        //递归版本 先序
        preOrderTraverse: function (visit) {
        	visit(this.data);
        	if (this.leftChild) preOrderTraverse.call(this.leftChild,visit);
        	if (this.rightChild) preOrderTraverse.call(this.rightChild,visit);
        },
        // 递归版 中序
        inOrderTraverse : function (visit) {
          if (this.leftChild) inOrderTraverse.call(this.leftChild,visit);
          visit(this.data);
          if (this.rightChild) inOrderTraverse.call(this.rightChild,visit);
        },
        // 递归版 后序
        postOrderTraverse : function (visit) {
          if (this.leftChild) postOrderTraverse.call(this.leftChild,visit);
          if (this.rightChild) postOrderTraverse.call(this.rightChild,visit);
          visit(this.data);
        },
        // 原来递归真的比循环更简洁吗?
        
        levelOrderTraverse : function (visit) {
        	var queue = new Queue();// 这个js也没见过.
        	// 这个似乎是 系统自带的一个模块之一. 系统组件之一.
        	// 用来创建,先入先出的东西?
        	//https://msdn.microsoft.com/zh-cn/library/system.collections.queue(v=vs.110).aspx
        	// 好像还不是上面这个组件.
        	// enQueue 就先简单理解成push
        	// queue 是队列的意思..
        	// 讲解 https://blog.csdn.net/dengpei187/article/details/51880491
        	// 队列（Queue）是只允许在一端进行插入工作，而在另一端进行删除操作的线性表。队列是一种先进先出（First In First Out）的线性表，简称FIFO。允许插入的一端称为队尾，允许删除的一端称为队头。
        	queue.enQueue(this);
        	while (queue.rear){ // 最后一个元素的下一个元素,循环,所以是第一个元素. 不深究,咱先把本篇抄录一下再说.
        		var p = queue.deQueue ();// 就相当于 shift 方法?
        		p.data && visit(p.data);
        		p.leftChild && queue.enQueue(p.leftChild);
        		p.rightChild && queue.enQueue(p.rightChild);
        	}
        },
        
        //求先序序列为k的节点的值
        getPreSequence : function (k) {
        	var count = 0;
        	
        	void function recurse (node) {
        		if (node) {
        		  if (++count === k) {
        		    console.log('Value is: ' + node.data);
        		  } else {
        		    recurse(node.leftChild);
        		    recurse(node.rightChild);
        		  }
        		}
        	}(this);
        },
        
        // 求二叉树中叶子节点的数目.
        
        countLeaves: function () {
        	return function recurse (node) {
        		if (!node) return 0;
        		else if (!node.leftChild && !ndoe.rightChild) return 1;
        		else return recurse(node.leftChild) + recurse(node.rightChild);
        	}(this);
        },
        
        // 交换所有节点的左右子树
        revoluteBinaryTree : function revoluteBinaryTree () {
        	var temp = this.leftChild;
        	this.leftChild = this.rightChild;
        	this.rightChild = temp;
        	
        	if (this.leftChild) revoluteBinaryTree.call(this.leftChild);
        	if (this.rightChild) revoluteBinaryTree.call(this.rightChild);
        },
        
        // 求二叉树中以值为x的节点为根的子树深度
        getSubDepth : function getSubDepth (x) {
        	if (this.data === x) {
        		console.log('subDepth: ' + this.getDepth());// 这个函数应该在下面定义了.
        	} else{
        		if (this.leftChild) getSubDepth.call(this.leftChild, x);
        		if (this.rightChild) getSubDepth.call(this.rightChild, x);
        	}
        },
        // 返回二叉树的深度.
        getDepth: function getDepth () {
        	if (this === global) return 0;
        	else {
        	  var m = getDepth.call(this.leftChild);
        	  var n = getDepth.call(this.rightChild);
        	  return (m > n ? m : n) + 1;// 我了个擦, 这个 + 1 是神来之笔吗?
        	}
        },
        // 删除所有以元素x为根的子树
        delSubX : function delSubX (x) {
        	if (this.data === x) {
        		this.leftChild = null;
        		this.rightChild = null;
        	} else {
        	  if (this.leftChild) delSubX.call(this.leftChild,x);// 原文应该是忘了传这个x了.
        	  if (this.rightChild) delSubX.call(this.rightChild,x);
        	}
        	// 这个版本和 博客一相比, 博客一里的需求是把后面的树给连上, 这里是直接删除整个树.
        },
        // 非递归赋值二叉树
        copyBinaryTree_stack : function () {
        	// 用来存放本体节点的栈
        	var stack1 = new Stack();
        	// 用来存放新二叉树节点的栈
        	var stack2 = new Stack();
        	stack1.push(this);
        	var newTree = new BinaryTree();
        	var q = newTree;
        	stack2.push(newTree);
        	var p;
        	
        	while (stack1.top){
        		// 向左走到尽头
        		while ((p = stack1.peek())){
        			if (p.leftChild) q.leftChild = new BinaryTree();
        			q = q.leftChild;
        			stack1.push(p.leftChild);
        			stack2.push(q);
        		}
        		
        		p = stack1.pop();
        		q = stack2.pop();
        		
        		if (stack1.top) {
        		  p = stack1.pop();
        		  q = stack2.pop();
        		  if (p.rightChild) q.rightChild = new BinaryTree();
        		  q.data = p.data;
        		  q = q.rightChild;
        		  stack1.push(p.rightChild); // 向右一步
        		  stack2.push(q);
        		}
        	}
        	return newTree;
        },
        // 求二叉树中节点p和q的最先祖先
        findNearAncient : function (pNode,qNode) {
        	var pathP = [];
        	var pathQ = [];
        	findPath(this, pNode, pathP, 0);
        	findPath(this, qNode, pathQ, 0);
        	
        	for (var i = 0; pathP[i] == pathQ[i] && pathP[i];i++);
        	// 这又是什么秀操作? 明白了..
        	return pathP[--i];
        },
        toString : function () {
        	// 这是用来干嘛的?
        },
        // 求一颗二叉树的繁茂度.
        // 繁茂度的定义：各层节点数的最大值与树的高度的乘积 
        lunshDegree : function () {
        	var countArr = [];
        	var queue = new Queue();
        	queue.enQueue({
        	  node: this,
        	  layer: 0// 用来表示在几层.
        	});
        	// 利用层序遍历来统计各层的节点数
        	var r;
        	while (queue.rear){
        		r = queue.deQueue();// deQueue 就相当于是  pop来着? 
        		countArr[r.layer] = (countArr[r.layer] || 0) + 1;
        		// 2.只要同一层级的再次出现,就 +1;
        		// 我刚开始错误的认为 countArr[r.layer] = r.layer//导致我一直想不通,觉得max只能是countArr[last]
        		if (r.node.leftChild) {
        		  queue.enQueue({
        		    node:r.node.leftChild,
        		    layer:r.layer + 1
        		  });
        		}
        		if (r.node.rightChild) {
        		  queue.enQueue({
        		    node: r.node.rightChild,
        		    layer: r.layer + 1
        		  });
        		}
        		// 1.先给在同一层级的节点进行标记,在几层. 2在上面
        	}
        	//最后一个队列元素所在层就是树的高度
        	var height = r.layer;
        	for (var max = counArr[0],i = 1;countArr[i];i++) {
        	  //求层最大节点数
        	  if(countArr[i] > max) max = countArr[i];
        	}
        	return height * max;// 繁茂度的定义就是这个..
        	//真是,从头到尾一直秀..难道是我基础太差了?
        },
        // 求深度等于树的高度减一的最靠左的节点.
        printPath_maxDepthS1: function () {
        	var maxh = this.getDepth();
        	var path = [];
        	
        	if (maxh < 2) return false;//表示只有一个节点.
        	
        	find_h(this,1);
        	
        	function find_h (tree,h) {
        		path[h] = tree;
        		
        		if (h == maxh - 1) {
        		  var s = ' ';
        		  for (var i = 1; path[i]; i++) s += path[i].data + (path[i + 1] ? '->' : '');
        		  // 这什么鬼? 无论 if 还是 for 来个空格就可以把 {} 省略? 测试发现确实这样.
        		  // 看来我真实小白..
        		  console.log(s);
        		  return;
        		}else {
        		  if (tree.leftChild) find_h(tree.leftChild, h + 1);
        		  if (tree.rightChild) find_h(tree.rightChild, h + 1);
        		}
        		path[h] = null;
        		// 
        	}
        },
        //求树节点的子孙总数填入descNum域中, 并返回
        descNum : function () {
        	return function recurse (node) {
        		var d ;
        		if (!node) return -1;
        		else d = recurse(node.leftChild) + recurse(node.rightChild) + 2;
        		
        		node.desNum = d;
        		return d;
        	}(this);
        }
      }// 原型链上的结束
      
      //判断二叉树是否完全二叉树
      BinaryTree.isFullBinaryTree = function (tree) {
      	var queue = new Queue();
      	var flag = 0;
      	queue.enQueue(tree);
      	
      	while (queue.rear){// 如果队列不为空, 依然return false,就表明leftChild和rightChild当中有一个是null
      	  // 不对啊, 如果 queue.rear 指的是最后一个元素的下一个,那么这个循环不合理啊..
      		var p = queue.deQueue();// 也就是 非完全二叉树
      		//
      		if(!p) flag = 1;
      		else if (flag) return false;
      		// 为什么  这两句 不直接改成 if (!p) return false;? 为什么要借助flag,再走一圈?
      		// 因为完全二叉树的最后一个元素
      		else {
      		  queue.enQueue(p.leftChild);// 前面是不是要添加 if(p.leftChild)啊?
      		  queue.enQueue(p.rightChild);// p.rightChild == null时 应该也会放进队列里.
      		}
      	}
      	return true;
      	// *** 这个函数的逻辑没想通.
      }
      
      
      
      function findPath (tree, node,path,i) {// 这个为什么不放在原型链上?因为有可能处理的数据和this树无关?
      	var found = false;
      	
      	void function recurse (tree, i) {
      		if (tree == node) {
      			found = true;
      			return;// 这个函数不需要返回? 因为整个过程我们递归用的都是同一个path,递归结束之后,path也就生成了.
      			// 我现在觉得这篇代码的价值根本不在什么二叉树是什么玩意,
      			// 这篇代码的价值是,简直就是各种花样写递归的教材嘛..
      			// 当然还有 for循环.
      		}
      		
      		path[i] = tree;
      		if (tree.leftChild) recurse(tree.leftChild, i + 1);
      		if (tree.rightChild && !found) recurse(tree.rightChild, i + 1);
      		if (!found) path[i] = null;
      	}(tree,i);
      }
      
      var global = Function ('return this;')();
      
      // 一下就是测试上面写的函数
      void function test () {
      	var tree = [1,2,3,4,5,,6,,,7];
      	var test = new BinaryTree();
      	test.createBinaryTree(tree);
      	test.preOrderTraverse(function (value) {
      		console.log('preOrder: ' + value);
      	});
      	test.inOrderTraverse(function (value) {
      		console.log('inOrder: ' + value);
      	});
      	test.postOrderTraverse(function (value) {
      		console.log('postOrder: ' + value);
      	});
      	
      	test.preOrder_stack(function (data) {
      		console.log('preOrderNonRecusive: ' + data);
      	});
      	test.preOrder_stack2(function (data) {
      		console.log('preOrder_stack2: ' + data);
      	});
      	test.inOrder_stack1(function (value) {
      		console.log('inOrder_stack1: ' + value);
      	});
      	test.inOrder_stack2(function (value) {
      		console.log('inOrder_stack2: ' + value);
      	});
      	test.postOrder_stack(function (value) {
      		console.log('postOrder_stack: ' + value);
      	});
      	test.getPreSequence(5);
      	console.log(test.countLeaves());
      	test.getSubDepth(6);
      	test.getSubDepth(2);
      	test.levelOrderTraverse(function (value) {
      		console.log('levelOrderTraverse: ' + value);
      	});
      	
      	var newTree = test.copyBinaryTree_stack();
      	
      	var node1 = test.leftChild.leftChild;
      	var node2 = test.leftChild.rightChild.leftChild;
      	var ancient = test.findNearAncient(node1,node2);
      	console.log(ancient);
      	console.log('expect false: ' + BinaryTree.isFullBinaryTree(newTree));
      	console.log('lush degree: ' + test.lunshDegree());
      	
      	test.printPath_maxDepthS1();
      	console.log(test.descNum());
      }
```


