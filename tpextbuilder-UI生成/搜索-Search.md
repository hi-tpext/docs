其实就是`Form`，把某些不适合使用的组件隐藏了
```php
/**
 * Methods.
 *
 * Text           text($name, $label = '', $colSize = 2, $filter = '')
 * Checkbox       checkbox($name, $label = '', $colSize = 2, $filter = '')
 * Radio          radio($name, $label = '', $colSize = 2, $filter = '')
 * Button         button($type, $label = '', $colSize = 2, $filter = '')
 * Select         select($name, $label = '', $colSize = 2, $filter = '')
 * MultipleSelect multipleSelect($name, $label = '', $colSize = 2, $filter = '')
 * Textarea       textarea($name, $label = '', $colSize = 2, $filter = '')
 * Hidden         hidden($name)
 * Color          color($name, $label = '', $colSize = 2, $filter = '')
 * RangeSlider    rangeSlider($name, $label = '', $colSize = 2, $filter = '')
 * Date           date($name, $label = '', $colSize = 2, $filter = '')
 * Datetime       datetime($name, $label = '', $colSize = 2, $filter = '')
 * Time           time($name, $label = '', $colSize = 2, $filter = '')
 * Year           year($name, $label = '', $colSize = 2, $filter = '')
 * Month          month($name, $label = '', $colSize = 2, $filter = '')
 * DateRange      dateRange($name, $label = '', $colSize = 2, $filter = '')
 * DateTimeRange  datetimeRange($name, $label = '', $colSize = 2, $filter = '')
 * TimeRange      timeRange($name, $label = '', $colSize = 2, $filter = '')
 * Number         number($name, $label = '', $colSize = 2, $filter = '')
 * SwitchBtn      switchBtn($name, $label = '', $colSize = 2, $filter = '')
 * Rate           rate($name, $label = '', $colSize = 2, $filter = '')
 * Divider        divider($text, $label = '', $colSize = 2, $filter = '')
 * Decimal        decimal($name, $label = '', $colSize = 2, $filter = '')
 * Tags           tags($name, $label = '', $colSize = 2, $filter = '')
 * Icon           icon($name, $label = '', $colSize = 2, $filter = '')
 * Fields         fields($name, $label = '', $colSize = 12, $filter = '')
 */
```
###### field参数说明

>$name 字段名称 必填

>$label     显示label ，不填则取name值

>$cloSize   col-md-大小，默认:2

>$filter  搜索条件，默认 'eq'

```
###### search常用方法
```php
//设置字段元素的默认大小，后面创建的元素就不必一个一个去设置大小了。
$search->defaultDisplayerSize(4, 8);

//设置字段元素默认`col-md`大小
$search->defaultDisplayerColSize(2);
```


`$search`相当于一个`$form`，是`$table`的一部分。

protected function filterWhere()
{
     //根据提交数据返回搜索条件，此方法可以不手动重写，会自动生成搜索条件，没怎么测试过，所以还是推荐手写。
}

```php
protected function buildSearch()
{
    //$search = $table->getSearch();//获取一个搜索

    $search = $this->search;

    //页面顶部快速切换：tabLink。

    $search->tabLink('is_onsasle')->options([1 => '已上架', 2 => '未上架']);

    $search->hidden('is_onsasle');//用一个隐藏字段接收切换的值，字段的名称要和上面tabLink的一样。

    //$search->select('is_onsasle', '上架')->options([1 => '已上架', 2 => '未上架']);//或者用一个select或radio也行。

    //其他
    $search->text('kwd', '名称/spu', 3)->maxlength(20);

    $search->select('category_id', '分类', 3)->dataUrl(url('/admin/shopcategory/selectPage'), 'name');

    $search->select('brand_id', '品牌', 3)->dataUrl(url('/admin/shopbrand/selectPage'));
}

```

## addTop / addBottom ,顶部或底部内容

```php
$search->addTop()->content()->fetch('demo');

$search->addBottom()->content()->display('{name}', ['name' => 'jim']);

```