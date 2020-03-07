###### 基本使用
```php
    $builder = Builder::getInstance('用户管理', '列表');
    $table = $builder->table();

    $table->show('id', 'ID');
    $table->show('username', '登录帐号');
    $table->text('name', '姓名')->autoPost()->getWapper()->addStyle('max-width:80px');
    $table->show('role_name', '角色');
    $table->show('email', '电子邮箱')->default('无');
    $table->show('phone', '手机号')->default('无');
    $table->show('errors', '登录失败');
    $table->show('create_time', '添加时间')->getWapper()->addStyle('width:180px');
    $table->show('update_time', '修改时间')->getWapper()->addStyle('width:180px');

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

>禁用
```
useLayer(false) 
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

```
>其他，如果上面的不改用，你可以自己添加

添加一个链接
>btnLink($url, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '')

添加一个批量操作
btnPostChecked($url, $label = '', $class = 'btn-secondary', $icon = 'mdi-checkbox-marked-outline', $attr = '', $confirm = true)