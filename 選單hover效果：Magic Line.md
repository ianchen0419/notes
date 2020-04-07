# 選單hover效果：Magic Line

## 效果說明

這是一個選單的hover特效，本來底線會放在現在訪問的那一頁的選單項目之下，當滑鼠碰到某個其他項目時，那條底線就會滑過去

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/選單hover效果：Magic%20Line/01.gif)

## 做法詳解

首先，做一個簡單的頁首選單

```pug
header
 a.logo(href="javascript") LOGO
 nav
  a(href="javascript").visited 首頁
  a(href="javascript") 服務項目
  a(href="javascript") 產品一覽
  a(href="javascript") 關於我們
  a(href="javascript") 聯絡表單
  #line
```

這裡假定現在造訪的位置在「首頁」，所以給「首頁」掛了一個`.visited`  
並且可以看到，提示的線不是一個固定的`border`，他是一個叫做`#line`的元素，要假裝成`border`掛在底下而已  
之後會隨著JS設定而飄來飄去

```sass
header
 display: flex
 justify-content: space-between
 padding: 0 20px
 background: #333
 border-radius: 4px

a
 text-decoration: none
 color: #fff
 padding: 20px 0

nav
 position: relative
 
nav *
 margin: 0 10px
 display: inline-block

#line
 margin: 0
 position: absolute
 height: 2px
 background: #fff
 bottom: 10px
 left: 0
 width: 32px
 transition-duration: 0.3s
 border-radius: 2px
```

## JS詳解⑴ 抓取`visited`的固定位置

現在我們還沒法看到魔法底線，所以先讓他顯示出來  
注意假如造訪了首頁，底線會出現在「首頁」底下  
但如果又造訪了關於我們，底線會出現在「關於我們底下」    

所以底線的長度與位置都不能用CSS寫死，必須用JS動態設定才行

```javascript
const visitedMenu=document.querySelector('.visited');
const allMenu=document.querySelectorAll('nav a');
const nav=document.querySelector('nav');

line.style.width=`${visitedMenu.clientWidth}px`;
line.style.left=`${visitedMenu.offsetLeft}px`;
```

這裡使用`clientWidth`抓取寬度，`offsetLeft`抓取該選單項目與左邊邊界的距離  
注意由於`<a>`預設的`display: inline`之下，回傳的`clientWidth`會為`0`  
（畢竟`inline`元素有寬度也是件奇怪的事情）  
所以必須將`<a>`改成`display: inline-block`

## JS詳解⑵ 動態抓到每個hover的位置

接著，來實作當滑鼠滑到別的選單項目時，底線移動（與改變長度）的效果  
因為JS沒有`hover`這個事件，所以改成用`mouseover`來實作滑鼠移入    

我們在原本的JS程式碼下方加入這段：

```javascript
allMenu.forEach(item => item.onmouseover=function(){
 line.style.width=`${this.clientWidth}px`;
 line.style.left=`${this.offsetLeft}px`;
})
```

這時我們的小白線就能隨著滑鼠位置而動來動去了  
不過，本範例中的`visited`位置在首頁，我今天滑到了「關於我們」後  
小白線就直接停留在「關於我們」下面了，不會回到「首頁」下面  
這樣邏輯不通，所以要在補寫一個`mouseout`事件，讓他在滑來滑去結束後  
回到原本`visited`的位置

```javascript
nav.onmouseout=function(){
 line.style.width=`${visitedMenu.clientWidth}px`;
 line.style.left=`${visitedMenu.offsetLeft}px`;
}
```

這裡雖然直覺上會想要把`mouseout`事件掛在`allMenu`上  
但看倌們仔細想想，我們這些選單項目`<a>`都有設定`margin`啥的  
滑鼠非常容易就滑出去`<a>`，然後小白線就會像中風一樣一直想要回到`visited`的位置  
因此，本例將此還原事件掛在更為全面的`<nav>`上面，以防小白線動得太靈敏了

## JS詳解⑶ 函式化整理程式碼

到此為止，功能已經做好了  
只是看看我們亂七八糟的JS程式碼

```javascript
const visitedMenu=document.querySelector('.visited');
const allMenu=document.querySelectorAll('nav a');
const nav=document.querySelector('nav');

line.style.width=`${visitedMenu.clientWidth}px`;
line.style.left=`${visitedMenu.offsetLeft}px`;

allMenu.forEach(item => item.onmouseover=function(){
 line.style.width=`${this.clientWidth}px`;
 line.style.left=`${this.offsetLeft}px`
})

nav.onmouseout=function(){
 line.style.width=`${visitedMenu.clientWidth}px`;
 line.style.left=`${visitedMenu.offsetLeft}px`;
}
```

可以看到很多`line.style....`的東西一直在重複  
這裡也是可以做簡化的，我們再把它寫成進階的函式整理成以下

```javascript
const visitedMenu=document.querySelector('.visited');
const allMenu=document.querySelectorAll('nav a');
const nav=document.querySelector('nav');

function lineMove(target){
 line.style.width=`${target.clientWidth}px`;
 line.style.left=`${target.offsetLeft}px`
}

// line.style.width=`${visitedMenu.clientWidth}px`;
// line.style.left=`${visitedMenu.offsetLeft}px`;
lineMove(visitedMenu);

allMenu.forEach(item => item.onmouseover=function(){
 // line.style.width=`${this.clientWidth}px`;
 // line.style.left=`${this.offsetLeft}px`
 lineMove(this);
})

nav.onmouseout=function(){
 // line.style.width=`${visitedMenu.clientWidth}px`;
 // line.style.left=`${visitedMenu.offsetLeft}px`;
 lineMove(visitedMenu);
}
```

簡化後，不到20行JS就能搞定！

參考資料：[https://css-tricks.com/jquery-magicline-navigation/](https://css-tricks.com/jquery-magicline-navigation/)
