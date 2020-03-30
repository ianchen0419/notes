# CSS animation

* 指定`keyframes`，定義動畫動作
* 設定`animation`，定義動畫秒速、次數

```pug
.outer
 .block 上下移動
```

```sass
.outer
 width: 300px
 height: 200px
 border: 1px solid #000
 text-align: center
 position: relative
 display: flex
 justify-content: center
 
.block
 width: 50px
 height: 50px
 border: 1px solid #000
 position: absolute
 bottom: 0
 animation: UpAndDown 2s infinite
 
@keyframes UpAndDown
 0%
  bottom: 0
 50%
  bottom: 100px
 100%
  bottom: 0
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/CSS%20animation/01.png)

## 動畫速度曲線

```sass
animation-timing-function: linear
```
[貝茲曲線換算](https://cubic-bezier.com/#0,1.02,1,-1.17)
