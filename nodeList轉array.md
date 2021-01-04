# nodeList轉array

由`querySelectorAll()`抓取下來的物件，雖然看起來跟`array`很像，但他其實是`nodeList`，所以不能直接適用於`array`可以用的一大堆好用`method`，例如`map()`、`reduce()`等等

```pug
ul
 li apple
 li banana
 li grape
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/nodeList轉array/01.png)

## ES6法 展開運算符 Spread syntax

Spread syntax是ES6提供的方法，只要用`[...]`就能夠轉換了

```javascript
var mylist=document.querySelectorAll('li');
var newlist=[...mylist];
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/nodeList轉array/01.png)


## 傳統法 `Array.from()`

如果瀏覽器較舊不支援ES6 `[...]`大法的話，也能改用傳統的`Array.from()`
雖然不比ES6法簡潔，但也算方便


```javascript
var mylist=document.querySelectorAll('li');
var newlist=Array.from(mylist);
```