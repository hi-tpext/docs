所有`displayer`的基类。

直接输出value(支持html),一般不直接使用。

`form`中使用：无label, 不支持col-md-大小控制。

`table`中使用，和`show`类似。

`table`中使用`fields`里面使用`show`和`field`有略微差别。`show`有div包裹着，是块级元素，`field`是行内元素。


```php
        $table->fields('consignee', '收货人/电话')->with(
            $table->show('consignee', '收货人'),
            $table->show('mobile', '电话')->default('--')
        );
        
```
显示：

```html
   小明 
13612345678
```

```php
        $table->fields('consignee', '收货人/电话')->with(
            $table->field('consignee', '收货人'),
            $table->field('mobile', '电话')->default('--')
        );
```
显示：

```html
小明13612345678
```
|  表头   | 表头  |
|  ----  | ----  |
| 单元\n格  | 单元格 |
| 单元格  | 单元格 |
