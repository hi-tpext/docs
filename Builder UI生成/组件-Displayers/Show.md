显示内容

跟`Raw`差不多，区别是`Raw`可以显示html,`show`会转义html。

主要方法

```php
//对于较长的内容，切割一部分显示，点击[...]按钮显示全部
public function cut($len = 0, $more = '...'){}

//内容默认是被一个`div`包围的,inline模式就没有外面的`div`。此用法在fields包含多个`show`时有用
public function inline($val){}
```