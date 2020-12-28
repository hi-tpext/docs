`HasOptions`　trait 为`Checkbox` `Radio` `Select` `MultipleSelect` `Match` `Matches` 共有。
```php
//选项,传入数组　如 [1=>'男',　2=>'女'];
public function options($options){}

//键值一样的选项,传入数组　如 ['男', '女']
public function texts($texts){}

//传入查询结果集　textField　为表中可作为显示文本的字段，idField　为表中可作为key的字段
public function optionsData($optionsData, $textField = '', $idField = 'id'){}

/*以下为3个方法为增加/合并选项操作，在上面3个方法设置了选项以后再使用*/

//在现有选项【前面】加入选项
public function beforOptions($options){}

//在现有选项【后面】加入选项
public function afterOptions($options){}

//与现有选项合并，会重排数组键
public function mergeOptions($options){}
```
optionsData使用说明：　　

数据库表: tp_gender_type ,模型　\app\common\model\GenderType;

| id |name| key |
| ---- | ---- | ---- |
| 1  |  男 | m　 |
| 2  |  女 | f　 |
| 3  |  未知 | n　 |

```php
use \app\common\model\GenderType;
```

```php
//指定text/key字段
$form->select('gender','性别')->optionsData(GenderType::select(), 'name', 'key');
```
```html
<select name="gender">
<option vlaue="m">男</option>
<option vlaue="f">女</option>
<option vlaue="n">未知</option>
</select>
```
//指定text，主键id作为key:

```php
$form->select('gender','性别')->optionsData(GenderType::select(), 'name');
```
```html
<select name="gender">
<option vlaue="1">男</option>
<option vlaue="2">女</option>
<option vlaue="3">未知</option>
</select>
```

注意：`optionsData`的驱动表尽量结果集较少的表，对于数据较多的表应使用其他替代方法。

如表单中：
```php
$form->select('type_id','类型')->optionsData(Type::select(), 'name', 'id');//Type表数据较少，可以使用
//$form->select('member_id','会员')->optionsData(Member::select(), 'nicknname', 'id');//不推荐，会员数量很多，全部查询出来不划算
$form->select('member_id','会员')->dataUrl(url('/admin/member/selectPage')); //推荐，使用ajax加载
```

如表格中：
```php
$table->match('type_id','类型')->optionsData(Type::select(), 'name', 'id');//Type表数据较少，可以使用
//$table->match('member_id','会员')->optionsData(Member::select(), 'nicknname', 'id');//不推荐
$table->show('member.nickname','会员')->dataUrl(url('/admin/member/selectPage')); //推荐，关联模型
```