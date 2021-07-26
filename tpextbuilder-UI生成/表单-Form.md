# form表单

## 支持的组件

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
```

## 特殊组件

`fields`, `items`, `tab`, `step`

## field参数说明

`$name` 字段名称 必填 ,如 `goods_name` 或 `category.name`(关联模型)

`$label`     显示label ，不填则取name值

`$cloSize`   col-md-大小，默认:12

## form常用方法

```php
//设置字段元素的默认大小，后面创建的元素就不必一个一个去设置大小了。
$form->defaultDisplayerSize(2, 6);

//设置字段元素默认`col-md`大小
$form->defaultDisplayerColSize(12);

//只读，表单里面所有元素只读
$form->readonly(true);

//是否使用ajax提交，默认使用，一般按默即可
$form->ajax(true);

//设置表单的id，同一个页面有多个表单时可设置不同的id，避免js冲突，一般按默即可
$form->formId('form2');

//设置表单提交的url/action
$form->action(url('myaction');

//设置【提交】【重置】按钮大小
$form->butonsSizeClass('btn-xs');

//禁用自动生成底部【提交】【重置】按钮
$form->bottomButtons(false);

//手动设置按钮
$form->btnSubmit('提&nbsp;&nbsp;交');
$form->btnReset('重&nbsp;&nbsp;置');
$form->btnBack('返&nbsp;&nbsp;回');
```

### 分组布局

建议使用`fields`分组，基于`clo-size`的分组布局不易控制，互相影响。

#### 假如要分成左右两列

1.使用`fields`:

```php
//第一组：
$form->fields('g1', '', 6)->showLabel(false)->size(0, 12);
$form->text('nickname', '姓名');
$form->text('mobile', '手机号')->maxlength(11);
$form->select('department_id', '部门')->options($departList);
$form->fieldsEnd();

//第二组：
$form->fields('g2', '', 6)->showLabel(false)->size(0, 12);
$form->image('avatar', '照片');
$form->text('school', '学校');
$form->select('nation', '民族')->options($nationList);
$form->fieldsEnd();
```

2.基于`co-sizel`分:

```php
$form->defaultDisplayerColSize(6);//设置默认col大小col-md-6，自动分为左右两列。

$form->text('nickname', '姓名');
$form->text('mobile', '手机号')->maxlength(11);
$form->select('department_id', '部门')->options($departList);
$form->image('avatar', '照片');//图片高度与其他的不同，容易影响布局
$form->text('school', '学校');
$form->select('nation', '民族')->options($nationList);

```
