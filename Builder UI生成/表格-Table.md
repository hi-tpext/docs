###### 基本使用
```php
    $builder = Builder::getInstance('用户管理', '列表');
    $table = $builder->table();

    $form = $table->getSearch();
    $form->text('username', '账号', 3)->maxlength(20);
    $form->text('name', '姓名', 3)->maxlength(20);
    $form->text('phone', '手机号', 3)->maxlength(20);
    $form->text('email', '邮箱', 3)->maxlength(20);
    $form->select('role_id', '角色组', 3)->options($this->getRoleList());

    $table->show('id', 'ID');
    $table->show('username', '登录帐号');
    $table->text('name', '姓名')->autoPost()->getWapper()->addStyle('max-width:80px');
    $table->show('role_name', '角色');
    $table->show('email', '电子邮箱')->default('无');
    $table->show('phone', '手机号')->default('无');
    $table->show('errors', '登录失败');
    $table->show('create_time', '添加时间')->getWapper()->addStyle('width:180px');
    $table->show('update_time', '修改时间')->getWapper()->addStyle('width:180px');

    $searchData = request()->post();

    $where = [];
    if (!empty($searchData['username'])) {
        $where[] = ['username', 'like', '%' . $searchData['username'] . '%'];
    }
    if (!empty($searchData['name'])) {
        $where[] = ['name', 'like', '%' . $searchData['name'] . '%'];
    }
    if (!empty($searchData['phone'])) {
        $where[] = ['phone', 'like', '%' . $searchData['phone'] . '%'];
    }
    if (!empty($searchData['email'])) {
        $where[] = ['email', 'like', '%' . $searchData['email'] . '%'];
    }
    if (!empty($searchData['role_id'])) {
        $where[] = ['role_id', 'eq', $searchData['role_id']];
    }

    $sortOrder = input('__sort__', 'id desc');

    $data = $this->dataModel->where($where)->order($sortOrder)->limit(($page - 1) * $pagezise, $pagezise)->select();
    $table->data($data);
    $table->sortOrder($sortOrder);
    $table->paginator($this->dataModel->where($where)->count(), $pagezise);

    if (request()->isAjax()) {
        return $table->partial()->render();
    }

    return $builder->render();
```
###### 常用

>show 显示 

>raw  显示带html的内容

###### 支持部分的form组件行内编辑：

>text,

>textarea

>radio

>select

>checkbox

*** 行内编辑续配合 `autoPost($url)`方法使用，`url`参数不传则默认请求到同一个控制器的`autoPost`action


###### Toolbar工具栏

>默认自动生成[添加 / 批量删除 / 刷新] 即
```
btnAdd / btnDelete / btnRefresh
```

- 基本使用

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

>禁用

```php
$table->useToolbar(false);
```

>手动设置
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
>其他，如果上面的不够用，你可以自己添加

```php
//添加一个链接，打开$ulr
btnLink($url, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '')

//添加一个批量操作，自动附带多选框选中的id只post到`$url`，`$confirm` 批量操作前是否显示确认提示框。
btnPostChecked($url, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '', $confirm = true)
```

********************
###### Actionbar动作栏

>默认自动生成[编辑 / 删除] 即
```
btnEdit / btnDelet
```

- 基本使用

```php
     $table->getActionbar()
            ->btnEdit()
            ->btnEnable()
            ->btnDisable()
            ->btnDelete()
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

>其他，如果上面的不够用，你可以自己添加

```php

//添加一个链接，打开$ulr
btnLink($name = '', $url, $label = '', $class = 'btn-secondary', $icon = '', $attr = '')
```

- `url('demo', ['id' => '__data.pk__']);`
- `相当于 url('demo', ['id'=>'__data.id__']);`
-其他参数：`url('demo', ['id' => '__data.id__', 'type' => '__data.type__', 'status' => 1]);`
```php
//添加一个操作，自动附带当前列id参数post到`$postUrl`，`$confirm` 操作前是否显示确认提示框。
btnPostRowid($name = '', $postUrl, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '', $confirm = true)
```

>控制action的显示禁用

```php
->mapClass([
                'delete' => ['hidden' => '__h_del__'],
                'enable' => ['hidden' => '__h_en__'],
                'disable' => ['hidden' => '__h_dis__'],
            ]);
```

- `delete|enable|disable`按钮名称，如果是自定义[btnLink/btnPostRowid]则为传入的`$name`.
- 'hidden' => '__h_del__'，当这一条记录的`__h_del__`值为真时，这个action会加上`hidden`这个class
- 同理，可以加上`disabled`
```
'enable' => ['disabled' => '__dis_en__'],
```