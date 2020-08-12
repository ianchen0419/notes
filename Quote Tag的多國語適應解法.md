# Quote Tag的多國語適應解法

`<q>` 是 CSS `2.1` 標準的古早標籤，本意是用來提示引言（與多語系客製化），同時也能活用他客制接頭詞、接尾詞的特性，解決多國語常見的空格問題

## 多國語的空格問題

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Quote%20Tag的多國語適應解法/01.png)

這是常見的紅字強調排版，通常會這樣處理

```html
<p>
  我是一段字，而且想要<span class="txt-red">強調</span>某些內容
</p>
```

```sass
.txt-red
 color: red
```

這樣做在方塊字體系中沒什麼問題（中文、日文、韓文等），但在以空格區別單字的字母體系中（如英文、德文）就會發生以下事故

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Quote%20Tag的多國語適應解法/02.png)

看官可以看到紅色的字跟前後文連在一起的事故發生了（汗）

## 神奇的`<q>`標籤

讓我們用神奇`<q>`改寫一次這個範例

```html
<p>
  我是一段字，而且想要<q class="txt-red">強調</q>某些內容
</p>
```
`<q>`在沒定義`quote`時會給出蝌蚪上下引號`“`/ `”`框住內容，但這題不需要蝌蚪引號所以我們給他拿掉


```sass
q
 quotes: '' ''
```

然後，在英語的環境下則需要用上下各一個半形空白框住紅色字  
為了區別語系差異所以加上`lang`選取器

```html
<p lang="zh-TW">
  我是一段字，而且想要<q class="txt-red">強調</q>某些內容
</p>
<p lang="en-US">
 I am a paragraph and want to<q class="txt-red">emphasize</q>something
</p>
```

```sass
.txt-red
 color: red
 
q
 &:lang(zh-TW)
  quotes: '' ''
 &:lang(en-US)
  quotes: ' ' ' '
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Quote%20Tag的多國語適應解法/03.png)

實務上多語系的切換往往是一頁一頁換，所以`lang`通常都會掛在最上層的`<html>`然後讓他一層一層繼承下去（CSS這樣一樣可以選到）

```
<html lang="zh-TW">
```
