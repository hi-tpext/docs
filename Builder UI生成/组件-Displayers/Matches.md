多个值匹配

HasOptions　trait 为[Checkbox][Radio][Select][MultipleSelect][Match][Matches]共有。


相当于只读的`checkbox`。

```php
$table->match('hobbies', '爱好')->options([
    1 => '唱歌', 
    2 => '跳舞',
    3 => '爬山',
    4 => '游泳'
])->value(2);

//输出 ：女
```

数据库表: tp_gender_type ,模型　\app\common\model\GenderType;

| id |name| key |
| ---- | ---- | ---- |
| 1  |  男 | m　 |
| 2  |  女 | f　 |
| 3  |  未知 | n　 |

```php
//指定text字段
$genderMocel = new GenderType;
$table->match('gender','性别')->optionsData($genderMocel::all(), 'name')->value(3);//默认主键`id`作为key
//输出 ：未知
```

```php
//指定text/key字段
$genderMocel = new GenderType;
$table->match('gender','性别')->optionsData($genderMocel::all(), 'name', 'key')->value('m');
//输出 ：男
```