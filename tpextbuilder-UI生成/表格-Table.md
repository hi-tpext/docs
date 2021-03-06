# table 表格

## 支持的组件

```php
/**
 * Methods.
 *
 * Field          field($name, $label = '', $colSize = 12)
 * Text           text($name, $label = '', $colSize = 12)
 * Checkbox       checkbox($name, $label = '', $colSize = 12)
 * Radio          radio($name, $label = '', $colSize = 12)
 * Select         select($name, $label = '', $colSize = 12)
 * MultipleSelect multipleSelect($name, $label = '', $colSize = 12)
 * Textarea       textarea($name, $label = '', $colSize = 12)
 * Color          color($name, $label = '', $colSize = 12)
 * RangeSlider    rangeSlider($name, $label = '', $colSize = 12)
 * File           file($name, $label = '', $colSize = 12)
 * Image          image($name, $label = '', $colSize = 12)
 * Date           date($name, $label = '', $colSize = 12)
 * Datetime       datetime($name, $label = '', $colSize = 12)
 * Time           time($name, $label = '', $colSize = 12)
 * Year           year($name, $label = '', $colSize = 12)
 * Month          month($name, $label = '', $colSize = 12)
 * TimeRange      timeRange($name, $label = '', $colSize = 12)
 * Number         number($name, $label = '', $colSize = 12)
 * SwitchBtn      switchBtn($name, $label = '', $colSize = 12)
 * Decimal        decimal($name, $label = '', $colSize = 12)
 * Html           html($html, $label = '', $colSize = 12)
 * Raw            raw($name, $label = '', $colSize = 12)
 * Show           show($name, $label = '', $colSize = 12)
 * Tags           tags($name, $label = '', $colSize = 12)
 * Icon           icon($name, $label = '', $colSize = 12)
 * MultipleImage  multipleImage($name, $label = '', $colSize = 12)
 * MultipleFile   multipleFile($name, $label = '', $colSize = 12)
 * Match          match($name, $label = '', $colSize = 12)
 * Matches        matches($name, $label = '', $colSize = 12)
 * Fields         fields($name, $label = '', $colSize = 12)
 *
 */
```

## field参数说明

`$name` 字段名称 必填

`$label`     显示label ，不填则取name值

`$cloSize`   col-md-大小，暂无实际用处

- 理论上支持全部`form`组件，但一般来说，使用`show`,`field`,`text`,`Checkbox`,`Radio`,`Select`,`Textarea`等基本够用了。
- `show`和`field`纯显示，`text`,`Checkbox`等表单元素支持在表格行内修改并失去焦点自动提交【配合autoPost】。

## 基本使用

```php

    $table->show('id', 'ID');
    $table->show('username', '登录帐号');
    $table->text('name', '姓名')->autoPost()->getWrapper()->addStyle('max-width:80px');
    $table->show('role_name', '角色');
    $table->show('email', '电子邮箱')->default('无');
    $table->show('phone', '手机号')->default('无');
    $table->show('errors', '登录失败');
    //多字段组合使用`fields`
    $table->fields('times', '添加/更新时间')->with(
       $table->show('create_time', '添加时间'),
       $table->show('update_time', '修改时间')
    )->getWrapper()->addStyle('width:180px');
   
```

## 常用

- `show()` 显示

- `raw()`  显示带html的内容

## 支持部分的form组件行内编辑

`text`,`textarea`,`radio`,`select`,`checkbox`

行内编辑续配合 `autoPost($url)`方法使用，`url`参数不传则默认请求到同一个控制器的[`autoPost`]action

## Toolbar工具栏

> 默认自动生成 [添加 / 批量删除 / 刷新] 即

```php
btnAdd() / btnDelete() / btnRefresh()
```

### 完整实列

```php
$table->getToolbar()
    ->btnAdd()
    ->btnEnable()
    ->btnDisable()
    ->btnDelete()
    ->btnExport()
    ->btnExports(['xlxs'=>'xlsx','xls'=>'xls'])
    ->btnRefresh();
```

### 使用 `dropdown actions`

