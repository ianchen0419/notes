# PHP與MySQL的資料庫互動

PHP版本：`7.3.11`
MySQL版本：`8.0.18`
執行環境：`Mac OS 10.15.3`

## 資料庫連線 `mysqli_connect()`

|資料名|值|
|----|---|
|網址|`127.0.0.1`|
|登入帳號|`root`（預設）|
|密碼|`zaq1@WSX`|

## 選擇資料庫

選擇`test`資料庫（帶有水庫圖示的就叫做資料庫，資料庫底下的叫做資料表）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/PHP與MySQL的資料庫互動/01.png)

```php
$connect=mysqli_connect('127.0.0.1', 'root', 'zaq1@WSX', 'test');
```

### 檢查是否連線成功

```php
if(!$connect){
	echo '連線失敗';
}else{
	echo '連線成功';
}
```

## 抓取資料與迴圈處理

`test`裡面有一張資料表`mylist`，記載了一些水果的品項與價格

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/PHP與MySQL的資料庫互動/02.png)

### ⑴ 抓取資料`mysqli_query()`，並且存成變數`$re`

`mysqli_query()`要放2個參數，  
第1個是`mysqli_connect`的連線資訊  
第2個放`MySQL`的語法

```php
$re=mysqli_query($connect, 'SELECT * FROM mylist');
```

### ⑵ 回傳資料處理 `mysqli_fetch_array()`

`mysqli_fetch_array()`在沒寫迴圈下只會回傳第一筆符合條件的資料    
所以搭配`while`迴圈，只要條件符合，就會一筆筆將資料丟出來

```php
while($row=mysqli_fetch_array($re)){
	echo $row['name'].'<br/>';
}
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/PHP與MySQL的資料庫互動/03.png)

## 進階：處理完整資料

資料表`mylist`裡面有「水果名」、「序號」、「價格」這3項資訊
更進一步地將所有資料都印出來

```php
$connect=mysqli_connect('127.0.0.1', 'root', 'zaq1@WSX', 'test');
if(!$connect){
	echo '連線失敗';
}else{
	echo '連線成功';
}

echo '<hr>';

echo '<table border="1">';

echo '<caption>水果價目表</caption>';

echo 
	'<thead>
		<tr>
			<th>序號</th>
			<th>水果名</th>
			<th>價格</th>
		</tr>
	</thead>';

echo '<tbody>';

$re=mysqli_query($connect, 'SELECT * FROM mylist');
while($row=mysqli_fetch_array($re)){
	echo '<tr>';

	echo '<td align="center">'.$row['index'].'</td>';
	echo '<td>'.$row['name'].'</td>';
	echo '<td>$'.$row['price'].'元</td>';

}
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/PHP與MySQL的資料庫互動/04.png)


## 動態查詢：`MySQL`指令塞變數

在`mysqli_query()`塞變數`$_GET['name']`，需注意引號`"` / `'`必須要包成以下格式

```
"SELECT * FROM mylist WHERE name='$_GET[name]'"
```

水果店今天要做查價網頁，使用者在網頁輸入水果名，系統回傳價格

```html
<h2>請輸入品項名</h2>
<form action="" method="GET">
	<input type="text" name="name" />
	<input type="submit" name="submit" value="查詢" />
</form>
```

```php
$connect=mysqli_connect('127.0.0.1', 'root', 'zaq1@WSX', 'test');

if(!isset($_GET['submit'])) return;

$re=mysqli_query($connect, "SELECT * FROM mylist WHERE name='$_GET[name]'");
$row=mysqli_fetch_array($re);
if(!$row){
	echo '查無此人';
}else{
	echo '查詢品項：'.$row['name'].'<br>';
	echo '價格：$'.$row['price'].'元';
}
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/PHP與MySQL的資料庫互動/05.gif)

## 總筆數 `mysqli_num_rows()`

`mysqli_num_rows()`會回傳`$result`總共抓了幾筆資料

```php
$connect=mysqli_connect('127.0.0.1', 'root', 'zaq1@WSX', 'test');
$re=mysqli_query($connect, "SELECT * FROM mylist");
$total=mysqli_num_rows($re);
echo '總共有'.$total.'筆資料';
```

## SQL Injection 資料庫隱碼注入攻擊

假設今天是做水果會員網站，用戶可以用水果ID登入，目前一共有4個ID

```html
<h2>請輸入ID登入</h2>
<form action="" method="GET">
	<input type="text" name="id" />
	<input type="submit" name="submit" value="登入" />
</form>
```

```php
$connect=mysqli_connect('127.0.0.1', 'root', 'zaq1@WSX', 'test');

if(!isset($_GET['submit'])) return;

$re=mysqli_query($connect, "SELECT * FROM mylist WHERE name='$_GET[id]'");
$row=mysqli_fetch_array($re);
if(!$row){
	echo '登入失敗';
}else{
	echo '您已經登入'.'<br>';
	echo '您的ID：'.$row['name'].'<br>';
}
```

如果有駭客在前台`<input>`輸入`' OR '1'='1`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/PHP與MySQL的資料庫互動/06.png)

這時，後端的`MySQL`搜尋語法就會變成

```MySQL
SELECT * FROM mylist WHERE name='' OR '1'='1'
```

`'1'='1'`一定會為`true`，所以駭客就能騙過程式，成功登入系統

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/PHP與MySQL的資料庫互動/07.png)

## 隱碼注入對策 `mysqli_escape_string()`

`mysqli_escape_string()`可以讓值變成**不具程式碼效力的普通字串**    
因此建議掛在任何使用者輸入的內容上，以防止被駭客攻擊


```php
$connect=mysqli_connect('127.0.0.1', 'root', 'zaq1@WSX', 'test');

if(!isset($_GET['submit'])) return;

$safe_id=mysqli_escape_string($connect, $_GET['id']);
$re=mysqli_query($connect, "SELECT * FROM mylist WHERE name='$safe_id'");
$row=mysqli_fetch_array($re);
if(!$row){
	echo '登入失敗';
}else{
	echo '您已經登入'.'<br>';
	echo '您的ID：'.$row['name'].'<br>';
}
```
