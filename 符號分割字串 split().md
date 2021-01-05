# 符號分割字串 split()

## 字串的分割

`split()` 裡面填入一個字串形式的值，這個值用來切割其他要拿來切割的字串

```javascript
var str='2020/01/01';
console.log(str.split('/')); //["2020", "01", "01"]
```

## 陣列=>字串的分割

陣列可以搭配 `map()` 轉換成字串在分割，但分割後的格式會變成陣列中的陣列

```javascript
var arr=['2020/01/01 15:00', '2020/04/04 13:00', '2020/03/03 09:00'];
var arr2=arr.map(item => item.split(' '));
console.log(arr2); //[["2020/01/01", "15:00"], ["2020/04/04", "13:00"], ["2020/03/03", "09:00"]]
```

或乾脆只抓取分割後的某部分，組成新的陣列

```javascript
var arr=['2020/01/01 15:00', '2020/04/04 13:00', '2020/03/03 09:00'];
var arr2=arr.map(item => {
 var [date, time]=item.split(' ');
 return date;
})
console.log(arr2); //["2020/01/01", "2020/04/04", "2020/03/03"]
```

## `shift()` 切出第一個字串

```javascript
var str="2020/01/01"
console.log(str.split('/').shift()); //"2020"
```

## `pop()` 切出最後一個字串

```javascript
var str="2020/01/01"
console.log(str.split('/').pop()); //"01"
```