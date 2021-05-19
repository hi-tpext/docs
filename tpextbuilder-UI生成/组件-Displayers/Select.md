# 下拉选择

`HasOptions`　trait 为`Checkbox` `Radio` `Select` `DualListbox` `MultipleSelect` `Match` `Matches` 共有。

## 主要方法

```php
//是否使用增强的select2，默认为使用
public function select2($use){}

//ajax加载url
public function dataUrl($url, $textField = '', $idField = '', $delay = 250, $loadmore = true){}

//占位提示
public function placeholder($val){}

//js 参数设置
public function jsOptions($options){}

//联动，当此select的选值改变时，nextSelect会重新加载，nextSelect必须设置了ajax加载url
public function withNext($nextSelect){}
```

HasOptions　trait 为[Checkbox][Radio][Select][MultipleSelect][Match][Matches]共有。

### 关于联动

```php
 $search->select('province', '省份')->dataUrl(url('api/areacity/province'), 'ext_name')->withNext(
     $search->select('city', '城市')->dataUrl(url('api/areacity/city'), 'ext_name')->withNext(
         $search->select('area', '地区')->dataUrl(url('api/areacity/area'), 'ext_name')
     )
 );
 //省份变化了，会以选中的省份值作为参数去请求`api/areacity/city`把下面的城市列出来，
 //城市变化也类似
```

相当于：

```php
$province = $search->select('province', '省份')->dataUrl(url('api/areacity/province'), 'ext_name');
$city = $search->select('city', '城市')->dataUrl(url('api/areacity/city'), 'ext_name')->withPrev($area);
$area = $search->select('area', '地区')->dataUrl(url('api/areacity/area'), 'ext_name')->withPrev($city);
```

但一般不这么用，除非这几个字段被其他字段分开了，位置上没有连在一起，到仍然保持联动效果。

### ajax 数据源

`tpext\builder\traits\actions\HasIndex`已内置了以当前控制器模型`$dataModel`为基础的[selectPage]

如有控制器：`\app\admin\controller\Member`

```php
<?php

namespace app\admin\controller;

use app\common\model;
use think\Controller;
use tpext\builder\traits\HasBuilder;

/**
 * Undocumented class
 * @title 会员管理
 */
class Member extends Controller
{
    use HasBuilder;

    /**
     * Undocumented variable
     *
     * @var model\Member
     */
    protected $dataModel;

    protected function initialize()
    {
        $this->dataModel = new model\Member;
        $this->pageTitle = '会员管理';
        $this->enableField = 'status';
        $this->pagesize = 8;

        $this->selectTextField = '{id}#{nickname}({mobile})';//设置下拉显示格式
        $this->selectSearch = 'username|nickname|mobile';//设置搜索字段
    }
}
```

那么其他页面可以：`$search->select('member_id', '会员')->dataUrl(url('/admin/member/selectPage'));`

显示：

```html
<select name="member_id">
<option vlaue="1001">1001#小明(13312345678)</option>
<option vlaue="1002">1002#小红(13312345677)</option>
<option vlaue="1003">1003#小刚(13312345676)</option>
<!--更多-->
</select>
```

其他情况可以自己写`action`实现

实例：

```php
/**
* Undocumented function
*
* @title 下拉选择用户
* @return mixed
*/
public function selectPageUser()
{
    $q = input('q');
    $page = input('page/d');
    $selected = input('selected');

    if ($selected) {
        $list = $this->dataModel->where('id', 'in', $selected)->order($sortOrder)->select();
    } else {
        $q = input('q', '');
        $page = $page < 1 ? 1 : $page;
        $pagesize = 20;

        $where = [];

        if ($q) {
            $where[] = ['nickname|mobile|username', 'like', '%' . $q . '%'];
        }

        $list = $this->dataModel->where($where)->limit(($page - 1) * $pagesize, $pagesize)->select();
    }

    $data = [];

    foreach ($list as $li) {
        $data[] = [
            'id' => $li['id'],
            'text' => $li['id_name'],
        ];
    }

    return json(
        [
            'data' => $data,
            'has_more' => count($data) == $pagesize,
        ]
    );
}
```

### ajax附带其他字段值

`->withParams($parasm)`;

如：

```php
$form->radio('type', '人员类型')->options([1=>'男', 2=>'女']);
$form->select('member_id', '人员')->dataUrl(url('/admin/member/selectPage2'))->withParams('type');
//每次ajax请求[/admin/member/selectPage2]页面时，都会附带一个参数如[&type=1]，在selectPage2方法中就可以根据此参数，只返回男性或女性的姓名。
```
