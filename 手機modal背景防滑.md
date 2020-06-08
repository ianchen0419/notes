# 手機modal背景防滑

手機的modal背景防滑一直是個千古難題，在PC裝置適用的`overflow: hidden`在手機上卻不管用。

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/手機modal背景防滑/01.gif)

一般來說主流的作法有幾個

* 禁止`touch`事件（缺點：`modal`如果自帶拉霸也會變得不能滑）
* `modal`外層那塊灰的用`position: fixed`處理（缺點：當同時遇到`<input>`小鍵盤時會衍生手機端的`fixed`靈肉分離問題）
* 紀錄好現在的`scrollTop`參數，只要`body`一滑，就套上那個參數（原地滑動`0`的概念）（缺點：某些機型的手機可以從下方可以往上滑呼叫出小功能面板，那一塊戳久了還是可以拖動背景）
* 手指一碰到背景灰的就關閉`modal`（缺點：`modal`本體戳久了還是可以穿透碰到背景）

上述4個做法都會自帶其他bug，沒一個能夠真正解決到問題。但其實此問題可以透過巧妙的html排法+CSS解決

## HTML排法

```pug
.content-area
 ul
  li 內容內容
  li 內容內容（以下放大概50個li，讓這頁長出拉霸）
```

然後，在`<head>`裡面塞入一個`<meta>`


```html
<meta name="viewport" content="width=device-width">
```

## CSS內容防滑實作

```sass
html
 margin: 0
 height: 100%
 
body
 margin: 0
 height: 100%
 
.content-area
 height: 100%
 overflow: hidden
 -webkit-overflow-scrolling: auto
```

`html`與`body`的`margin: 0`是為了解除原生賦予的外距（他會造成一點點的空間可以滑）。    

精髓是從`html`到`body`，再到`.content-area`的父子三層都套上`height: 100%`
這樣設定後原本在手機端失效的`overflow: hidden`就便有效了（雖然還要搭配`-webkit-overflow-scrolling: auto`使用）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/手機modal背景防滑/02.gif)

經過上述設定後，就成功防止內容被滑動了  
但是，這樣的設定如果手機滑到一半才在中途加`overflow: hidden`那些  
頁面會被強制跳到開頭，沒辦法固定在先前滑到一半的地方

## 固定在先前滑動到的地方

在`.content-area`下面在新增`.content-wrapper`
並且把`overflow: hidden`那些掛在`.content-wrapper`上

```pug
.content-area
 .content-wrapper
  ul
   li 內容內容
   li 內容內容（以下放大概50個li，讓這頁長出拉霸）
```

然後，讓原先長出拉霸的`<body>`取消拉霸（掛上`overflow: hidden`）
將拉霸設定到`.content-wrapper`上面去


```sass
html
 margin: 0
 height: 100%
 
body
 margin: 0
 height: 100%
 overflow: hidden
 
.content-area
 height: 100%
 // overflow: hidden
 // -webkit-overflow-scrolling: auto

.content-wrapper
 height; 100%
 overflow: scroll
 
.no-scroll .content-wrapper
 overflow: hidden
 -webkit-overflow-scrolling: auto
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/手機modal背景防滑/03.gif)
