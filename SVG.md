# SVG

## viewbox

```
viewbox="右上角的X座標 右上角的Y座標 寬度 高度"
```

右上角的X座標，建議設定為`0`  
右上角的Y座標，建議設定為`0`  
這樣，svg圖形的中心點會為`(寬度/2, 高度/2)`

## 圓形

```
circle(cx=圓心X座標 cy=圓心Y座標 r=半徑)
```

```pug
svg(viewbox="0 0 100 100" width="300" height="300")
 circle(cx=50 cy=50 r=10)
```

```sass
svg
 border: 1px solid #000
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG/01.png)

## 方形

```
rect(右上角X座標 右上角Y座標 寬度 高度)
```

```pug
svg(viewbox="0 0 100 100" width="300" height="300")
 rect(x=40 y=40 width=20 height=20)
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG/02.png)

## stroke與fill：框線與填色

svg圖形的填色不使用`background`、`border`等CSS屬性  
他要使用專門的定義顏色的系統

```pug
svg(viewbox="0 0 100 100" width="300" height="300")
 rect(x=40 y=40 width=20 height=20 stroke="skyblue" fill="aliceblue")
```
![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG/03.png)

這些指定樣式的屬性也可以寫到CSS裡面

```pug
svg(viewbox="0 0 100 100")
 rect(x=40 y=40 width=20 height=20)
```

```sass
svg
 border: 1px solid #000
 width: 300px
 height: 300px
 rect
  stroke: skyblue
  fill: aliceblue
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG/04.png)

上圖將`<svg>`的`width`與`height`、`<rect>`的`stroke`與`fill`都寫到CSS裡了

## 直線

```
line(x1=起始點X座標 y1=起始點Y座標 x2=終結點X座標 y2=終結點Y座標 stroke=線條顏色) 
```

`stroke`不是必備屬性，只是不指定的話就看不到線條了

```pug
svg(viewbox="0 0 100 100" width="300" height="300")
 line(x1=30 y1=50 x2=70 y2=50 stroke="black")
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG/05.png)

## 文字

```
text(x=起始X座標 y=起始Y座標) ★★文字內容★★
```

```pug
svg(viewbox="0 0 100 100" width="300" height="300")
 text(x=50 y=50) 文字
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG/06.png)

## 存成svg檔案

* 確認`width`、`height`有寫在`<svg>`裡面
* `<svg>`加上`xmlns="http://www.w3.org/2000/svg"`，指定xml檔案類型為svg

```html
<svg xmlns="http://www.w3.org/2000/svg" width="300" height="300" viewbox="0 0 100 100">
	<circle cx="50" cy="50" r="10"></circle>
</svg>
```