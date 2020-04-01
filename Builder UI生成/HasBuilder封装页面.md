`HasBuilder`封装了常用操作

```php
use tpext\builder\common\Builder;

class Admin extends Controller
{
    use HasBuilder;
    
    protected function filterWhere()
    {
        $searchData = request()->post();

        $where = [];
        //构建搜索条件
        return $where;
    }
}