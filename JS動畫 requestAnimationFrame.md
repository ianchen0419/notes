# JS動畫 requestAnimationFrame

## 前端動畫

* CSS `animation`
* CSS `transition`
* SVG SMIL `<animate>`
* JavaScript `setInterval`
* JavaScript `setTimeout`
* JavaScript `requestAnimationFrame`

`requestAnimationFrame`是一個專門用來處理動態的方法，相對於前5項作法，其用法也相當複雜（但同時也很精細）  
注意他不支援IE9（含）以下

## RAF（略）用法初探

`requestAnimationFrame`的用法跟`setInterval` / `setTimeout`有一點點很像  
這3種動畫函數都是`window`呼叫（並且都能省略`window`）  
塞的第一個值都必須是動作的`function`  
不過，`setInterval` / `setTimeout`都要指定第二個值：「秒數」  
然後RAF不用塞秒數，所以我們只要寫成這樣就好▼

```javascript
window.requestAnimationFrame(function(timestamp){
 console.log(timestamp)
})
```

注意RAF塞進去的**第一個值：函數**的裡面  
我又在塞了一個callback name：`timestamp`  
這個callback name名字隨意取就行，不叫`timestamp`也可以    

這個`timestamp`代表什麼。我們開啟開發者工具看看`console.log(timestamp)`的回傳結果

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/JS動畫%20requestAnimationFrame/01.png)

`timestamp`回傳的結果是「毫秒」    

第一個值`15147.488`毫秒，換算成正常秒數約等於`15`秒。代表我打開這個網頁後，等了大約`15`秒後，我才打開了開發面板，鍵入了`window.requestAnimationFrame(...)`這坨函數    

第二個值`16281.32`毫秒，約等於`16`秒。等於網頁準備好後過了`16`秒，`window.request...(...)`才被執行（所以他跟第一個`console`相距`1`秒）    

但是，實務上執行動畫時不能夠像這樣一直key函數上去，所以需要改寫成循環函數，讓RAF可以不斷地被重複執行

```javascript
function call(timestamp){
 console.log(timestamp);
 window.requestAnimationFrame(call);
}

window.requestAnimationFrame(call);
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/JS動畫%20requestAnimationFrame/02.png)

【補充說明】  
想要抓到RAF的index時，可以這樣做

```javascript
function call(timestamp){
 var idx=window.requestAnimationFrame(call);
 console.log(idx);
}

window.requestAnimationFrame(call);
```

## 實作動態

本次實作利用`rgb`參數調整的方式  
做出動態的變色效果

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/JS動畫%20requestAnimationFrame/03.gif)

* `b`值最小為`0`
* `b`值最大為`255`

### ⑴ 用canvas畫一個圓

```pug
canvas#canvas(width=500 height=500)
```

```sass
canvas
 border: 1px solid #000
 width: 250px
 height: 250px
```

```javascript
var ctx=canvas.getContext('2d');
ctx.beginPath();
ctx.arc(250, 250, 100, 0, 2*Math.PI, false);
ctx.fill();
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/JS動畫%20requestAnimationFrame/04.png)

### ⑵ 加入RAF函數

定義每毫秒`colorIndex`就會跑一次

* 當`colorIndex`加到`255`時，反向遞減
* 當`colorIndex`減到`0`時，又變成遞增

```javascript
var colorIndex=0;
var isPlus=true;

function call(timestamp){
 if(colorIndex==255){
  isPlus=false;
 }
 
 if(colorIndex==0){
  isPlus=true;
 }
 
 if(isPlus==true){
  colorIndex++;
 }else{
  colorIndex--;
 }
 
 ctx.fillStyle=`rgb(0, 150, ${colorIndex})`;
 ctx.fill();
 
 window.requestAnimationFrame(call);
}

window.requestAnimationFrame(call);
```

### ⑶ RAF的停止

停止運作要用到`cancelAnimationFrame`這個方法  
用法如下

```
cancelAnimationFrame(★這裏填入要停下的RAF★)
```

`★要停下的RAF★`可以用變數的方式預先儲存好  
完整範例如下

```pug
canvas#canvas(width=500 height=500)
button(onclick="stopAnimation()") STOP IT
```

```sass
canvas
 border: 1px solid #000
 width: 250px
 height: 250px
```

```javascript
var ctx=canvas.getContext('2d');
ctx.beginPath();
ctx.arc(250, 250, 100, 0, 2*Math.PI, false);
ctx.fill();

var colorIndex=0;
var isPlus=true;
var myAnimation;

function call(timestamp){
 if(colorIndex==250){
  isPlus=false;
 }
 
 if(colorIndex==0){
  isPlus=true;
 }
 
 if(isPlus==true){
  colorIndex++;
 }else{
  colorIndex--;
 }
 
 ctx.fillStyle=`rgb(0, 150, ${colorIndex})`;
 ctx.fill();
 
 myAnimation=window.requestAnimationFrame(call);
}

window.requestAnimationFrame(call);

function stopAnimation(){
 window.cancelAnimationFrame(myAnimation);
}
```







