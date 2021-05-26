# With

`with`是`fields`,`items`,`tab`,`step`中的通用方法。

`fields`和`items`如果不使用`with`方法，需要配合`fieldsEnd`、`itemsEnd`结尾。

使用`with`可省略结尾方法(`fieldsEnd、`itemsEnd`)，使代码层次更分明。

`tab`,`step`不需要显式调用`end`方法，但也支持`with`方法。

有3种使用方式：

- 1. 作为可变参数：

`with($field1, $field2, $field3, $fieldN, );`

- 2. 作为数组元素[作为1的折衷方案，可变参数最后跟随一个,号，在低版本php中会报错，放在数组中可避免]

`with([$field1, $field2, $field3, $fieldN, ]);`

- 3. 作为匿名方法中的语句

`with(function($form){$field1;$field2;$field3;$fieldN;});`

以下代码可正常运行，其中仅使用了`tab`、`fields`，`step`、`items`也类似。

```php
$form->tab('tab1')->with(
    function () use ($form) {
        $form->fields('left1', '', 6)->size(0, 12)->showLabel(false)->with(
            function () use ($form) {
                $form->text('name', '名称')->required()->maxlength(55);
                $form->tags('keyword', '关键字');
                $form->textarea('description', '摘要')->maxlength(255);
            }
        );

        $form->fields('right1', '', 6)->size(0, 12)->showLabel(false)->with(
            $form->text('name', '名称')->required()->maxlength(55),
            $form->tags('keyword', '关键字'),
            $form->textarea('description', '摘要')->maxlength(255),//注意最后这个,号在低版本php中会报错，删除或者把fields放在[]中作为一个数组
        );
    }
);

$form->tab('tab2')->with(
    //如果不想使用use($from)，那可以在匿名方法传入参数.
    //并声明类型:\tpext\builder\common\Form(方便代码编辑器提示).
    //最好是在php文件头部引入: use tpext\builder\common\Form; 
    //然后可简写为：function (Form $_form){/* code */}
    //以下代码中 $_form 和 $form 是同一个东西，实际中使用其中一种方式即可。
    function (\tpext\builder\common\Form $_form) use ($form) {
        //left2 start
        $_form->fields('left2', '', 7)->showLabel(false)->size(0, 12);
        $_form->number('stock', '库存')->default(99);
        $form->number('click', '点击量')->default(1);
        $form->number('sales_sum', '销量')->default(0);
        $form->fieldsEnd();
        //left2 end
        //
        $form->fields('right2', '', 5)->size(0, 12)->showLabel(false)->with(
            [
                $_form->text('market_price', '市场价'),
                $form->text('cost_price', '成本价'),
            ]
        );
    }
);
```
