# 圖層混合模式 mix-blend-mode

`mix-blend-mode`是一個CSS屬性，可以對圖層混合做出一些調整（類似Photoshop），IE不能用。
本篇介紹2個簡單的去背效果   

本次使用的範例圖

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/圖層混合模式%20mix-blend-mode/01.png)

這張圖沒有去背，如果放到有色背景上會變這樣

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/圖層混合模式%20mix-blend-mode/02.png)

## 色彩增值模式 `multiply`

背景色與目標圖片相乘後，成為新的顏色代換掉圖片自己的顏色

* 背景色×目標圖片的`黑色部分`＝**黑色**（原地不動的意思）
* 背景色×目標圖片的`白色部分`＝**背景色**

```pug
.image-outer
 img(src="https://raw.githubusercontent.com/ianchen0419/notes/master/img/圖層混合模式%20mix-blend-mode/01.png")
```

```sass
.image-outer
 background: orange
 display: inline-block
 padding: 40px
 img
  mix-blend-mode: multiply
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/圖層混合模式%20mix-blend-mode/03.png)

原本白色的部分會被背景的橘色吃掉，做了簡單的去背處理  
（但只適用在在圖片只有黑白兩色的情況而已！）

## 濾色模式 `screen`

背景色與目標圖片的補值相乘後，成為新的顏色代換掉圖片自己的顏色
上面的`multiply`會做去背，這次的`screen`則會做去黑

背景色×目標圖片的`黑色部分`＝**背景色**
背景色×目標圖片的`白色部分`＝**白色**（原地不動的意思）

```sass
.image-outer
 background: orange
 display: inline-block
 padding: 40px
 img
  mix-blend-mode: screen
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/圖層混合模式%20mix-blend-mode/04.png)

這次換層黑色的部分被背景的橘色吃掉，達成了去黑效果  
（一樣只適用在在圖片只有黑白兩色的情況而已！）
