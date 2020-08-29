多选框

主要方法：

```
//多个选项框是否在同一行
public function inline($val = true)

//【全选】按钮文字，若传入空字符串，则不显示此按钮
public function checkallBtn($val = '全选')

//选项,传入数组　如 [1=>'男',　2=>'女'];
public function options($options)

//传入查询结果集
public function optionsData($optionsData, $textField = '', $idField = 'id')

//在现有选项【前面】加入选项
public function beforOptions($options)

//在现有选项【后面】加入选项
public function afterOptions($options)

//与现有选项合并，会重排数组键
public function mergeOptions($options)
```
