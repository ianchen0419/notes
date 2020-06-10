# 定位三劍客：scrollTop、offsetTop、clientTop

## `scrollTop`：滑動多少的距離

```pug
#outer
 #inner
```

```sass
#outer
 height: 500px
 border: 1px solid #000
 overflow-y: scroll
 
#inner
 height: 800px
 background: teal
```

上述範例在滑動到最底時，外層的`#outer`一共是滑動了`300px`，因為`#outer`高度只有`500px`，但內層的`#innter`卻有`800px`，外層不夠的`300px`就會變成滑動的距離。當滑到最底部時，一共滑了`300px`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/定位三劍客：scrollTop、offsetTop、clientTop/01.png)

### 網頁整體的拉霸


若想取得現在整體網頁拉霸滑動到哪裡的位置，可以用以下JS

```javascript
document.documentElement.scrollTop
```

如果用了`document.body.scrollTop`不論滑動到哪裡都會回傳0，所以必須用`documentElement`（實測Chrome/IE/FireFox/Safari）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/定位三劍客：scrollTop、offsetTop、clientTop/02.png)

## `offsetTop`：本體相對於`offsetParent`的距離

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/定位三劍客：scrollTop、offsetTop、clientTop/03.png)

`offsetTop`的指涉的概念大概就像上圖這樣  
`offsetParent`所在的位置可以透過`targetElement.offsetParent`來查詢

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/定位三劍客：scrollTop、offsetTop、clientTop/04.png)

`offsetParent`就是擁有`position: relative`定位的母層元素  
如果我把上圖中的`<article>`的相對定位屬性移除，`offsetParent`會再找到更上面擁有相對定位的母層  
如果把上面所有相對定位都掃掉，`offsetParent`就會回傳`<body>  `  

※例外：當目標元素為`position: fixed`時，由於他是相對於視窗做定位，不存在什麼絕對母層，所以他的`offsetParent`會回傳null    

`padding` / `border` 會不會影響到`offsetTop`呢？  
由於`padding` / `border` 都是屬於上圖咖啡色方塊的目標元素之中  
所以他們不會影響到`offsetTop`

## `clientTop`：簡單來說就是`border-top`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/定位三劍客：scrollTop、offsetTop、clientTop/05.png)

但其實`clientTop`指涉的不是`border-top`，他是指元素外層與內層之間的距離。
如果把OS設定為阿拉伯文 / 希伯來文這種拉霸在左邊的語言，就可以看出端倪

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/定位三劍客：scrollTop、offsetTop、clientTop/06.png)

這時的`clientLeft`會加上拉霸的`15px`，所以總和值為`50px`+`15px`=`65px`

## 參考資料
![要素サイズとスクローリング](https://ja.javascript.info/size-and-scroll)

