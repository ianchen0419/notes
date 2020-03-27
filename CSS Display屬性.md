# CSS Display屬性

## display: block

* `<div>`, `<h1>`的預設屬性
* 元素寬度預設填滿寬度，並且會往下掉
* 排版css支援情況
  * `height`：支援
  * `width`：支援
  * `margin`：支援
  * `padding`：支援 

```pug
div block
div block
div block
div block
div block
```

```sass
 div
	border: 1px solid #000
	display: block
	height: 50px
	margin: 10px 20px
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/CSS%20Display屬性/01.png)

## display: inline
* `<span>`, `<a>`的預設屬性
* 不會像block一直往下掉
* 排版css支援情況
  * `height`：不支援
  * `width`：不支援
  * `margin`：僅支援`margin-left`、`margin-right`
  * `padding`：僅支援`padding-left`、`padding-right`

```pug
div inline
div inline
div inline
div inline
div inline
```

```sass
div
	border: 1px solid #000
	display: inline
	height: 50px
	margin: 10px 20px
```
![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/CSS%20Display屬性/02.png)

## display: inline-block

* `<img>`預設屬性
* 元素不會往下掉，會往右排
* 排版css支援情況
  * `height`：不支援
  * `width`：不支援
  * `margin`：支援
  * `padding`：支援

```pug
div inline-block
div inline-block
div inline-block
div inline-block
div inline-block
```

```sass
div
	border: 1px solid #000
	display: inline-block
	height: 50px
	margin: 10px 20px
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/CSS%20Display屬性/03.png)

