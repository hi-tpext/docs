# 日期选择　　

## 主要方法

```php
//修改格式，默认为YYYY-MM-DD
public function format($val){}

//时间戳格式化，若value值为时间戳数字格式
public function timespan($val = 'Y-m-d'){}
```

只选择到月份：

```php
$form->date('date', '日期')->format('YYYY-MM');
```

选择到月份，号数固定为1号：

```php
$form->date('date', '日期')->format('YYYY-MM-01');
```
