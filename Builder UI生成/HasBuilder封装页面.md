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
        if (!empty($searchData['username'])) {
            $where[] = ['username', 'like', '%' . $searchData['username'] . '%'];
        }
        return $where;
    }

     /**
     * 构建搜索
     *
     * @return void
     */
    protected function builSearch()
    {
        $search = $this->search;
        $search->text('username', '账号', 3)->maxlength(20);
        //构建搜索表单
    }

    /**
     * Undocumented function
     *
     * @param array $data
     * @return void
     */
    protected function buildTable(&$data = [])
    {
        $table = $this->table;

        $table->show('id', 'ID');
        $table->show('username', '登录帐号');
        //构建表格
        //略

        $table->getToolbar()
           ->btnAdd()
           ->btnDelete();

         $table->getActionbar()
           ->btnEdit()
           ->btnDelete();
     }
   
    /**
     * 构建表单
     *
     * @param boolean $isEdit
     * @param array $data
     */
    protected function builForm($isEdit, &$data = [])
    {
        $form = $this->form;
        $form->text('username', '登录帐号')->required()->beforSymbol('<i class="mdi mdi-account-key"></i>');
        //构建表单
        //略
    }

   /**
     * 保存数据
     *
     * @param integer $id
     * @return void
     */
    private function save($id = 0)
    {
        $data = request()->only([
          'username',
        ], 'post');

        // 数据验证等，略
        if ($id) {
            $data['update_time'] = date('Y-m-d H:i:s');
            $res = $this->dataModel->where(['id' => $id])->update($data);
        } else {
            $res = $this->dataModel->create($data);
        }
    }
}
```
* `HasBuilder` 包含了全部，如果用不到，可以按需加载。
* 一方面避免分配权限的时候不需要的动作也显示，
* 另一方面也保证api安全，动作是存在的。
* 即使你没有显示`删除`这个按钮。
```php
    protected function buildTable(&$data = [])
    {
        $table->getToolbar()
           ->btnAdd();
           //->btnDelete();

         $table->getActionbar()
            ->btnEdit();
            //->btnDelete();
    }

    public function delete()
    {
       //
    }
```
* 不代表用户就调用不了`delete`这个动作。

```php
use tpext\builder\traits\actions\HasBase;
use tpext\builder\traits\actions\HasIndex;
use tpext\builder\traits\actions\HasDelete;

class Operationlog extends Controller
{
    //只需要 index、delete 两个动作
    use HasBase;
    use HasIndex;
    use HasDelete;
    
    //实现下面三个动作逻辑：

    protected function filterWhere()
    {
       //...
    }
    
    protected function builSearch()
    {
        //...
    }
    
    protected function buildTable(&$data = [])
    {
        //...
    }
}
```