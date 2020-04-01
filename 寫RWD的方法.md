# 寫RWD的方法

## RWD寬度範例

`max-width`的指定值為包含  
該當寬度與該當寬度以下的裝置，都會套用到RWD的CSS內容

```sass
@media (max-width: 768px)
 body
  background: pink
```

* 寬度767px：粉紅色背景（手機版）
* 寬度768px：粉紅色背景（手機版）
* 寬度769px：白色背景（電腦版）

## 圖片RWD

圖片也能透過`<picture>`與`<source>`做到當大螢幕時讀A圖，小螢幕時讀B圖的效果

```pug
picture
 source(media="(max-width: 480px)" srcset="手機版的圖.png")
 img(src="電腦版的圖.png" width="100%")
```

不論在電腦版，或是手機版，畫面都會顯示出<img>，並且一樣繼承width="100%"的參數
只是，當他變成手機版時（依照上例的設定，當寬度等於或小於480px時），<img>的src會作切換，切換成source所定義的「手機版的圖.png」的位置