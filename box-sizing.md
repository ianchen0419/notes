# box-sizing

## box-sizing: content-box

預設屬性  
框線本身的高度不包含在元素高度內    

假如一個`div`的高度為`100px`，上框線為`2px`，下框線為`2px`  
此`div`的總高度為`100+2+2=104px`    

※因此，容易因為少計算了框線高度導致內元素過大而撐壞版面   

```pug
div content-box
```

```sass
div
 height: 100px
 width: 300px
 border: 2px solid #000
 text-align: center
```
![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/box-sizing/01.png)

```javascript
var mydiv=document.querySelector('div');
console.log(mydiv.offsetHeight); //104
```

【補充】這題抓高度不能用`clientHeight`，因為`clientHeight`不包含`border`高度，所以必須使用`offsetHeight`才能抓到包含`border`的高度

## box-sizing: border-box

框線本身的高度內加於元素高度之中    

假如一個`div`的高度為`100px`，上框線為`2px`，下框線為`2px`.  
此`div`的總高度仍會維持`100px`，`div`內容高度變為`96px`. 
`div`高度會受到擠壓（`-4px`）

```sass
div
 height: 100px
 width: 300px
 border: 2px solid #000
 text-align: center
 box-sizing: border-box
```
![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/box-sizing/02.png)

```javascript
var mydiv=document.querySelector('div');
console.log(mydiv.offsetHeight); //100
```

