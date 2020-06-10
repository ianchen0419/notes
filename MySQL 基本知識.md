# MySQL 基本知識

## 資料型別

|參數名稱		|意義			|
|-----------|---------------|
|`text`		|文字			|
|`varchar`	|固定型態的文字	|
|`int`		|整數數字			|
|`bool`		|布林值			|

## phpmyadmin介面操作：建立資料庫與資料表

點選右邊水庫圖示旁的新增後，輸入新資料庫名，編碼選`uf8_unicode_ci`    
（避免某些中文國字出不來）

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/MySQL%20基本知識/01.png)

接者建立資料庫底下的資料表，輸入好資料表名後，按「建立」

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/MySQL%20基本知識/02.png)

建立資料欄位，`AI`代表Automatic Increment，自動累加    
如果資料欄位有索引欄，可以勾選`AI`，他每新增一筆就會給`+1`

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/MySQL%20基本知識/03.png)

## MySQL指令操作

MySQL指令操作可以透過端末終端機，或從`phpmyadmin`的SQL頁籤進入，撰寫指令

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/MySQL%20基本知識/04.png)

### 建立資料表
```MySQL
CREATE TABLE newsheet2(
 ID INT,
 name TEXT,
 price INT,
 weight INT
)
```

### 塞資料進去

在資料表`newsheet`塞一筆資料進去

|欄位		|值		|
|-----------|-------|
|`name`		|apple	|
|`price`	|100	|
|`weight`	|12		|


```MySQL
INSERT INTO newsheet(name, price, weight) VALUES ('apple', 100, 12)
```

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/MySQL%20基本知識/05.png)

### 刪資料

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/MySQL%20基本知識/06.png)

要把`name="badbad"`這筆資料刪掉

```MySQL
DELETE FROM newsheet WHERE name="badbad"
```

### 撈資料

```MySQL
SELECT * FROM newsheet WHERE name="apple"
```

`SELECT`後面接要搜尋的「資料欄位」，`*`代表全部欄位    
`WHERE`後面接搜尋條件，可省略

```MySQL
SELECT * FROM newsheet WHERE name="apple" AND price=100
```

多條件篩選，關鍵字意涵請參考下表

|關鍵字						|意思	|
|---------------------------|-------|
|`AND`						|且		|
|`OR`						|或		|
|`BETWEEN` ★★★ `AND` ☆☆☆	|指定區間	|

### 更新（修改）資料

![](https://raw.githubusercontent.com/ianchen0419/notes/master/img/MySQL%20基本知識/07.png)

要把`banana`的價格改成`500`

```MySQL
UPDATE newsheet SET price=500 WHERE name="banana"
```
