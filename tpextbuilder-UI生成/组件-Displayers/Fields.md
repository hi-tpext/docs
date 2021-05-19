
# Fields

## 多字段组合　　

多个组件组合为一个，多用于排版布局。

主要方法：

```php
//with 包含多个其他组件
public function with(...$fields){}

//设置　内部组件的值(数组)　同: fill,overWrite=ture
public function value($val){}

//设置　内部组件的值(数组)，overWrite是否覆盖.
public function fill($data = [], $overWrite = false){}
```

### with用法

有4种写法:

- 1. 使用with可变参数(...fields);

```php
$form->fields('', '基本信息', 7)->with(
    $form->text('name', '名称')->required()->maxlength(55),
    $form->text('spu', 'spu码')->maxlength(100)
    //其他组件以,分割
);
```

- 2. 使用with包含数组中的fields;

```php
$form->fields('', '基本信息', 7)->with([
    $form->text('name', '名称')->required()->maxlength(55),
    $form->text('spu', 'spu码')->maxlength(100)
    //其他组件以,分割
 ]
);
```

- 3. [版本>=1.9.0010]使用with匿名方法;
  
```php
$form->fields('', '基本信息', 7)->with(
    function() use($from){
        $form->text('name', '名称')->required()->maxlength(55);
        $form->text('spu', 'spu码')->maxlength(100;
        //其他组件以
    }
);
//或者
$form->fields('', '基本信息', 7)->with(
    function(\tpext\builder\common\Form $from){
        $form->text('name', '名称')->required()->maxlength(55);
        $form->text('spu', 'spu码')->maxlength(100;
        //其他组件以
    }
);
```

- 4. 使用[fieldsEnd]收尾;

```php
$form->fields('', '基本信息', 7);
//写包含的组件
$form->text('name', '名称')->required()->maxlength(55);
$form->text('spu', 'spu码')->maxlength(100);
//其他组件

$form->fieldsEnd();//结束
```

### 主要功能

- 1. : 页面布局，左边`col-md-7` + 右边`col-md-5`,把页码整体做一个基本的划分。　　

```php
$form->fields('left', '', 7)->size(0, 12)->showLabel(false);
$form->text('name', '名称')->required()->maxlength(55);
$form->text('spu', 'spu码')->maxlength(100);
$form->tags('keyword', '关键字')->maxlength(255);
$form->textarea('description', '摘要')->maxlength(255);
$form->wangEditor('content', '产品详情')->required();
$form->fieldsEnd();

$form->fields('right', '', 5)->size(0, 12)->showLabel(false);
$form->image('logo', '封面图')->required()->mediumSize();
$form->text('market_sale', '市场价', 4);
$form->text('cost_price', '成本价', 4);
$form->number('sort', '排序')->default(0);
$form->number('weight', '重量')->default(1000)->help('单位:克');
$form->fieldsEnd();
```

也可使用3个针对[fields]个语法糖：`left`,`middle`,`right`。

`$form->left(string $size[, Closure $call]);`
`$form->middle(string $size[, Closure $call]);`
`$form->right(string $size[, Closure $call]);`

如：把表单分为左右两部分，每边各占一半[col-md-6]:

```php
$form->left(6, function () use ($form) {
    $form->text('name', '名称')->required()->maxlength(55);
    $form->select('category_id', '分类')->required()->dataUrl(url('/admin/shopcategory/selectPage'));
    $form->select('brand_id', '品牌')->dataUrl(url('/admin/shopbrand/selectPage'));
    $form->select('admin_group_id', '商家')->dataUrl(url('/admin/group/selectPage'));
});

// 同理，如果不想使用use($form)，可以在方法传参并声明类型
// $form->left(6, function (\tpext\builder\common\Form $from) {
//     $form->text('name', '名称')->required()->maxlength(55);
//     $form->select('category_id', '分类')->required()->dataUrl(url('/admin/shopcategory/selectPage'));
//     $form->select('brand_id', '品牌')->dataUrl(url('/admin/shopbrand/selectPage'));
//     $form->select('admin_group_id', '商家')->dataUrl(url('/admin/group/selectPage'));
// });

//右边，这里演示另外一种形式，如果第二个方法不传入匿名方法，可以继续调用with方法再传入字段，with方法的用法和fields的with方法一致。
$form->right(6)->with(
    $form->image('logo', '封面图')->required()->mediumSize(),
    $form->text('share_commission', '分销佣金')->default(0),
    $form->text('market_price', '市场价', 4),
    $form->text('cost_price', '成本价', 4)
);
```

- 2. : 把一些相关的字段组合到一起.

```php
$form->fields('省/市/区');
$form->select('province', ' ', 4)->size(0, 12)->showLabel(false)->dataUrl(url('api/areacity/province'), 'ext_name')->withNext(
     $form->select('city', ' ', 4)->size(0, 12)->showLabel(false)->dataUrl(url('api/areacity/city'), 'ext_name')->withNext(
          $form->select('area', ' ', 4)->size(0, 12)->showLabel(false)->dataUrl(url('api/areacity/area'), 'ext_name'))
);
$form->fieldsEnd();

```
- 功能3 : `table`中使用，把相关字段合并到同一列，避免字段过多时表格显示不便。

```php
$table->fields('consignee', '收货人/电话')->with(
     $table->show('consignee', '收货人'),
     $table->show('mobile', '电话')->default('--')
);

$table->show('pay_money', '支付金额');

$table->fields('pay_status', '支付状态/时间')->with(
     $table->match('pay_status', '支付状态')->options(OrderModel::$pay_status_types),
     $table->show('pay_time', '支付时间')->default('--')
);
```

显示：
|  收货人/电话   |　支付金额 | 支付状态/时间 |
|  :----:  |   :----:  | :----:  |
| 小明<br>13612345678  | 100.00 | 已支付<br>2020-08-29 12:31:24 |

ps : `table`中使用 `fields`组合多个字段时，表头只显示`fields`的label，但里面的各个字段还是需要单独设置其label，因为导出数据时，字段是分开的。