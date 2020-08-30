数据条目　　

一般用于一对多的数据录入。

主要方法：
```php
//包含多个组件
public function with(...$fields){}

//设置内容组件的值(数组),同fill,overWrite=true
public function value($val){}

//设置内容组件的值(数组),overWrite是否覆盖
public function fill($data = [], $overWrite = false){}

//条目是否可[删除]
public function cnaDelete($val){}

//条目是否可[添加]
public function canAdd($val){}

//条目只读，不可[删除]或[添加]
public function canNotAddOrDelete(){}

```
### 主要用法
```php
$attrList = $isEdit ? ShopGoodsAttr::where(['goods_id' => $data['id']])->order('sort')->select() : [];

$form->items('attr_list', '产品属性')->dataWithId($attrList)->with(
            $form->text('name', '名称')->placeholder('属性名称，如生产日期')->maxlength(55)->required()->getWrapper()->addStyle('width:200px;'),
            $form->text('sort', '排序')->placeholder('规格名称，如颜色')->default(1)->required()->getWrapper()->addStyle('width:80px;'),
            $form->text('value', '属性值')->required()->getWrapper()->addStyle('min-width:70%;'),
        )->help('【属性】不影响价格，仅展示');
```