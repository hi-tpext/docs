多个组件组合为一个，多用于排版布局。

有两种写法:
- 1 使用with;
```php
$form->fields('', '基本信息', 7)->with(
    $form->text('name', '名称')->required()->maxlength(55),
    $form->text('spu', 'spu码')->maxlength(100)
    //其他组件以,分割
);
```

- 2 使用fieldsEnd;
```php
$form->fields('', '基本信息', 7);
//写包含的组件
$form->text('name', '名称')->required()->maxlength(55);
$form->text('spu', 'spu码')->maxlength(100);
//其他组件

$form->fieldsEnd();//结束
```