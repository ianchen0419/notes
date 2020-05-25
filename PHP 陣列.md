# PHP 陣列

## 陣列

建立陣列

```php
$fruits=array('apple', 'banana', 'orange', 'grape');
```

印出整個陣列

```php
print_r($fruits);
```

```
( [0] => apple [1] => banana [2] => orange [3] => grape )
```

印出特定索引值的陣列

```php
print_r($fruits[0]);
```

```
apple
```

## 自訂索引值

PHP的陣列可以自訂索引值，做出類似物件的效果

```
$fruits2=array('name'=>'apple', "price"=>100, 'weight'=>10);
print_r($fruits2['name']);
```

```
apple
```