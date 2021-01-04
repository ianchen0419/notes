# 檢查陣列是否包含特定值 includes()

`includes()` 可以用來檢查陣列是否包含某個值，回傳值為布林值

```javascript
var arr=['2020/01/01', '2020/01/02', '2020/01/03'];

console.log(arr.includes('2020/01/01')) //true
```

## 結合 `filter()` 篩出特定值組合成一個新陣列

```javascript
var arr=['2020/01/01', '2020/01/02', '2020/01/03', '2020/02/01', '2020/02/02', '2020/02/03'];

var arr2=arr.filter(item => item.includes('2020/01'));
console.log(arr2); //["2020/01/01", "2020/01/02", "2020/01/03"]
```
