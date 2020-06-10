# 原生CSS變數 root

原生的CSS變數，方便又好用，但是IE不能用

```css
:root {
 --green: #11c1a4;
}
```

變數的宣告使用`:root`選擇器，位置在`<html>`這裏

```css
h1 {
 color: var(--green);
}
```

使用變數時要用`var()`括弧包起來

