所有`displayer`的基类。

直接输出value(支持html)，一般不直接使用。

`form`中使用：无label, 不支持col-md-大小控制。

##### 主要通用方法
|  方法    |  说明    |  备注  | 实例|
| :--: | :--: | :--: |
|class($val)|设置field的class||
|labelClass($val) | 设置label的class ||
|attr($val) | 设置field的属性 ||
|addClass($val) |添加field的class ||
|addAttr($val) |添加field的属性 ||
|addStyle($val) |  添加field的style ||
|labelAttr($val) | 添加label的属性 ||
|size($label, $elemetm) | 设置大小(label,field)|默认: 2, 8|
|help($text) | 添加帮助信息 ||
|readonly($val =true) | 只读 ||
|disabled($val =true) | 禁用 ||
|required($val =true) | 必填(主要是前端js验证，不涉及后端) ||
|showLabel($val =true) | 是否显示label ||
|default($val) | 默认值 ||
|value($val) | 设置值 ||
|to($tpl) | 简单的转换 ||

如 `$table->show('name','姓名')->to('{val}#{mobile}')`  

{val}代表当前字段`name`值,{mobile}为这条记录中的`mobile`字段值。

>mapClassWhen() / mapClassWhenGroup 样式匹配  

如 
```php
$table->match('open', '状态')->options(['0' => '关闭', '1' => '开启'])->mapClassWhen(1, 'hidden');
$table->match('pay_status', '支付状态')->options(['0' => '未支付', '1' => '已支付', '2' =>'已关闭'])->mapClassWhenGroup([[1, 'success'], [2, 'danger']])
`。
```