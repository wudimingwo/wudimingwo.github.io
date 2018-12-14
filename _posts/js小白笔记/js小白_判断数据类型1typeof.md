typeof 能返回的六种数据类型（区分数字类型）
number、string、boolean、undefined、object、function
返回的都是字符串格式.

typeof 判断数据,主要用来区分是引用值还是原始值.
''object'':引用值  (除了null)
其他: 原始值

function比较特殊.
```
function name () {}//name是函数
name.age = 18;
name.son = 'mike';
//又可以像对象一样使用.
//这种在前期容易混淆,不容易消化的看似特殊现象,
//在后期可以被灵活的使用
```