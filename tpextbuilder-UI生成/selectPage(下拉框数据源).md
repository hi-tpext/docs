默认每一个有列表页`index`的控制器都对应一个`selectPage`，`url('/admin/controller/selectPage')`;

```php
class Member extends Controller
{
    protected function initialize()
    {
        //...其他初始化
        
        $this->selectTextField = '{id}#{nickname}({mobile})';
        $this->selectSearch = 'nickname|mobile';
        
        $this->selectIdField ='id';
        $this->selectFields ='id,nickname,mobile';
        $this->selectOrder = 'nickname';
        $this->selectScope = [['enable', 'eq' ,1]];
    }
}
```
### 说明

`selectTextField` 格式化显示的文本，单个字段直接用字段名，多字段名称用大括号包围;`{fieldname}`。

如上面的格式表示：会员id#昵称(手机号)：

```html
<select>
<option value="10001">10001#小明(13312345670)</option>
<option value="10003">10002#小红(13312345671)</option>
<option value="10003">10003#小刚(13312345672)</option>
<select>
```
`selectSearch` 查询字段
用户在下拉框中输入字符串查询，ajax请求后台接口，接口中返回`昵称`或`手机号包含`这个关键字的数据。
核心代码：
```php
$kwd = input('q');
$data = $this->dataModel->where('nickname|mobile','like',"%$kwd%")->select();
```

`selectIdField` 键，控制的是 `<option value="10001">10001#小明(13312345670)</option>` 中的`value`对应到哪个字段。如果键不是`id`，那就需要设置。

`selectFields` 优化查询效果，比如上面的查询，只需要`id`、`nickname`、`mobile`三个字段。默认是`*`全部字段，如果追求性能，可以设置查询字段只这三个 。

`selectOrder` 顾名思义，排序方式。

`selectScope` 默认条件，比如上面的例子，只显示已启用的用户，未启用的就不显示出来让选择。

### 其他说明

`selectTextField`、`selectIdField`是默认情况，如果使用`select`没设置`textField`、`idField`两个参数，就按默认配置的。如果指定了，就可以覆盖。

默认情况：

```php
$select->select('member_id', '会员')->dataUrl(url('/admin/member/selectPage'));
```

```html
<select>
<option value="10001">10001#小明(13312345670)</option>
<option value="10003">10002#小红(13312345671)</option>
<option value="10003">10003#小刚(13312345672)</option>
<select>
```

指定`textField`、`idField`：

```php
$select->select('mobile', '会员')->dataUrl(url('/admin/member/selectPage'),'{id}#{nickname}','mobile');
```
```html
<select>
<option value="13312345670">10001#小明</option>
<option value="13312345671">10002#小红</option>
<option value="13312345672">10003#小刚</option>
<select>
```

`textField`是单个字段，大括号`{}`省略

```php
$select->select('mobile', '会员手机')->dataUrl(url('/admin/member/selectPage'),'nickname','mobile'); 
```
```html
<select>
<option value="13312345670">小明</option>
<option value="13312345671">小红</option>
<option value="13312345672">小刚</option>
<select>
```