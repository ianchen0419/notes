# console 相關method介紹

`console`系列除了開發抓蟲最常用的`console.log()`以外，還存在著許多便利的`method`，幫助在開發中更有智慧的抓蟲

## 字詞置換 `%s`

`%s`的`s`是`string`的意思，可以做到在噴出除錯訊息時做到字詞置換的效果

```javascript
var a='apple';
console.log('hello, I want a %s', a);
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/01.png)


## 樣式變更 `%c`

在多人開發的環境中，`console log`時常會被上百個訊息給淹沒，這時可以透過`%c`自訂顯目的樣式讓他在很多訊息之中脫穎而出

```javascript
var style='font-size: 60px; background: red; color: white';
console.log('%cImportant!', style);
````

`%c`如果放在訊息開頭的地方表示他從最頭開始就要套上醒目樣式，如果`%c`宣告在訊息中間的話則代表從指定的位置開始再做醒目提示

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/02.png)

## 警告/錯誤/提示訊息

這三種在一般開發上都蠻少見，但在別人做好的套件上會常常看到

### 警告訊息 `console.warn()`

`console.warn()`用來提示警告性的訊息，在Chrome上的樣式是驚嘆號三角形+黃色底的造型

```javascript
console.warn('我是警告訊息');
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/03.png)

### 錯誤訊息 `console.error()`

`console.error()`用來提示錯誤性的訊息，在Chrome上的樣式是圓形叉叉+紅色底的造型

```javascript
console.error('我是錯誤訊息');
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/04.png)

### 提示訊息 `console.info()`

`console.info()`居然被新版的Chrome移除了，他現在用起來跟`console.log()`無異


## 驗證 `console.assert()`

```javascript
console.assert(1===2);
```

第二個值可填可不填，填了如果出錯時他會幫你噴出自訂的錯誤訊息  
（填了第二個值的範例：`console.assert(1===2, '錯了');`）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/05.png)

## 清除 `console.clear()`

用了就會幫你把上面的歷史紀錄都清掉

## 檢視屬性 `console.dir()`

他可以一口氣噴出指定元素的所有屬性，像是`offsetTop`、`innerHTML`、`parentNode`、以及綁在他身上的各種事件

```javascript
console.dir(document.body);
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/06.png)

## 群組化呈現 `console.group()`

這也是給多人開發時使用的便利工具，尤其是在同一頁面同時噴出好幾百個log令人無法招架時，可以用`console.group()`將訊息歸類分群組

```javascript
console.group('===登入頁測試區===');
console.log('假log1');
console.log('假log2');
console.log('假log3');
console.groupEnd();

console.group('===首頁測試區===');
console.log('假log1');
console.log('假log2');
console.log('假log3');
console.groupEnd();
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/07.png)

上面的`console.group()`預設是將所有訊息展開，如果怕他太亂也可以試試看`console.groupCollapsed()`，是預設收合的樣式

```javascript
console.groupCollapsed('===登入頁測試區 測試已完成===');
console.log('假log1');
console.log('假log2');
console.log('假log3');
console.groupEnd();

console.group('===首頁測試區===');
console.log('假log1');
console.log('假log2');
console.log('假log3');
console.groupEnd();
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/08.png)

## 計算次數 `console.count()`

`console.count()`原意是計算次數，但可以巧妙的把它塞進某些`function`之中，觀察該函式被使用的次數（看執行效能？）

```javascript
const arr=[1,3,5,7,9];
arr.reduce((total, number)=>{
 console.count();
 return total+=number;
},0);
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/09.png)

`reduce()`看起來只是一個簡單的`method`而已，寫起來也不過幾行，沒想到一放入`console.count()`就發現他默默地被執行了`5`次

## 計算時間 `console.time()`

`console.time()`可以計算一個動作執行時所花費的時間，藉以觀察效能
由於一般程式執行速度都很快，所以這邊用一個跟外部檔案抓資料的`fetch()`範例來看看花費時間

```javascript
console.time("抓下資料");
fetch("https://gist.githubusercontent.com/ianchen0419/d499e572044655814f38aaf56c779823/raw/9876407c12b1e6bc5c31fe6e9f875ccfb82af43b/schedule.json")
 .then(data => data.json())
 .then(data => {
  console.timeEnd("抓下資料");
  console.log(data);
});
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/10.png)


## 陣列+物件資料用表格呈現 `console.table()`

`console.table()`可以把一坨難看懂的陣列物件複合資料用表格呈現，可以一目瞭然增加易讀性

```javascript
fetch("https://gist.githubusercontent.com/ianchen0419/d499e572044655814f38aaf56c779823/raw/9876407c12b1e6bc5c31fe6e9f875ccfb82af43b/schedule.json")
 .then(data => data.json())
 .then(data => {
  console.table(data);
});
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/console%20相關method介紹/11.png)
