# 多选框

## 主要方法

```php
//多个选项框是否在同一行
public function inline($val = true)

//【全选】按钮文字，若传入空字符串，则不显示此按钮
public function checkallBtn($val = '全选')

//以块状显示，一种美化
public function blockStyle($val = true)
```

`HasOptions`　trait 为`Checkbox` `Radio` `Select` `DualListbox` `MultipleSelect` `Match` `Matches` 共有。

## 颜色主题

```php
$form->checkbox('attr', '属性')
    ->class('checkbox-warning')//颜色主题
    ->blockStyle()//显示为块状
    ->checkallBtn()//显示[全选]按钮
    ->options(['is_recommend' => '推荐', 'is_hot' => '热门', 'is_top' => '置顶']);
```

`checkbox-warning`，其中[warning]为颜色主题，所有可选主题如下：

- primary（主色）
- success（成功）
- secondary（灰色）
- info（一般信息）
- warning（警告）
- danger（警告）
- dark（黑色）
- purple（紫色）
- pink（粉红色）
- cyan（青色）
- yellow（黄色）
- brown（棕色）
