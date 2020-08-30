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
布局：左边`col-md-7` + 右边`col-md-5`　　
```php
$form->fields('', '', 7)->size(0, 12)->showLabel(false);
$form->text('name', '名称')->required()->maxlength(55);
$form->text('spu', 'spu码')->maxlength(100);
$form->tags('keyword', '关键字')->maxlength(255);
$form->textarea('description', '摘要')->maxlength(255);
$form->wangEditor('content', '产品详情')->required();
$form->fieldsEnd();

$form->fields('', '', 5)->size(0, 12)->showLabel(false);
$form->image('logo', '封面图')->required()->mediumSize();
$form->text('market_sale', '市场价', 4);
$form->text('cost_price', '成本价', 4);
$form->number('sort', '排序')->default(0);
$form->number('weight', '重量')->default(1000)->help('单位:克');
$form->fieldsEnd();
```
