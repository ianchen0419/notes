# php除錯模式display_errors

透過啟用`display_errors`，php會把錯誤噴在網頁上，在開發模式下可以更快速的找出問題

## 檢視目前的`display_errors`狀態

開一個php檔案，並寫下

```php
echo phpinfo();
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/php除錯模式display_errors/01.png)


在網頁中尋找`display_errors`這一項，狀態為`On`表示已開啟噴錯模式，狀態為`Off`代表關閉噴錯模式

## 修改php.ini設定檔

開啟以下檔案（作業系統：Mac）

`/private/etc/php.ini`    

找出`display_errors =`這行，並且依照狀況在等號後面填入`On` / `Off`    

修改後存檔，重啟Apache