```php
$table->getToolbar()
    ->btnAdd()
    ->btnActions(
        [
            'enable' => ['url' => url('enable', ['state' => 1])，'label' => '启用'],
            'disable' => ['url' => url('enable', ['state' => 0]), 'label' => '禁用'],
            'delete' => '删除',
        ]
    )
    ->btnExport()
    ->btnExports(['xlxs'=>'xlsx','xls'=>'xls'])
    ->btnRefresh();
```

### 禁用工具栏

```php
$table->useToolbar(false);
```

### 手动设置

```php

//添加
btnAdd($url = '', $label = '添加', $class = 'btn-primary', $icon = 'mdi-plus', $attr = '');

//批量删除
btnDelete($postUrl = '', $label = '删除', $class = 'btn-danger', $icon = 'mdi-delete', $confirm = true, $attr = '');

//刷新
btnRefresh($label = '', $class = 'btn-cyan', $icon = 'mdi-refresh', $attr = 'title="刷新"');

//启用
btnEnable($postUrl = '', $label = '启用', $class = 'btn-success', $icon = 'mdi-check', $confirm = true, $attr = '');

//禁用
btnDisable($postUrl = '', $label = '禁用', $class = 'btn-warning', $icon = 'mdi-block-helper', $confirm = true, $attr = '');

//导入
btnImport($afterSuccessUrl, $acceptedExts = "rar,zip,doc,docx,xls,xlsx,ppt,pptx,pdf", $fileSize = '20', $label = '导入', $class = 'btn-pink', $icon = 'mdi-cloud-upload', $attr = 'title="上传文件"')

//导出（默认，点击按钮直接请求后台）
btnExport($postUrl = '', $label = '导出', $class = 'btn-pink', $icon = 'mdi-export', $attr = 'title="导出"')

//导出（可选，点击弹出菜单，选择导出类型）
btnExports($items, $postUrl = '', $label = '导出', $class = 'btn-secondary', $icon = 'mdi-export', $attr = 'title="导出"')

```

>其他，如果上面的不够用，你可以添加自定义按钮

```php
//添加一个链接，打开$ulr
btnLink($url, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '')

//添加一个批量操作，自动附带多选框选中的id发送post请求到`$url`，`$confirm` 批量操作前是否显示确认提示框。
btnPostChecked($url, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '', $confirm = true)
//已选中多个id参数获取
//$ids = input('post.ids');

//添加一个批量打开，自动附带多选框选中的id发送get请求到`$url`。一般用于批量分配，移动等功能。
btnOpenChecked($url, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '')

//已选中多个id参数获取
//$ids = input('get.ids');
```

---

## Actionbar动作栏

>默认自动生成 [编辑 / 删除] 即

```php
btnEdit() / btnDelete()
```

- 基本使用

```php
     $table->getActionbar()
            ->btnEdit()
            ->btnEnable()
            ->br()//换行
            ->btnDisable()
            ->btnDelete()
            ->mapClass([
                'delete' => ['hidden' => '__h_del__'],
                'enable' => ['hidden' => '__h_en__'],
                'disable' => ['hidden' => '__h_dis__'],
            ]);
```

### 使用`dropdown actions`

```php
$table->getActionbar()
    ->btnEdit()
    ->btnActions(
        [
            'enable' => ['url' => url('enable', ['state' => 1]), 'label' => '启用'],
            'disable' => ['url' => url('enable', ['state' => 0]), 'label' => '禁用'],
            'delete' => '删除',
            'view' => ['url' => url('view', ['id' => '__dat.pk__']), 'label' => '查看','confirm' => '2'],
        ]
    )
    ->mapClass([
        'delete' => ['hidden' => '__h_del__'],
        'enable' => ['hidden' => '__h_en__'],
        'disable' => ['hidden' => '__h_dis__'],
    ]);
```

>禁用

```php
$table->useActionbar(false);
```

>手动设置

```php
//编辑
btnEdit($url = '', $label = '', $class = 'btn-primary', $icon = 'mdi-lead-pencil', $attr = 'title="编辑"')

//删除
btnDelete($postUrl = '', $label = '', $class = 'btn-danger', $icon = 'mdi-delete', $confirm = true, $attr = 'title="删除"')

//查看
btnView($url = '', $label = '', $class = 'btn-primary', $icon = 'mdi-lead-pencil', $attr = 'title="查看"')

//禁用
btnDisable($postUrl = '', $label = '', $class = 'btn-warning', $icon = 'mdi-block-helper', $confirm = true, $attr = 'title="禁用"')

//启用
btnEnable($postUrl = '', $label = '', $class = 'btn-success', $icon = 'mdi-check', $confirm = true, $attr = 'title="启用"')
```

