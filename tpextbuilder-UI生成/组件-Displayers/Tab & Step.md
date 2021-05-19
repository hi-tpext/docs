# Tab & Step

Tab和Step是`form`内置的用于分割组件的方法。

tab实例：

- 1. 平铺直叙式，多次调用`$form->tab($label)`,每次调用后开启一个新的`tab`，然后跟随其他[fields]

```php
$form->tab('基本信息');//tab 1

$form->image('avatar', '头像')->thumbSize(50, 50);
$form->text('username', '账号')->required()->maxlength(20);
$form->text('nickname', '昵称')->required()->maxlength(20);
$form->text('mobile', '手机号')->maxlength(11);
$form->text('email', '邮件')->maxlength(60);
//
$form->tab('其他信息');//tab 2

$form->textarea('remark', '备注')->maxlength(255);
$form->switchBtn('status', '状态')->default(1);
```

- 2. 使用`with`，此方式把内部的字段使用[with]方法包围，层次更加分明

```php
$form->tab('基本信息')->with(
     $form->image('avatar', '头像')->thumbSize(50, 50),
     $form->text('username', '账号')->required()->maxlength(20),
     $form->text('nickname', '昵称')->required()->maxlength(20),
     $form->text('mobile', '手机号')->maxlength(11),
     $form->text('email', '邮件')->maxlength(60)
);//tab 1

//注意with参数与上面的不同之处
$form->tab('其他信息')->with(function(\tpext\builder\common\Form $from){
     $form->textarea('remark', '备注')->maxlength(255);
     $form->switchBtn('status', '状态')->default(1);
});//tab 2
```

step实例：

不常用也不实用，用法跟`tab`差不多
