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
           ->btnEnable();

         $table->getActionbar()
           ->btnEdit()
           ->btnEnable();
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