>其他，如果上面的不够用，你可以自己添加自定义按钮

```php

//添加一个链接，打开$ulr
btnLink($name = '', $url, $label = '', $class = 'btn-secondary', $icon = '', $attr = '')
```

- `url('demo', ['id' => '__data.pk__']);`

- 相当于 `url('demo', ['id'=>'__data.id__']);`，因为`pk`代表当前的主键。

- 其他参数：`__data.字段名__`

  如：`url('demo', ['id' => '__data.id__', 'type' => '__data.type__', 'status' => 1]);`

```php
//添加一个操作，自动附带当前列id参数post到`$postUrl`，`$confirm` 操作前是否显示确认提示框。
btnPostRowid($name = '', $postUrl, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '', $confirm = true)
```

> 控制`action`的显示禁用

```php
$table->getActionbar()
    ->btnEdit()
    ->btnEnableAndDisable()
    ->btnView()
    ->btnDelete()
    ->btnPostRowid('clear_errors', url('clearErrors'), '', 'btn-info', 'mdi-backup-restore', 'title="重置登录失败次数"')
    ->mapClass([
        'delete' => ['hidden' => '__h_del__'],//当这行数据的`__h_del__`字段值为真(1或true)时，`enable`这个按钮加上`hidden`的class
        'enable' => ['hidden' => '__h_en__'],
        'disable' => ['hidden' => '__h_dis__'],
        //也可以像下面这样,就不用去循环数组设置。
        //'enable' => ['hidden' => [1, 'enable']],//,当这行数据的`enable`字段值为`1`时，`enable`这个按钮加上`hidden`的class
        //'disable' => ['hidden' => [[0,2], 'enable']],//当这行数据的`enable`字段值为`0`或`2`时，`disable`这个按钮加上`hidden`的class
        //'disable' => ['hidden' => [2, 'enable', '>']],//当这行数据的`enable`字段值大于`2`时，`disable`这个按钮加上`hidden`的class
        //[2, 'enable', '>'] 中 `>` 为比较逻辑
        // 更多逻辑 : in_array|not_in_array|eq|gt|lt|egt|elt|strstr|not_strstr
        // eq|gt|lt|egt|elt等价于 =|>|<|>=|<=
        // !in_array 等价于not_in_array,!strstr等价于not_strstr

        // 'enable' => ['hidden' => function ($data) { //闭包，返回真则加上对应的
        //     return $data['enable'] == 1;
        // }],
    ]);
//循环数组去设置
foreach ($data as &$d) {
    $d['__h_del__'] = $d['id'] == 1;
    $d['__h_en__'] = $d['enable'] == 1;
    $d['__h_dis__'] = $d['enable'] != 1 || $d['id'] == 1;
}
unset($d);
```

- `delete|enable|disable`按钮名称，如果是自定义[btnLink/btnPostRowid]则为传入的`$name`.
- '`hidden`' => '`__h_del__`'，当这一条记录的`__h_del__`值为真时，这个action会加上`hidden`这个class

- 同理，可以加上`disabled`

```php
'enable' => ['disabled' => '__dis_en__'],
```

### `ActionBtn`的`label`支持使用变量

如`评论({comments_count})` => `评论(12)`

模型定义一个获取器：

```php
class ShopGoods extends Model
{
    public function getCommentCountAttr($value, $data)
    {
        return ShopGoodsComment::where(['goods_id' => $data['id']])->count();
    }
}
```

```php
$table->getActionbar()
    ->btnEdit()
    ->btnLink('comments', url('/admin/shopgoodscomment/index', ['goods_id' => '__data.pk__']), '评论{comments_count}', 'btn-warning', 'mdi-comment-processing-outline')
```

## addTop / addBottom ,顶部或底部内容

```php
$table->addTop()->content()->fetch('demo', ['name' => '小明']);

$table->addBottom()->content()->display('我的名字叫{name}', ['name' => '小明']);
```
