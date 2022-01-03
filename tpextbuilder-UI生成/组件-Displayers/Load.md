# 远程加载(单个值)

相当于只读且带ajax的`select`。

数据库表: tp_hobby_type 

| id |name| hoby |
| ---- | ---- | ---- |
| 1  |  唱歌 | sing　 |
| 2  |  跳舞 | dance　 |
| 3  |  爬山 | climb　 |
| 4  |  游泳 | swim　 |

假控制器`/admin/hobytype`实现了下拉选择数据方法`selectPage`，load可以复用此接口

```php
$form->load('hobbies','爱好')->dataUrl(url('/admin/hobytype/selectPage'), 'name')->value(1);
//ajax加载并输出 ：唱歌
```

#### 一般情况下，用户无需主动使用，在form的view[只读]模式中，带ajax的select自动替换为load