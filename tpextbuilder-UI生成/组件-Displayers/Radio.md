单选框


主要方法：

```
//多个选项框是否在同一行
public function inline($val = true)

//以块状显示，一种美化
public function blockStyle($val = true)
```

`HasOptions`　trait 为`Checkbox` `Radio` `Select` `DualListbox` `MultipleSelect` `Match` `Matches` 共有。

### 颜色主题
`$form->radio('on_sale', '上架')->class('radio-warning')->blockStyle()->options([1 => '已上架', 0 => '未上架'])->default(0);`
primary（主色）
success（成功）
secondary（灰色）
info（一般信息）
warning（警告）
danger（警告）
dark（黑色）
purple（紫色）
pink（粉红色）
cyan（青色）
yellow（黄色）
brown（棕色）