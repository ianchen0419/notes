# CSS偽元素

## 使用說明

* 透過`:after`或是`:before`指定偽元素
* 指定偽元素後，需要設定`content`屬性才能顯示出來<br>※偽元素不能被JS抓取到<br>※`<img>`、`<br>`等沒有close tag的元素，不能指定偽元素

## content指定固定文字

固定文字用引號包覆

```
content: '固定文字'
```

```pug
div
```

```sass
div
 width: 300px
 height: 200px
 border: 1px solid #000

div:before
 content: '固定文字'
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/CSS偽元素/01.png)

## content指定HTML Attribute

偽元素內容會隨attribute的值而變動

```
content: attr(○○)
```

```pug
.tag1(food="高麗菜" price="100")
.tag2(food="大蒜" price="20")
.tag3(food="玉米" price="300")
```

```sass
div
 width: 300px
 height: 200px
 border: 1px solid #000

div:before
 content: '品項：' attr(food) ' | 價錢：$' attr(price)
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/CSS偽元素/02.png)

