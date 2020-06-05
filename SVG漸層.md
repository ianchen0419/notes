# SVG漸層

## `<defs`>呼叫`<linearGradient>`

SVG的漸層要先在文件開頭定義`<def>`標籤，並且在裡面設定`<linearGradient>`寫漸層指示
然後再回到CSS用`fill`呼應漸層的`ID`

```pug
svg(viewbox="-50 -50 100 100")
 defs
  linearGradient#mycolor
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 circle(cx=0 cy=0 r=20)
```

```sass
svg
 border: 1px solid #000
 width: 500px
circle
 fill: url(#mycolor)
```

預設的漸層方向是由左至右

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/01.png)

## 漸層方向

預設漸層方向是由左至右，設定漸層方向要在`<linearGradient>`寫參數設定。值填入`0%`～`100%`

* 起點：`x1`、`y1`
* 終點：`x2`、`y2`

### 由左至右（預設值）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/02.png)

```pug
svg(viewbox="-50 -50 100 100" width="500")
 defs
  linearGradient#mycolor(x1="0%" y1="0%" x2="100%" y2="0%")
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 rect(x=-25 y=-25 width=50 height=50 fill="url(#mycolor)")
```

### 由右至左

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/03.png)

```pug
svg(viewbox="-50 -50 100 100" width="500")
 defs
  linearGradient#mycolor(x1="100%" y1="0%" x2="0%" y2="0%")
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 rect(x=-25 y=-25 width=50 height=50 fill="url(#mycolor)")
```

### 由下至上

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/04.png)

```pug
svg(viewbox="-50 -50 100 100" width="500")
 defs
  linearGradient#mycolor(x1="0%" y1="100%" x2="0%" y2="0%")
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 rect(x=-25 y=-25 width=50 height=50 fill="url(#mycolor)")
```

### 由上至下

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/05.png)

```pug
svg(viewbox="-50 -50 100 100" width="500")
 defs
  linearGradient#mycolor(x1="0%" y1="0%" x2="0%" y2="100%")
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 rect(x=-25 y=-25 width=50 height=50 fill="url(#mycolor)")
```
## 漸層渲染方式 `gradientUnits`

`gradientUnits`指定漸層的渲染方式，看是要以該生效物件為區域，在裡面切%畫漸層，還是以整個SVG為區域，整份SVG切%畫漸層，然後再把指定物件框出來

### `objectBoundingBox` （預設值）

`gradientUnits=objectBoundingBox` 只針對生效物件畫

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/06.png)

```pug
svg(viewbox="-50 -50 100 100")
 defs
 
 linearGradient#mycolor(gradientUnits="objectBoundingBox")
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 rect(x=-25 y=-25 width=50 height=50)
```

```sass
svg
 border: 1px solid #000
 width: 500px
rect
 fill: url(#mycolor)
```

### userSpaceOnUse

`gradientUnits=userSpaceOnUse` 針對整份SVG畫，在切出指定元素份的漸層  
※這裡有一個Bug，當在使用`userSpaceOnUse`的時候，SVG的`viewbox`起點一定要從`0,0`開始。不然漸層的位置也會一起偏掉

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/07.png)

```pug
svg(viewbox="0 0 100 100")
 defs
 
 linearGradient#mycolor(gradientUnits="userSpaceOnUse")
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 rect(x=25 y=25 width=50 height=50)
```

```sass
svg
 border: 1px solid #000
 width: 500px
rect
 fill: url(#mycolor)
```

### `<line>`漸層

由於`<line>`不視作一個區域（他不像`<rect>`或`<circle>`可以用`fill`填色）
所以`<line>`不能用好用的`gradientUnits`漸層，只能用`userSpaceOnUse`漸層。所以效果那些就不是那麼一目瞭然

```pug
svg(viewbox="0 0 100 100")
 defs
  linearGradient#mycolor(gradientUnits="userSpaceOnUse")
   stop(offset="5%" stop-color="skyblue")
   stop(offset="80%" stop-color="teal")
 line(x1=25 y1=50 x2=75 y2=50)
```
```sass
svg
 border: 1px solid #000
 width: 500px
line
 stroke: url(#mycolor)
 stroke-width: 3px
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG漸層/08.png)
