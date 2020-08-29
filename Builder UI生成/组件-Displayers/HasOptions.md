`HasOptions`　trait 为[Checkbox][Radio][Select][MultipleSelect][Match][Matches]共有。
```php
//选项,传入数组　如 [1=>'男',　2=>'女'];
public function options($options){}

//选项,传入数组　如 ['男', '女']
public function texts($texts){}

//传入查询结果集　textField　为表中可作为显示文本的字段
public function optionsData($optionsData, $textField = '', $idField = 'id'){}

//在现有选项【前面】加入选项
public function beforOptions($options){}

//在现有选项【后面】加入选项
public function afterOptions($options){}

//与现有选项合并，会重排数组键
public function mergeOptions($options){}
```
optionsData使用说明：　　

数据库表: tp_gender_type ,模型　\app\cpmmpn\model\GenderType;

| id |name| key |
| ---- | ---- | ---- |
| 1  |  男 | m　 |
| 2  |  女 | f　 |
| 3  |  未知 | n　 |

```php
$genderMocel = new GenderType;
$form->radio('gender','性别')->optionsData($genderMocel::all(), 'name', 'key');
```
```html
<select>
<option vlaue="m">男</option>
<option vlaue="f">女</option>
<option vlaue="n">未知</option>
</select>
```
