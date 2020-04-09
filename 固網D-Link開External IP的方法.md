# 固網D-Link開External IP的方法

## 條件限制

* 只能透過固網設定，行動網路因為會透過一層路由，所以沒法直接對外開放
* 只能開`localhost:80`的內容，沒法開像是`localhost:8080`、`localhost:8000`這樣複雜的`port`<br>所以如果網站的`port`不是`80`的話，要先改成`80`

## 外部IP的功能

外部IP可以把自己這台電腦當作主機發佈給網際網路  
所以網際網路上的任何人都能讀取自己電腦的`localhost`內容

### 步驟⑴ 設定固定IP

當電腦存取網路時，網路機器（有線網路 or WiFi）會給予該電腦一個IP  
如果有另一台電腦也連上同一個網路，網路機器會在給那台電腦另一個IP    

在未特別設定的情況下，IP會隨著每次接到網路時，而有不同的值  
這時可以透過固定IP設定，強制佔用某個IP，讓該電腦每次連網時都使用同一個IP  

### 查看目前的IP

打開系統偏好設定>網路，查看目前的浮動IP

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/固網D-Link開External%20IP的方法/01.png)

記下來目前的IP是`192.168.1.109`  
接著，打開D-Link的設定面板，網址列輸入`192.168.1.1`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/固網D-Link開External%20IP的方法/02.png)

【小提示】DSL-6740C的預設帳號密碼為  
帳號：cht  
密碼：chtvdsl    

點選DCHP Server  
進去後，可以看到EXISTING DCHP CLIENT列著一大排裝置  
（下圖有經過修改所以只能看到一個裝置）  
使用快速鍵`Ctrl`+`F`搜尋`192.168.1.109`（剛剛記起來的IP）  
找到我們現在連的這台裝置

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/固網D-Link開External%20IP的方法/03.png)

然後把IP Address、MAC Address分別填入下方的ADD STATIC IP ADDRESS裡面  
填好後按Apply    

這樣就完成了固定IP設定了，以後`192.168.1.109`這組IP就永遠給該電腦用了

### 步驟⑶ 開啟Virtual Server

上方選單先選ADVANCED，再從側選單選Virtual Server

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/固網D-Link開External%20IP的方法/04.png)

依照上圖設定輸入

|欄位|填值|
|----|---|
|Enable Virtual Server Rules|打勾|
|Name|隨意取名|
|Interface|選`WAN1_2`|
|Internal startport|選`80`|
|Internal endport|選`80`|
|External startport|選`80`|
|External endport|選`80`|
|Protocol Type|選`Both`|

## 大功告成

經過以上設定後，就打開了External Server  
來試試看用External Server開專案吧

### ⑴ 開localhost，設定`port`為`80`

如果是`python`的話，要使用以下指令開啟`localhost`

```
python -m SimpleHTTPServer 80
```

如果是`webpack`的話，要去`package.json`，在`webpack-dev-server`後面加入`port`的描述，改好後重啟他

```
"dev-server": "webpack-dev-server --port 80"
```

如果是`php`的話，因為預設就是`port: 80`了，所以什麼都不用設定

### ⑵ 查看電腦的對外IP

開啟[IP位置查詢網站](http://www.whatismyip.com.tw/)，會看到一組數字為`36.225.60.77`
（每台電腦，每個時間進去看到的IP都不同）

然後用另一台裝置，連不同網路，網址列輸入`36.225.60.77:80`
可以神奇地看到原本應該是`localhost`的東西變成可以對外了

