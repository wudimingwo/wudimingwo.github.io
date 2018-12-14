parseFloat(string)
parseFloat(string)转换成浮点数字，就是正常小数


例 var demo = “100.2”;
var num = parseFloat (demo);
console.log(typeof(num) + “:” + num);
答案显示 number: 100.2


例 var demo = “100.2.3”;
var num = parseFloat (demo);
console.log(typeof(num) + “:” + num);
答案显示 number: 100.2


例 var demo = “100.2abc”;
var num = parseFloat (demo);
console.log(typeof(num) + “:” + num);
答案显示 number: 100.2


parseFloat 从数字类开始看，看到除了第一个点以外的非数字类为截止，返回前面的
数