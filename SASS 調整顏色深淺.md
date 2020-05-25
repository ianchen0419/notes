# SASS 調整顏色深淺

SASS內建的顏色調整參數`lighten/darken`可以快速調整顏色的明度/暗度

```
darken(色碼/色名, 調整%數)
```

## 範例

```pug
h1 這是一段文字
h1.darken 暗沈的文字
h1.lighten 明亮的文字
```

```sass
h1
 color: dodgerblue
 
h1.darken
 color: darken(dodgerblue, 25%)
 
h1.lighten
 color: lighten(dodgerblue, 25%)
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/SASS%20調整顏色深淺/01.png)
