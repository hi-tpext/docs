```php
//在当前页面引入一个js文件
customJs($jsfile);
//如：
$builder->customJs('/static/admin/js/my.js');

//在当前页面引入一个css文件
customCss($cssfile);
//如：
$builder->customCss('/static/admin/css/my.css');

//在当前页面添加一段js脚本 
addScript($script);
//如：
$script = <<<EOT
alert('666');
EOT;
$builder->addScript($script);

//在当前页面添加一段style样式 
addStyleSheet($style);
//如：
$builder->addStyleSheet('
.row
{
    mrgin:0;
}
');

//在当前页面显示一个顶部通知消息
notify(($msg, $type = 'info');
//如：
$builder->notify('您未完善个人信息');

//关闭当前layer弹出层
layer()->close($success = true, $msg = '操作成功');

//关闭当前layer弹出层，并刷新上一级页面
layer()->closeRefresh($success = true, $msg = '操作成功');

//关闭当前layer弹出层，并刷让上一级页面跳转到一个新的url
layer()->closeGo($success = true, $msg = '操作成功', $url);
```

