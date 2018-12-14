cloneNode基本特点.
```
        var cln = dom.cloneNode(true);
        复制包括子元素.
        var cln = dom.cloneNode(false);
        复制不包括子元素,包括属性节点.

        cloneNode复制不包括元素绑定的事件
```
与对象深度克隆相比
```
无法通过对象深度克隆的方式克隆元素.
原因在于,
dom元素本身虽然也是对象,
但元素相关的属性,子元素都是独立的对象.
这些都无法深度克隆.
```
jq上的克隆是可以把事件也一起复制