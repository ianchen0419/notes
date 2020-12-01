# CSS原生模組化工具 @namespace

## 結論

在HTML架構上`@namespace`只能拆出`html`與`svg`兩種模組（以檔案類別拆），雞肋到等於沒有用。本文探討`@namespace`的設計初衷並解釋為何他在HTML架構上會如此沒用

## CSS模組化

```pug
h1 我是首頁標題
p 我是首頁文字
```

模組化設計的考量重點為確保程式碼的「獨特性」，比如說在用首頁的CSS，因為首頁很多UI元件只會出現在首頁而已，其他頁面不需要用到，也怕其他頁面會不小心混到，所以市面上常見的做法是給`class`特殊前綴，就會變成

```pug
h1.homepage-heading 我是首頁標題
p.homepage-text 我是首頁文字
```

諸如上圖，將首頁的所有特殊樣式`class`都冠上`.homepage-`確保其他頁面在用CSS時不會沾到首頁的東西

## 理想中的namespace

一個完整的`<html>`需要包含`xmlns`宣告，因此會長成這樣  
（HTML5表示：`xmlns`不寫也沒關係）

```html
<html lang="zh-tw" xmlns="http://www.w3.org/1999/xhtml">
```

然後，在`xmlns`宣告中定義`namespace`，取名為`homepage`

```html
<html lang="zh-tw" xmlns:homepage="http://www.w3.org/1999/xhtml">
```

接下來在CSS使用`@namepsace`宣告

```css
@namespace homepage url(http://www.w3.org/1999/xhtml);
homepage|body {
	background: pink !important;
}
```
寫到這裡，我們預期他在首頁時由於吃到`homepage`的命名空間所以套用粉紅色背景，但在其他頁面時保持白色背景

## 實際上的namespace
很遺憾的是，由於HTML不提供`xmlns`的命名空間（可以設定，但等於沒效）  
所以`homepage`有寫等於沒寫，所有頁面的背景也都會套成粉紅色了    

目前`namespace`可以應用的範圍僅侷限在`html`與`svg`的區分而已，但`svg`會寫成共用`class`的人也很少，所以幾乎沒法派上用場

