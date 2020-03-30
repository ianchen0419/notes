# 不用svg畫圓弧的方法

## 25%、30%、75%圓弧

```pug
.outer
	.sq1
	.sq2
	.inner
		.num 75%
```

```sass
.outer
	width: 150px
	height: 150px
	background: #c1d7ae
	border-radius: 100%
	position: relative
	overflow: hidden

.sq1
	width: 150px
	height: 150px
	position: absolute
	left: 75px
	background-color: #90a955
 
.sq2
	width: 75px
	height: 75px
	position: absolute
	top: 75px
	background-color: #90a955

.inner
	width: 140px
	height: 140px
	border-radius: 100%
	position: absolute
	top: 5px
	left: 5px
	background-color: white

.num
	text-align: center
	line-height: 140px
	font-size: 40px
	font-weight: 300
	color: #6A7152
	display: block
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/不用svg畫圓弧的方法/01.png)

## 上述以外的圓弧（需使用傾斜矩形）

```pug
.outer
	.sq1
	.sq2
	.sq3
	.inner
		.num 90%
```

```sass
.outer
	width: 150px
	height: 150px
	background: #c1d7ae
	border-radius: 100%
	position: relative
	overflow: hidden

.sq1
	width: 150px
	height: 150px
	position: absolute
	left: 75px
	background-color: #90a955
 
.sq2
	width: 75px
	height: 75px
	position: absolute
	top: 75px
	background-color: #90a955

.sq3
	width: 75px
	height: 75px
	position: absolute
	top: 0
	background-color: #90a955
	transform: skewX(-36deg)
	transform-origin: bottom

.inner
	width: 140px
	height: 140px
	border-radius: 100%
	position: absolute
	top: 5px
	left: 5px
	background-color: white

.num
	text-align: center
	line-height: 140px
	font-size: 40px
	font-weight: 300
	color: #6A7152
	display: block
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/不用svg畫圓弧的方法/02.png)

## 傾斜角度分析

```sass
transform: skewX(-36deg)
transform-origin: bottom
```

`skewX`角度的算法：    

完全傾斜至水平為`skewX(-90deg)`，此時圓弧為75%的狀態  
完全不傾斜為`skewX(0deg)`，此時圓弧為100%

```
-90deg:0deg = 75%:100%
-3.6deg = 1%
```

換算出`1%`等於`-3.6deg`

| 圓弧比例 | 角度          |
| ------ | ---------     |
| 100%圓弧| skew(0deg)    |
| 99%圓弧 | skew(-3.6deg) |
| 98%圓弧 | skew(-7.2deg) |
| 97%圓弧 | skew(-10.8deg)|
| 96%圓弧 | skew(-14.4deg)|

如上表，換算出本範例的90%圓弧為`skew(-36deg)`

## 會動的圓弧

本範例使用的方法不能讓圓弧動起來，必須改用SVG stroke的方式才能讓他會動
