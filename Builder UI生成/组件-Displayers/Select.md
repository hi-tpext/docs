下拉选择

主要方法：

```
//是否使用增强的select2，默认为使用
public function select2($use){}

//ajax加载url
public function dataUrl($url, $textField = '', $idField = '', $delay = 250, $loadmore = true){}

//占位提示
public function placeholder($val){}

//js 参数设置
public function jsOptions($options){}

//联动，当此select的选值改变时，nextSelect会重新加载，nextSelect必须设置了ajax加载url
public function withNext($nextSelect){}
```
HasOptions　trait 为[Checkbox][Radio][Select][MultipleSelect][Match][Matches]共有。

### 关于联动

```php
 $search->select('province', '省份')->dataUrl(url('api/areacity/province'), 'ext_name')->withNext(
     $search->select('city', '城市')->dataUrl(url('api/areacity/city'), 'ext_name')->withNext(
         $search->select('area', '地区')->dataUrl(url('api/areacity/area'), 'ext_name')
     )
 );
 //省份变化了，会以选中的省份值作为参数去请求`api/areacity/city`把下面的城市列出来，
 //城市变化也类似
```
相当于：
```php
$area = $search->select('area', '地区')->dataUrl(url('api/areacity/area'), 'ext_name');
$city = $search->select('city', '城市')->dataUrl(url('api/areacity/city'), 'ext_name')->withNext($area);
$search->select('province', '省份')->dataUrl(url('api/areacity/province'), 'ext_name')->withNext($city);
```
但一般不这么用