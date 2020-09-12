###### 支持的组件：
```php
/**
 * Methods.
 *
 * Field          field($name, $label = '', $colSize = 12)
 * Text           text($name, $label = '', $colSize = 12)
 * Checkbox       checkbox($name, $label = '', $colSize = 12)
 * Radio          radio($name, $label = '', $colSize = 12)
 * Button         button($type, $label = '', $colSize = 12)
 * Select         select($name, $label = '', $colSize = 12)
 * MultipleSelect multipleSelect($name, $label = '', $colSize = 12)
 * Textarea       textarea($name, $label = '', $colSize = 12)
 * Hidden         hidden($name)
 * Color          color($name, $label = '', $colSize = 12)
 * RangeSlider    rangeSlider($name, $label = '', $colSize = 12)
 * File           file($name, $label = '', $colSize = 12)
 * Image          image($name, $label = '', $colSize = 12)
 * Date           date($name, $label = '', $colSize = 12)
 * Datetime       datetime($name, $label = '', $colSize = 12)
 * Time           time($name, $label = '', $colSize = 12)
 * Year           year($name, $label = '', $colSize = 12)
 * Month          month($name, $label = '', $colSize = 12)
 * DateRange      dateRange($name, $label = '', $colSize = 12)
 * DateTimeRange  datetimeRange($name, $label = '', $colSize = 12)
 * TimeRange      timeRange($name, $label = '', $colSize = 12)
 * Number         number($name, $label = '', $colSize = 12)
 * SwitchBtn      switchBtn($name, $label = '', $colSize = 12)
 * Rate           rate($name, $label = '', $colSize = 12)
 * Divider        divider($text, $label = '', $colSize = 12)
 * Password       password($name, $label = '', $colSize = 12)
 * Decimal        decimal($name, $label = '', $colSize = 12)
 * Html           html($html, $label = '', $colSize = 12)
 * Raw            raw($name, $label = '', $colSize = 12)
 * Show           show($name, $label = '', $colSize = 12)
 * Tags           tags($name, $label = '', $colSize = 12)
 * Icon           icon($name, $label = '', $colSize = 12)
 * MultipleImage  multipleImage($name, $label = '', $colSize = 12)
 * MultipleFile   multipleFile($name, $label = '', $colSize = 12)
 * WangEditor     wangEditor($name, $label = '', $colSize = 12)
 * Tinymce        tinymce($name, $label = '', $colSize = 12)
 * UEditor        ueditor($name, $label = '', $colSize = 12)
 * WangEditor     editor($name, $label = '', $colSize = 12)
 * CKEditor       ckeditor($name, $label = '', $colSize = 12)
 * MDEditor       mdeditor($name, $label = '', $colSize = 12)
 * MDReader       mdreader($name, $label = '', $colSize = 12)
 * Match          match($name, $label = '', $colSize = 12)
 * Matches        matches($name, $label = '', $colSize = 12)
 * Fields         fields($name, $label = '', $colSize = 12)
 * Map            map($name, $label = '', $colSize = 12)
 * Items          items($name, $label = '', $colSize = 12)
 */
//特殊组件
fields
items
tab
step

```
###### 参数说明

>$name 字段名称 必填

>$label     显示label ，不填则取name值

>$cloSize   col-md-大小，默认:12