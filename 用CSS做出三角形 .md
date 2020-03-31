# 用CSS做出三角形

## 原理剖析

做一個`width`為0、`height`為0，`border`為40的元素

```pug
div
```

```sass
div
 width: 0
 height: 0
 border: 40px solid #000
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/01.png)

4個`border`都給予不同顏色，發現邊框與邊框之間呈現45度角

```sass
div
 width: 0
 height: 0
 border-top: 40px solid aliceblue
 border-bottom: 40px solid cadetblue
 border-left: 40px solid lightblue
 border-right: 40px solid skyblue
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/02.png)

移除`border-top`，並將`border-bottom`的寬度改成2倍大

```sass
div
 width: 0
 height: 0
 border-bottom: 80px solid cadetblue
 border-left: 40px solid lightblue
 border-right: 40px solid skyblue
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/03.png)

將`border-right`、`border-left`的顏色都設為`transparent`

```sass
div
 width: 0
 height: 0
 border-bottom: 80px solid cadetblue
 border-left: 40px solid transparent
 border-right: 40px solid transparent
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/04.png)

## 快速複製區

### 正三角形

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/04.png)

```sass
div
 width: 0
 height: 0
 border-bottom: 80px solid cadetblue
 border-left: 40px solid transparent
 border-right: 40px solid transparent
```

### 倒三角形

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/05.png)

```sass
div
 width: 0
 height: 0
 border-top: 80px solid cadetblue
 border-left: 40px solid transparent
 border-right: 40px solid transparent
```

### 右三角形

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/06.png)

```
div
 width: 0
 height: 0
 border-left: 80px solid cadetblue
 border-top: 40px solid transparent
 border-bottom: 40px solid transparent
```

### 左三角形

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/用CSS做出三角形/07.png)

```
div
 width: 0
 height: 0
 border-right: 80px solid cadetblue
 border-top: 40px solid transparent
 border-bottom: 40px solid transparent
```

