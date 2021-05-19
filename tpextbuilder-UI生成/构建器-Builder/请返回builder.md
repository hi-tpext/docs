# builder

大多数情况，请返回`$builder->render()`或`$builder`.

```php
$builder = $this->builder('出错了');
//错误，返回的是一个`content`，只渲染了部分内容，js、css等资源都没有。不算绝对错误，但可能与想象不符。
return $builder->content()->display('<p>' . '未能读取文件:' . $fileurl . '</p>');
```

```php
$builder = $this->builder('出错了');
$builder->content()->display('<p>' . '未能读取文件:' . $fileurl . '</p>');
//正确
return $builder->render();
```

特殊：`layer系列`

```php
return $this->builder()->layer()->closeRefresh(1, '保存成功');
return $this->builder()->layer()->closeRefresh(0, '保存失败');
return $this->builder()->layer()->close(0, '数据不存在');
```
