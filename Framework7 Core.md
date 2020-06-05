# Framework7 Core

Framework7是手機特化型的一套框架，他排除了一些在開發手機時常踩到的雷，比如popup開啟時背景防止滑動、輸入框點選時小鍵盤會蓋到輸入框自己、`fixed`元素過多時在輸入框操作會有視差位移的大bug

## 如何使用

Framework7 Core是以Vanilla JS為環境的套件，所以不需要使用React / Vue，本介紹連Webpack也不包，只描述簡單引入的方法

```
.
├── index.html (首頁)
├── pages
│   ├── news.html (最新消息)
│   └── about.html (關於我們)
├── app.js (Framework7設定檔)
├── router.js (路徑設定檔)
└── style.css (自訂的CSS)
```

範例網頁的架構有三頁

```
首頁 (index.html)
  ├── 最新消息 (news.html)
  └── 關於我們 (about.html)
```

Framework7最難的地方就是設換頁路徑（因為他是SPA）  
這邊先留意起來

## 換頁設定

參考[官網教學](https://framework7.io/docs/app-layout.html)，建立`index.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Required meta tags-->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no, minimal-ui, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <!-- Color theme for statusbar (Android only) -->
    <meta name="theme-color" content="#2196f3">
    <!-- Your app title -->
    <title>My App</title>
    <!-- Path to Framework7 Library Bundle CSS -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/framework7/5.7.5/css/framework7.bundle.css">
    <!-- Path to your custom app styles-->
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <!-- App root element -->
    <div id="app">

      <!-- Your main view, should have "view-main" class -->
      <div class="view view-main">
        <!-- Initial Page, "data-name" contains page name -->
        <div data-name="home" class="page">

          <!-- Top Navbar -->
          <div class="navbar">
            <div class="navbar-bg"></div>
            <div class="navbar-inner">
              <div class="title">我是首頁</div>
            </div>
          </div>

          <!-- Bottom Toolbar -->
          <div class="toolbar toolbar-bottom">
            <div class="toolbar-inner">
              <!-- Toolbar links -->
              <a href="/news/" class="link">最新消息</a>
              <a href="/about/" class="link">關於我們</a>
            </div>
          </div>

          <!-- Scrollable page content -->
          <div class="page-content">
            <p>你好我是首頁</p>
          </div>
        </div>
      </div>
    </div>
    <!-- Path to Framework7 Library Bundle JS-->
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/framework7/5.7.5/js/framework7.bundle.js"></script>
    <script type="text/javascript" src="routes.js"></script>
    <!-- Path to your app js-->
    <script type="text/javascript" src="app.js"></script>
  </body>
</html>
```


在Framework7裡面，換頁的路徑都要設定在`app.js`（或在本範例中額外拆出來放在`route.js`）

### `app.js`

```javascript
var app = new Framework7({
	// App root element
	root: '#app',
	// App Name
	name: 'My App',
	// App id
	id: 'com.myapp.test',
	// Enable swipe panel
	theme: 'ios',
	// Add default routes
	routes: routes,
});

var mainView = app.views.create('.view-main');
```

`theme`可以填入`ios`、`md`、`aurora`三種參數，建議填入不然他樣式在手機/電腦會長不一樣


### `router.js`

```javascript
var routes=[
	{
		//最新消息
		path: '/news/',
		url: 'pages/news.html',
		options: {
			transition: 'f7-parallax',
		},
	},
	{
		//關於我們
		path: '/about/',
		url: 'pages/about.html',
		options: {
			transition: 'f7-parallax',
		},
	},
]
```

換頁的動態寫在`options`裡面的`transition`，可提供的參數可以參考[官網範例](https://framework7.io/kitchen-sink/core/?theme=ios)的Page Transitions這頁

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Framework7%20Core/01.png)

### 最新消息 `news.html`

除了`index.html`以外的頁面html，只要放`<div class="page">`的內容就好


```html
<div data-name="news" class="page">

	<!-- Top Navbar -->
	<div class="navbar">
		<div class="navbar-bg"></div>
		<div class="navbar-inner">
			<div class="title">最新消息</div>
		</div>
	</div>

	<!-- Scrollable page content -->
	<div class="page-content">
		<p>Coming Soon...</p>
	</div>
</div>
```

### 關於我們 `about.html`

```html
<div data-name="about" class="page">

	<!-- Top Navbar -->
	<div class="navbar">
		<div class="navbar-bg"></div>
		<div class="navbar-inner">
			<div class="title">關於我們</div>
		</div>
	</div>

	<!-- Scrollable page content -->
	<div class="page-content">
		<p>本公司創立於西元100年</p>
	</div>
</div>
```

## 換頁demo

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Framework7%20Core/02.gif)



