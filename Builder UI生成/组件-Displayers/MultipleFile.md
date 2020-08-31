多个文件上传

主要方法

```php
//设置是否可以上传
public function canUpload($val){}

//是否显示文件路径输入框，可以直接手动修改
public function showInput($val){}

//是否显示[选择]按钮从已上传的文件中选择
public function showChooseBtn($val){}

//文件总数量限制
public function limit($val){}
```