### 简介
 
提供全局组件(form/tabel/layer/tree/cotent)的创建方法

### 主要方法
```php

//获取一个全局实例（单列模式）
//$title：页面标题,$desc：页面描述
getInstance($title = '', $desc = '');

//获取一个表单
form($size = 12);

//获取一个表格
table($size = 12);

//获取一个工具栏
toolbar($size = 12);

//默认获取一个ZTree树
tree($size = 12);

//获取一个ZTree树
zTree($size = 12);

//获取一个JSTree树
jsTree($size = 12);

//获取一自定义内容
content($size = 12);

//获取一tab内容
tab($size = 12);

```