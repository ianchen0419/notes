# JavaScript Array methods 陣列相關方法1

## 本篇介紹的`method`

|Method		|解說														|解說	|
|-----------|-----------------------------------------------------------|-------|
|`filter()`	|`[👧, 👦, 👩, 👨, 👵, 🧓]` => `[👦, 👨, 🧓]`				|原本的陣列有 `6` 個，後來變成 `3` 個|
|`map()`	|`[👧, 👦, 👩, 👨, 👵, 🧓]` => `[👧🏿, 👦🏿, 👩🏿, 👨🏿, 👵🏿, 🧓🏿]`|陣列內容都變成不一樣的顏色了（但數量一樣是 `6` 個）|
|`sort()`	|`[👧, 👦, 👩, 👨, 👵, 🧓]` => `[👧, 👩, 👵 👦, 👨, 🧓]`	|陣列的順序改變了|
|`reduce()`	|`[👧, 👦, 👩, 👨, 👵, 🧓]` => `👨‍👩‍👧`						|陣列被綜合成一個東西了|

## 本篇使用到的共用物件

```javascript
const inventors = [
 { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
 { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
 { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
 { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
 { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
 { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },
 { first: 'Max', last: 'Planck', year: 1858, passed: 1947 },
 { first: 'Katherine', last: 'Blodgett', year: 1898, passed: 1979 },
 { first: 'Ada', last: 'Lovelace', year: 1815, passed: 1852 },
 { first: 'Sarah E.', last: 'Goode', year: 1855, passed: 1905 },
 { first: 'Lise', last: 'Meitner', year: 1878, passed: 1968 },
 { first: 'Hanna', last: 'Hammarström', year: 1829, passed: 1909 }
 ];
```

## `filter()` 把陣列的數量變少，但是內容不變

`filter()` 裡面放一個函數，`filter()` 可以**物件→物件**，也能夠**陣列→陣列**

### 應用：篩選出出生於 `16` 世紀的投資客（出生年介於 `1500` 到 `1600` 之間）

```javascript
const arr1=inventors.filter(function(item){
 if(item.year>=1500 && item.year<1600){
  return true;
 }
})

console.log(arr1); //[{ first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 }, { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 }]
```

### ES6 應用：箭頭函數（省略 `return`）

```javascript
const arr1=inventors.filter(item => item.year>=1500 && item.year<1600);

console.log(arr1); //[{ first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 }, { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 }]
```

## `map()` 陣列數量固定，但裡面內容置換

`map()` 可以**物件→陣列**，也可以**陣列→陣列**

### 應用：列出所有投資客的全名（`first` + `last`）

```javascript
const arr1=inventors.map(item => `${item.first} ${item.last}`);

console.log(arr1); //["Albert Einstein", "Isaac Newton", "Galileo Galilei", "Marie Curie", "Johannes Kepler", "Nicolaus Copernicus", "Max Planck", "Katherine Blodgett", "Ada Lovelace", "Sarah E. Goode", "Lise Meitner", "Hanna Hammarström"]
```

## `sort()` 更動陣列順序

`sort()` 可以**物件→物件**，也能夠**陣列→陣列**

* `return 1`：往後移動
* `return -1`：往前移動

### 應用①：將投資客由老排到年輕（出生年數字越大代表越年輕，所以要越往後移動）

`sort()` 裡面的函數可以塞兩個參數，第一個值代表比較的第一個人、第二個值代表比較的第二個人，`sort()` 會幫忙把所有排列組合都列出來

```javascript
const arr1=inventors.sort(function(a, b){
 if(a.year>b.year){
  return 1; //如果a的年紀比b小，a往後擺
 }else{
  return -1;
 }
});

console.table(arr1); //結果會出來一個由老排到小的物件
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/JavaScript%20Array%20methods%20陣列相關方法1/01.png)

### ES6 應用：箭頭函數 + `if` 簡寫

```javascript
const arr1=inventors.sort((a, b) => a.year>b.year ? 1 : -1)

console.table(arr1);
```

### 應用②：將投資客的名字 (firstname) 開頭字母由A排到Z

```javascript
const arr1=inventors.sort((a, b) => a.first>b.first ? 1 : -1)

console.table(arr1);
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/JavaScript%20Array%20methods%20陣列相關方法1/02.png)


## `reduce()` 將陣列內容輸出為單一值

`reduce()` 可以**物件→單一值**，也可以**陣列→單一值**

### 應用①：計算所有投資客總共活了多久

* `reduce()` 裡面的函數的第一個參數為「累加器 `accumulator`」，第二個參數為「迭代中的元素 `currentValue`」
* `reduce()` 裡面的第二個值為一個數字，表示「累加器初始值 `initialValue`」（通常填 `0`）

```javascript
const value=inventors.reduce(function(total, item){
 return total += (item.passed-item.year);
}, 0)

console.log(value); //861
```

### ES6 應用：箭頭函數

```javascript
const value=inventors.reduce((total, item) => total += (item.passed-item.year), 0)

console.log(value); //861
```

### 應用②：統計各個交通工具出現的次數

```javascript
//原始資料
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];
```

```javascript
var value=data.reduce((obj, item)=>{
 obj[item]++;
 return obj;
},{
 car: 0,
 walk: 0,
 truck: 0,
 bike: 0,
 van: 0
})

console.log(value); // {bike: 2, car: 5, truck: 3, van: 2, walk: 2}
```




