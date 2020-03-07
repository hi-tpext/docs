###### 支持的组件：
```php
field($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
text($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
checkbox($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
radio($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
button($type, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
select($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
multipleSelect($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
textarea($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
hidden($name)
color($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
rangeSlider($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
file($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
image($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
date($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
datetime($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
time($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
year($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
month($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
dateRange($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
datetimeRange($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
timeRange($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
number($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
switchBtn($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
rate($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
divider($text, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
password($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
decimal($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
html($html, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
raw($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
show($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
tags($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
icon($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
multipleImage($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
multipleFile($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
wangEditor($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
tinymce($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
ueditor($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
editor($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
ckeditor($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
mdeditor($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
match($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
matches($name, $label = '', $cloSize = 12, $colClass = '', $colAttr = '')
 */
```
###### 参数说明

>$name 字段名称 必填

>$label     显示label ，不填则取name值

>$cloSize   col-md-大小，默认:12

>$colClass  col其他class

>$colAttr   col其他attr

##### 主要通用方法

>class()      设置field的class 

>labelClass() 设置label的class 

>attr()       设置field的class 

>addClass()   添加field的class

>addAttr()    添加field的属性

>addStyle()   添加field的style

>labelAttr()  添加label的属性

>size()       设置大小(label,field)，默认:2,8

>help()       添加帮助信息

>readonly()   只读

>disabled()   禁用

>required()   必填(主要是前端js验证，不涉及后端)

>showLabel()  是否显示label

>default()    默认值

>value()      设置值

>fill()       填充

##### 多选单选

>options()
