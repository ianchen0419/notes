# dataset

`dataset`是一個方便取用元素屬性的規範  
基本上元素屬性的命名是任意，但在`dataset`的規範下，會命名成以`data-`開頭的名稱，例如

```pug
#div(data-color="green" data-size="20")
```

如此一來，可以用強大的`dataset`物件快速取得屬性值

```javascript
div.dataset.color; //'green'

div.dataset.size; //'20'
```

針對不能用`dataset`的瀏覽器（例如很舊的IE），就只能使用傳統的`getAttribute()`

```javascript
div.getAttribute('data-color'); //'green'

div.getAttribute('data-size'); //'20'
```