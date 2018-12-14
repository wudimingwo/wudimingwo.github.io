> fill
```
            Array.prototype.myFill = function (value,start = 0,end = this.length) {
            	for(let i = start; i < end; i++) {
            	  this[i] = value;
            	}
            }
```
> 这里有个发现, es6默认值可以调用 this,确实方便

----
> find
```
            Array.prototype.myFind = function (fn, start = 0,end = this.length) {
            	for(let i = start; i < end; i++){
            	  if(fn.call(this,this[i],i,this)){
            	    return this[i]
            	  }
            	}
            }
```
---
> findIndex
```
            Array.prototype.myFindIndex = function (fn, start = 0,end = this.length) {
            	for(let i = start; i < end; i++){
            	  if(fn.call(this,this[i],i,this)){
            	    return i
            	  }
            	}
            	return -1
            }
```