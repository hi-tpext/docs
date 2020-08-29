- `HasBuilder`封装了增、删、查、改等所有动作
- 也可按需分别引入`tpext\builder\traits\actions\`命名空间下的相应动作。

```php
use tpext\builder\traits\HasBuilder;
use tpext\builder\traits\actions;

class Admin extends Controller
{
    //use HasBuilder;

    //基础
    use actions\HasBase;
    //按需加载，避免暴露不必要的action

    //列表
    use actions\HasIndex;
    //添加/修改
    use actions\HasAdd;
    use actions\HasEdit;

    //查看
    use actions\HasView;

    //字段编辑
    use actions\HasAutopost;
    //禁用/启用
    use actions\HasEnable;
    //删除
    use actions\HasDelete;
    
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
    protected function buildSearch()
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
    protected function buildForm($isEdit, &$data = [])
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