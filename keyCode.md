# keyCode

鍵盤上的每個鍵都有自己的識別代碼，稱為`keyCode`  
在實作`key`相關事件時，`keyCode`是不可或缺的情報

## 網頁查詢`keyCode`
![KeyCode Info](http://keycode.info/)

進入上述網站後，隨便按下想要查詢的按鍵，畫面就能顯示出該案件的`keyCode`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/keyCode/01.png)

## JavaScript查詢`keyCode`

```javascript
window.addEventListener("keydown",
 function(e){
  console.log(e.keyCode);
  //console.log(e.which);
 }
);
```

打開網頁，隨便按下一個案件，就能看到開發者工具回傳該案件的`keyCode`代碼
除了`e.keyCode`可以查到代碼外，`e.which`也能夠查到代碼。


