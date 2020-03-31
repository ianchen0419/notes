# SVG animate

稱為SMIL Animation，有別於CSS keyframes、JavaScript Animation，SMIL Animation為第三種前端動畫技巧

## 使用`<animate>`控制

`<animate>`寫在要動的元素之內

* `attributeName`：控制要動的屬性，如半徑`r` 、寬度`width`等等
* `values`：屬性移動的參數，用`;`分割<br>
`attributeName=r values=10;30;10`即表示<br>
動畫0%的時候半徑為`10`<br>
動畫50%的時候半徑為`30`<br>
動畫100%的時候半徑為`10`
* `dur`：動作時間，單位為`s`
* `repeatCount`：重複次數，如果要重複無限次的話則填入`indefinite`

```pug
svg(viewbox="0 0 100 100" width=300 height=300)
 line(x1=30 y1=50 x2=70 y2=50)
 line(x1=50 y1=30 x2=50 y2=70)
 circle(cx=50 cy=50 r=10)
  animate(attributeName="r" values="10;30;10" dur="2s" repeatCount="indefinite")
```

```sass
svg
 border: 1px solid #000
 *
  stroke-width: 3
  stroke: #000
  fill: #fff
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG%20animate/01.png)

## `animateTransform`變形動畫

比起`animate`多了一個`type`屬性，用來指定變形動作例如`rotate`、`scale`、`translate`等等  
`transform`預設的旋轉中心點為元素左上角，所以也跟CSS一樣，需要`transform-origin`來控制旋轉中心點

```pug
svg(viewbox="0 0 100 100" width=300 height=300)
 rect(x=30 y=30 width=40 height=40)
  animateTransform(attributeName="transform" type="rotate" values="0;360" dur="2s" repeatCount="indefinite")
 circle(cx=50 cy=50 r=10)
 line(x1=30 y1=50 x2=70 y2=50)
 line(x1=50 y1=30 x2=50 y2=70) 
```

```sass
svg
 border: 1px solid #000
 rect
  transform-origin: center center
 *
  stroke-width: 3
  stroke: #000
  fill: #fff
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG%20animate/02.png)

## group

使用`g`標籤，將需要群組化的元素都放進去後，再指定動畫，這坨元素都能一起動了  
※使用`g`後，`animate`標籤就放在`g`以下，跟群組內元素平行

```pug
svg(viewbox="0 0 100 100" width=300 height=300)
 g
  rect(x=30 y=30 width=40 height=40)
  circle(cx=50 cy=50 r=10)
  line(x1=30 y1=50 x2=70 y2=50)
  line(x1=50 y1=30 x2=50 y2=70) 
  animateTransform(attributeName="transform" type="rotate" values="0;360" dur="2s" repeatCount="indefinite")
```

```sass
svg
 border: 1px solid #000
 g
  transform-origin: center center
 *
  stroke-width: 3
  stroke: #000
  fill: #fff
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG%20animate/03.png)

## begin

透過`begin`指定開始時間，也可以指定負數，負數的話會在一開始時就直接動

```pug
svg(viewbox="0 0 100 100" width=300 height=300)
 rect(x=0 y=0 width=10 height=70)
  animate(attributeName="height" begin="0s" dur="2s" values="50;100;50" repeatCount="indefinite")
 rect(x=15 y=0 width=10 height=60)
  animate(attributeName="height" begin="-0.3s" dur="2s" values="50;100;50" repeatCount="indefinite")
 rect(x=30 y=0 width=10 height=80)
  animate(attributeName="height" begin="-0.6s" dur="2s" values="50;100;50" repeatCount="indefinite")
 rect(x=45 y=0 width=10 height=90)
  animate(attributeName="height" begin="-0.9s" dur="2s" values="50;100;50" repeatCount="indefinite")
 rect(x=60 y=0 width=10 height=50)
  animate(attributeName="height" begin="-1.2s" dur="2s" values="50;100;50" repeatCount="indefinite")
 rect(x=75 y=0 width=10 height=40)
  animate(attributeName="height" begin="-1.5s" dur="2s" values="50;100;50" repeatCount="indefinite")
 rect(x=90 y=0 width=10 height=30)
  animate(attributeName="height" begin="-1.8s" dur="2s" values="50;100;50" repeatCount="indefinite")
```

```sass
svg
 border: 1px solid #000
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SVG%20animate/04.png)

