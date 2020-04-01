# inline-block排滿後會產生的空隙

## 發生狀況

使用`inline-block`排版時，給定的元素寬度加總等於`100%`時會掉下來

```pug
.item1 item1
.item2 item2
```

```sass
div
 border: 1px solid #000
 display: inline-block
 height: 200px
 
.item1
 width: 30%
 
.item2
 width: 70%
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/inline-block排滿後會產生的空隙/01.png)

上述範例中，本來預期元素排成一行  
但item2被擠下來了，所以變成兩行了    

這是因為，由於各種原因，item1跟item2之間有空隙，所以寬度下得太滿時，他們會無法排成一行    

針對這個問題，有兩個做法可以讓他們排成一行

## 方法⑴ 偷改寬度法（爛方法）

只要偷偷地將item2的寬度減個`1%`（或`2%`）他就能排上去了

```sass
div
 border: 1px solid #000
 display: inline-block
 height: 200px
 
.item1
 width: 30%
 
.item2
 width: 68%
```

## 方法⑵ 消除間隙法（認真法）

認真地從各個方面消除排版產生的間隙，讓他們真實地能夠排成一行

### 間隙處① html產生的文字空白

HTML架構中有一種元素叫做`textNode`  
這個textNode不是**畫面上看得到的元素**  
他是開發人員在寫html時，為了程式碼排版美觀，所以在文件上產生的  
**「既沒有被tag包覆，也沒有內容的空白」**

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/inline-block排滿後會產生的空隙/02.png)

如上圖，雖然看似是一份普通的HTML文件  
但橘色虛線框部分跟綠色虛線框部分因為的確存在著排版上的空隙  
所以上圖範例會產生2個`textNode`  
（和一個`elementNode`：`<h1>`）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/inline-block排滿後會產生的空隙/03.png)

消除`textNode`造成的空白間隙影響，有兩個方法。
方法之一是排版時給他連在一起

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/inline-block排滿後會產生的空隙/04.png)

這樣子，就能夠物理上消除`textNode`產生的影響了。  
（或是使用pug等前處理器，也能在編譯時自動幫忙把`textNode`給移走）    

另外一個方法是使用`font-size: 0`（比較常用，因為前一個方法太難讀程式碼了）  
這時，即便存在著`textNode`，但因為顯示的空間都被設定成`0`了，所以畫面上就真正沒有了

```pug
body
 h1 嗨你好，我是標題
```

```sass
body
 font-size: 0

h1
 font-size: 14px
```

回到一開始的兩個item的範例，這時程式碼會變成

```pug
.item1 item1
.item2 item2
```

```sass
div
 border: 1px solid #000
 display: inline-block
 height: 200px
 font-size: 14px
 
.item1
 width: 30%
 
.item2
 width: 70%
 
body
 font-size: 0
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/inline-block排滿後會產生的空隙/05.png)

把`textNode`的影響移除了，但空間還是不夠，item仍舊掉下來了

### 間隙處② `border`（或是`padding`等人）導致的外溢

在預設的`box-sizing: content-box`之下`border`、`padding`這些空間都會往外長  
因為本例用了`border: 1px solid`，這左框+右框×2個item，合計`4px`的空間就導致了空間不足，所以item2就掉下來了    

這時，需要使用`box-sizing: border-box`，將`border`等人的空間設定為往內長

```sass
div
 border: 1px solid #000
 display: inline-block
 height: 200px
 font-size: 14px
 box-sizing: border-box
 
.item1
 width: 30%
 
.item2
 width: 70%
 
body
 font-size: 0
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/inline-block排滿後會產生的空隙/05.png)

經過以上設定後，兩個item終於能排在一起了