# SVG stroke-linecap

`stroke-linecap`用來描述線段`<line>`的端點呈現方式，提供三種屬性

* `stroke-linecap: butt` 預設值，端點不外擴也不變形
* `stroke-linecap: round` 端點外擴並呈現圓角
* `stroke-linecap: square` 端點外擴並呈現方角
（中間畫一條`<path>`比較好觀察外擴情形）


## `butt`（預設值）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG%20stroke-linecap/01.png)

```pug
svg(viewbox="-50 -50 100 100" width="500")
	line(x1=-40 y1=0 x2=40 y2=0 stroke="black" stroke-width=8 stroke-linecap="butt")
	path(d="M-40, 00 L40, 0" stroke="white")
```

## `round`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG%20stroke-linecap/02.png)

```pug
svg(viewbox="-50 -50 100 100" width="500")
	line(x1=-40 y1=0 x2=40 y2=0 stroke="black" stroke-width=8 stroke-linecap="round")
	path(d="M-40, 00 L40, 0" stroke="white")
```

## `square`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG%20stroke-linecap/03.png)

```pug
svg(viewbox="-50 -50 100 100" width="500")
	line(x1=-40 y1=0 x2=40 y2=0 stroke="black" stroke-width=8 stroke-linecap="square")
	path(d="M-40, 00 L40, 0" stroke="white")
```
