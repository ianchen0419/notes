# Mac安裝php

## 開啟Apache

Mac內建php與Apache，只需要透過一些設定就能建置php開發環境
本指南適用於php版本`5.6.30`

```
sudo apachectl start
```

輸入完指令後，打開瀏覽器`http://localhost`，如果看到「It works!」即代表成功開啟了Apache

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Mac安裝php/01.png)

## 開啟httpd.conf檢視權限

Mac的php文件都放置在`/Library/WebServer/Documents/`之下  
首先進去該路徑，並且在`~/Documents/`底下新增一個資料夾`test/`  
接者在底下新增一個檔案`index.php`，隨意`echo`一些內容  

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Mac安裝php/02.png)

回到瀏覽器，輸入`http://localhost/test`，網頁沒有如預期的出現「hey」的內容，而是出現了「Forbidden」的畫面            

接者用文字編輯器（Sublime），開啟`/etc/apache2/httpd.conf`這個檔案  
搜尋以下字串

```
#LoadModule php5_module libexec/apache2/libphp5.so
```

將最前方的`#`移除，使其成為

```
LoadModule php5_module libexec/apache2/libphp5.so
```

回到`http://localhost/test`，網頁能正常顯示了
※備註：`php 7`的話就是找這段`LoadModule php7_module libexec/apache2/libphp7.so`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Mac安裝php/03.png)

## MySQL與phpMyAdmin

Mac沒有附帶MySQL與phpMyAdmin，所以兩者需要去官網額外下載安裝

## phpMyAdmin連線錯誤的解法

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Mac安裝php/04.png)

Mac作業系統沒辦法用`localhost`當主機名，必須改成用`127.0.0.1`當主機名  
由於phpMyAdmin的config檔案裡預設是寫成連到`localhost`  
所以必須手動進去config檔案，修改成`127.0.0.1`

## config檔案

用文字編輯器（Sublime, VSCode）開啟以下檔案

```
/Library/WebServer/Documents/phpMyAdmin/libraries/config.default.php
```

找到檔案中的這一行

```
$cfg['Servers'][$i]['host'] = 'localhost';
```

並且改成

```
$cfg['Servers'][$i]['host'] = '127.0.0.1';
```

