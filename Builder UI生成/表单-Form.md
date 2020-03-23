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
//特殊组件
tab
step
fields
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

##### 多选[checkbox]、单选[radio]、下拉[select]

>`options($data)`
如 `$field->options(['1' => '男', '2' => '女'])`。

>`optionsData($collect, $textField, $idField = 'id')`
如 `$field->optionsData(Department::where(['status' => 1])->select(), 'dep_name')`。

##### 下拉[select]
>`dataUrl($url, $textField, $KeyField= 'id')` ajax加载
如 `$field->dataUrl(url('user/data'), 'nickname')`

```php
// **** 数据接口返回
class User extends Controller
{
    protected $dataModel;

    protected function initialize()
    {
        $this->dataModel = new User;
    }

    public function data()
    {
        $q = input('q');
        $where =[]; 

        if($q)
        {
            $where []= ['nickname|phone|email', 'like', '%' . $q .'%'];
        }

        return json(['data' => $this->dataModel->where($where)->select()]);
    }
}
```


##### From 中 Tab的使用

```php
        $form->tab('基本信息');

        $form->text('nickname', '姓名')->required();
        $form->text('police_no', '警号')->required();
        $form->text('idcard_no', '身份证号')->required();
        $form->text('mobile', '手机号')->required();
        $form->radio('sex', '性别')->options([0 => '保密', 1 => '男', 2 => '女']);

        $form->tab('个人信息');

        $form->select('politic', '政治面貌')->options(['' => '请选择'] + UserInfo::$politics);
        $form->textarea('hoby', '特长爱好');
        $form->text('school', '学校');
        $form->text('major', '专业');
        $form->select('education', '学历')->options(['' => '请选择'] + UserInfo::$educations);
        $form->date('birthday', '生日');
        $form->textarea('description', '个人备注');
```

##### From 中 Step的使用

```php
        $form->step('基本信息');

        $form->text('nickname', '姓名')->required();
        $form->text('police_no', '警号')->required();
        $form->text('idcard_no', '身份证号')->required();
        $form->text('mobile', '手机号')->required();
        $form->radio('sex', '性别')->options([0 => '保密', 1 => '男', 2 => '女']);

        $form->step('个人信息');

        $form->select('politic', '政治面貌')->options(['' => '请选择'] + UserInfo::$politics);
        $form->textarea('hoby', '特长爱好');
        $form->text('school', '学校');
        $form->text('major', '专业');
        $form->select('education', '学历')->options(['' => '请选择'] + UserInfo::$educations);
        $form->date('birthday', '生日');
        $form->textarea('description', '个人备注');
```

##### From 中 Fields的使用

> fields方便组合排版多个输入字段，一般用于多个字段放在同一行的情况

```php
        $form->fields('教育信息')->size(2, 10);
        $form->text('school', '学校', 6);
        $form->text('major', '专业', 6);
        //[教育信息]这个label占[col-2],[学校] + [专业]平分剩余的[col-10]。
        $form->fieldsEnd();//调用 fieldsEnd结束，否则后面的会继续加入

        //上面的相当于：
        $form->fields('教育信息')->size(2, 10)->with(
            $form->text('school', '学校', 6),
            $form->text('major', '专业', 6)
        );
        //使用 with接收不定数量的`Field` 就不需要调用 fieldsEnd
```
##### Select 级联使用: `$select->withNext($nextSelect, $autoLoad);`

>$nextSelect : 下一级Select

>$autoLoad : 当这个Select选值变化时，是否自动ajax加载下一级

以下示例使用扩展：(省市区镇，三级或四级联动)<https://gitee.com/ichynul/tpextareacity>
```php
         $form->fields('省/市/区2')->size(2, 10)->with(
            $form->select('province1', '省份', 3)
                ->optionsData($selectP, 'ext_name')
                ->showLabel(false)
                ->dataUrl(url('api/areacity/province'), 'ext_name')
                ->size(0, 12)
                ->withNext(
                    $form->select('city1', '城市', 3)
                        ->optionsData($selectC, 'ext_name')
                        ->showLabel(false)
                        ->dataUrl(url('api/areacity/city'), 'ext_name')
                        ->size(0, 12)
                        ->withNext(
                            $form->select('area1', '区域', 3)
                                ->optionsData($selectA, 'ext_name')
                                ->showLabel(false)
                                ->dataUrl(url('api/areacity/area'), 'ext_name')
                                ->size(0, 12)
                        )
                )
        );
```

##### match 和 matches
分别相当于只读的`radio`和只读的`checkbox`,纯文字的。

```php
$table->match('type', '类型')->options([
    1 => '<label class="label label-success">增加</label>', 
    2 => '<label class="label label-danger">支出</label>'
])->value(1);

//输出 ：增加
```

```php
$form->matches('colors', '颜色')->options([
    1 => '红', 
    2 => '橙',
    3 => '黄', 
    4 => '绿',
    5 => '青', 
    6 => '蓝',
])->value('1,3,5');

//输出 ：红、黄、青
```