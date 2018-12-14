例 var num = Number(‘123’);
 //123

例 var demo = “123”;
var num = Number(demo);
//123

例 var demo = true;
var num = Number(demo);
// 1

例 var demo = false;
var num = Number(demo);
// 0

例 var demo = null;
var num = Number(demo);
//0

例 var demo = [];
var num = Number(demo);
//0

例 var demo = [123];
var num = Number(demo);
//123

例 var demo = [1,2];
var num = Number(demo);
//NaN

例 var demo = undefined;
var num = Number(demo);
//NaN

例 var demo = “abc”;
var num = Number(demo);
//NaN

例 var demo = “-123”;
var num = Number(demo);
//-123

例 var demo = “123abc”;
var num = Number(demo);
// NaN

例 var demo = function () {};
var num = Number(demo);
// NaN

引用值当中,只有[],null,[123] 不为0 其他都是NaN