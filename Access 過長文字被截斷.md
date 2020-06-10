# Access 過長文字被截斷

用Microsoft Access開啟`.csv`文件的時候，如果有欄位內容文字太長超過`255`個字，載入Access後他會幫你自動消除`255`字以後的字元，導致內容缺失

## 將資料類型改成「長文字」

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/Access%20過長文字被截斷/01.png)

匯入`.csv`檔案後的設定畫面，按下左下角的「進階」，彈出匯入規格的小視窗  
在欄位資訊的資料類型選「長文字」    

這樣，他就能編出`255`字以後的內容了