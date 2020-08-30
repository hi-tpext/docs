数据条目　　

一般用于一对多的数据录入。

主要方法：
```php
//包含多个组件
public function with(...$fields){}

//设置内容组件的值(数组)
public function value($val){}

//条目是否可[删除]
public function cnaDelete($val){}

//条目是否可[添加]
public function canAdd($val){}

//条目只读，不可[删除]或[添加]
public function canNotAddOrDelete(){}

```