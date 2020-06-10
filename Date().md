# Date()

* 抓現在是西元幾年 `new Date().getFullYear()`
* 抓現在是幾點 `new Date().getHours()`
* 抓現在是幾分 `new Date().getMinutes()`
* 抓現在是幾秒 `new Date().getSeconds()`

## 顯示現在時間

```javascript
function runTime(){
 var now=new Date();
 var seconds=now.getSeconds();
 var mins=now.getMinutes();
 var hours=now.getHours();
 console.log(`現在是${hours}時${mins}分${seconds}秒`);
}
//每一秒偵測一次時間
setInterval(runTime, 1000);
```