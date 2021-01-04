# CSS not selector

## 指定不要選到某`class`的元素

語法：`:not(.your-class)`

```pug
h1.h1 h111
h1.h2 h222
h1.h3 h333
```

```sass
h1:not(.h1)
 color: red
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/CSS%20not%20selector/01.png)

## 指定不要選到某`attribute`的元素

抓取`attribute`名稱的範例

```pug
h1.h1(data-h1) h111
h1.h2(data-h2) h222
h1.h3(data-h3) h333
```

```sass
h1:not([data-h1])
 color: red
```

抓取`attribute`名稱+內容的範例

```pug
h1.h1(data-heading="h1") h111
h1.h2(data-heading="h2") h222
h1.h3(data-heading="h3") h333
```

```sass
h1:not([data-heading="h1"])
 color: red
```

## 多重條件

```pug
h1.h1 h111
h1.h2 h222
h1.h3 h333
```

```sass
h1
 color: red
 
h1:not(.h2):not(.h3)
 color: black
```
