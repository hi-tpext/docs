匹配

HasOptions　trait 为[Checkbox][Radio][Select][MultipleSelect][Match][Matches]共有。

分别相当于只读的`radio`。

```php
$table->match('type', '类型')->options([
    1 => '<label class="label label-success">增加</label>', 
    2 => '<label class="label label-danger">支出</label>'
])->value(1);

//输出 ：增加
```

```php
$table->match('type', '类型')->options([
    1 => '男', 
    2 => '女',
    3 => '未知'
])->value(2);

//输出 ：女
```