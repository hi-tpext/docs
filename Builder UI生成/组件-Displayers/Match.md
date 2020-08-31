匹配

分别相当于只读的`radio`。

```php
$table->match('type', '类型')->options([
    1 => '<label class="label label-success">增加</label>', 
    2 => '<label class="label label-danger">支出</label>'
])->value(1);

//输出 ：增加
```