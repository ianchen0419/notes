# node版本管理工具

介紹node版本管理工具`n`，可以輕鬆的安裝（或切換）`node`版本  
在切換`node`版本前，可以先透過指令查詢現有的`node`版號

```
node -v
```

回傳值即為現有`node`版號

安裝`n`工具

```
npm install -g n
```

假設今天要新裝`12.0.0`的版本，則執行以下程式碼

```
sudo n 12.0.0
```

因為執行了`sudo`所以要輸入電腦的開機密碼  
執行後，如果電腦裡找不到`12.0.0`這個版，他會幫你重新裝  
但如果電腦之前已經安裝`12.0.0`的話，他會幫你切換到那個版過去

## 尋找已經裝過的版本

可以透過資料夾找出曾經裝過的`node`版本
如果覺得`node`太多版了，也可以直接在資料夾裡面刪除他 以mac為例，`node`版本會放置在

```
/usr/local/n/versions/
```

這個地方不好找，以下說明具體的尋找方式，先開一個Finder出來
![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/node版本管理工具/01.png)

然後，點選上方選單的「前往」，再選「前往檔案夾」
![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/node版本管理工具/02.png)

然後，在檔案夾路徑輸入`/usr/local/n/versions/`
![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/node版本管理工具/03.png)

按下「前往」，就能到達該資料夾了




