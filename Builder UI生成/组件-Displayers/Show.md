显示内容

跟`Raw`差不多，区别是`Raw`可以显示html,`show`会转义html。

主要方法

```php
//对于较长的内容，切割一部分显示，点击[...]按钮显示全部
public function cut($len = 0, $more = '...'){}

//内容默认是被一个`div`包围的,inline模式就没有外面的`div`。此用法在fields包含多个`show`时有用
public function inline($val){}
```

`table`中使用，和`show`类似。

`table`中使用`fields`里面使用`show`和`field`有略微差别。`show`有div包裹着，是块级元素，`field`是行内元素。


```php
$table->fields('consignee', '收货人/电话')->with(
      $table->show('consignee', '收货人'),
      $table->show('mobile', '电话')->default('--')
);
        
```
显示：
|  收货人/电话   |
|  :----:  |
| 小明<br>13612345678  | 

```php
$table->fields('consignee', '收货人/电话')->with(
     $table->field('consignee', '收货人'),
     $table->field('mobile', '电话')->default('--')
);
```
显示：
|  收货人/电话   |
|  :----:  |
| 小明13612345678  | 