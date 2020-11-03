下拉多选

继承:`Select`

`HasOptions`　trait 为`Checkbox` `Radio` `Select` `MultipleSelect` `Match` `Matches` 共有。

```php
public function selectPage()
{
    $selected = input('selected');

    $data = [];

    if ($selected) {
        $list = $this->dataModel->where('id', 'in', $selected)->order($sortOrder)->select();
    } else {
        $q = input('q', '');
        $page = input('page/d', 1);
        $page = $page < 1 ? 1 : $page;

        $list = $this->dataModel->where('name|nickname', 'like', '%' . $q . '%')->order($sortOrder)->limit(($page - 1) * $pagesize, $pagesize)->select();
    }

    $hasMore = count($list) == $pagesize ? 1 : 0;

    return json(
        [
            'data' => $data,
            'has_more' => 0,
        ]
    );
}
```