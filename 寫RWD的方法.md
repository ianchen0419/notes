# 寫RWD的方法

## RWD寬度範例

`max-width`的指定值為包含。  
該當寬度與該當寬度以下的裝置，都會套用到RWD的CSS內容

```sass
@media (max-width: 768px)
 body
  background: pink
```

* 寬度`767px`：粉紅色背景（手機版）
* 寬度`768px`：粉紅色背景（手機版）
* 寬度`769px`：白色背景（電腦版）

## 圖片RWD

圖片也能透過`<picture>`與`<source>`做到當大螢幕時讀A圖，小螢幕時讀B圖的效果

```pug
picture
 source(media="(max-width: 480px)" srcset="手機版的圖.png")
 img(src="電腦版的圖.png" width="100%")
```

不論在電腦版，或是手機版，畫面都會顯示出`<img>`，並且一樣繼承`width="100%"`的參數  
只是，當他變成手機版時（依照上例的設定，當寬度等於或小於`480px`時），`<img>`的`src`會作切換，切換成`source`所定義的「**手機版的圖.png**」的位置    

Again，因為`max-width`具備了包含的含義，所以顯示情形如下（以上例為例）    

* 寬度`479px`：手機版的圖.png
* 寬度`480px`：手機版的圖.png
* 寬度`481px`：電腦版的圖.png

## JavaScript與螢幕寬度

在JavaScript實作螢幕寬度的功能，我們需要使用到`innerWidth`這個方法。    

需要注意的一點是，假如今天這份網站的break point統一設定為`768px`好了。  
在`767px`、`768px`時切換為手機版，但在`769px`時切換成電腦版。    

由於media `max-width`的包含的特性，參數會下成

```sass
@media (max-width: 768px)
 body
  background: pink
```

```pug
picture
 source(media="(max-width: 768px)" srcset="手機版的圖.png")
 img(src="電腦版的圖.png" width="100%")
```

但在JavaScript，如果我們也想要使用768px這個參數，if statement需要寫成「小於等於」，也就是「`<=`」

```javascript
if(innerWidth<=768){
　　document.body.style.backgroundColor='pink';
}
```

如此一來，才能與CSS沿用同一個參數，並同樣達成以下效果

* 寬度`767px`：粉紅色背景（手機版）
* 寬度`768px`：粉紅色背景（手機版）
* 寬度`769px`：白色背景（電腦版）

當然，如果搞剛的話，也可以加上`resize`事件，讓畫面一動到尺寸就重新渲染JavaScript。
但基於使用者（基本上）不會亂切尺寸，所以本例就沒有加工了。

