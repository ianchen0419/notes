# 模板字符串 Template Literals

模板字符串是ES6的新標準，IE不能使用　　
捨棄宣告傳統字串的雙引號`"`/單引號`'`，改用重音符號宣告　　
字串裡面可以使用變數，提升了方便性也減低了撰寫字串的痛苦

```javascript
var a=3;
var b=2;

var str=`Hi! I Have ${a+b} apple`;
console.log(str) //"Hi! I Have 5 apple"
```