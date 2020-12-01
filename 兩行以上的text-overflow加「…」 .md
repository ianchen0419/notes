# 兩行以上的text-overflow加「…」

## `text-overflow` 的一般用法

一般來說 `text-overflow` 用在文字只放了一行的情況下，搭配 `white-space: nowrap` 做使用

```pug
.box 本行保留核貸與否、詮釋、裁決及終止本活動辦法之權利。本行保留核貸與否、詮釋、裁決及終止本活動辦法之權利。本行保留核貸與否、詮釋、裁決及終止本活動辦法之權利。本行保留核貸與否、詮釋、裁決及終止本活動辦法之權利。本行保留核貸與否、詮釋、裁決及終止本活動辦法之權利。本行保留核貸與否、詮釋、裁決及終止本活動辦法之權利。
```

```sass
.box
 width: 300px
 border: 1px solid #000
 text-overflow: ellipsis
 overflow: hidden
 white-space: nowrap
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/兩行以上的text-overflow加「…」/01.png)

如此作法，雖然能夠做出超過寬度的文字加「…」效果，但也只能適用於一行的範圍

## 兩行以上的作法

```sass
.box
 width: 300px
 border: 1px solid #000
 display: -webkit-box
 text-overflow: ellipsis
 overflow: hidden
 -webkit-line-clamp: 2
 -webkit-box-orient: vertical
```

更改 `webkit-line-clamp` 的數值，自由調整要顯示的行數

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/兩行以上的text-overflow加「…」/02.png)

## `display: -webkit-box` 的各家瀏覽器相容度
|Chrome	|FireFox|Safari	|IE	|Android|iOS|
|-------|-------|-------|---|-------|---|
|✔︎		|✔︎		|✔︎		|×	|✔︎		|✔︎	|
