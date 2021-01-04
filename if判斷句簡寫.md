# if判斷句簡寫

* `?` 接**條件成立**時要執行的動作
* `:` 接**條件不成立**時要執行的動作

未簡化的`if`判斷句如下

```javascript
if(1===1){
 console.log('正確');
}else {
 console.log('錯誤');
}
```

簡寫後如下

```javascript
1===1 ? console.log('正確') : ('錯誤')
```