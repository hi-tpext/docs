输出Html

主要方法：
```php
//渲染一个模板文件，和thinkphp框架类似`Controller`,模板存放位置也遵循
public function fetch($template = '', $vars = [], $config = []){}

//渲染一个字符串(模板)
public function display($content = '', $vars = [], $config = []){}
```
### 实例
```php
$form->html('', 'tree')->vale($treeHtml);

$form->html('', 'tree')->fetch('tree',['data' => $data]);

$form->html('', 'tree')->display('<p>{$name}</p>',['name' => '小明']);

```