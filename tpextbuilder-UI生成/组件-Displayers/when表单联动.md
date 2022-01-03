# 表单联动

## [form]和[search]中可用

### 单选: radio / select

```php
// 单选，radio / select 
$form->radio('test1', '测试1')->options(['1' => '选项1', '2' => '选项2', '3' => '选项3'])->default(1)
    ->when(
        1, //选中值为1时
        $form->text('test_1_a', 'test_1_a')->required()
        //... 更多字段
    )->when(
        [2, 3],//选中值为[2 或 3]时，多个情况时传入参数为数组，数组各元素之间为[或]的关系
        $form->text('test_1_b', 'test_1_b')->required(),
        $form->textarea('test_1_c', 'test_1_c')->required()
        //... 更多字段
    );
```

### 多选：checkbox / multipleSelect / dualListbox

```php
// 
$form->checkbox('test2', '测试2')->options(['1' => '选项1', '2' => '选项2', '3' => '选项3', '4' => '选项4'])->default(1)
    ->when(
        1,//只选中一个值，且这个值为1时
        $form->text('test_2_a', 'test_2_a')->required()
        //... 更多字段
    )->when(
        [2, 3],//只选中一个值，且这个值为[2 或 3]时，多个情况时传入参数为数组，数组各元素之间为[或]的关系
        $form->text('test_2_b', 'test_2_b')->required(),
        $form->textarea('test_2_c', 'test_2_c')->required()
        //... 更多字段
    )->when(
        [4, '3+4', '2+1+4'],//(只选中一个值，且这个值为4时) 或 (同时选中3,4两个值) 或 (同时选中1,2,4三个值)。
        //数组各元素之间为[或]的关系，单个元素用+号连接多个值表示同时选中（值之间不分先后顺序[2+1+4]和[1+2+4]和[4+1+2]等情况等效）
        $form->radio('test_2_d', 'test_2_d')->options([1 => '1', 2 => '2']),
        $form->textarea('test_2_e', 'test_2_e')->required()
        //... 更多字段
    );
```

#### 单个元素用+号连接多个值

单个元素内字符串都可以用`+`相连，不一定是数字，取决于根据选项值的类型：

```php
// 
$form->checkbox('test2', '测试2')->options(['type1' => '选项1', 'type2' => '选项2', 'type3' => '选项3', 'type4' => '选项4'])->default(1)
    ->when(
        'type1',
        $form->text('test_2_a', 'test_2_a')->required()
        //...
    )->when(
        ['type2', 'type3'],
        $form->text('test_2_b', 'test_2_b')->required()
        //...
    )->when(
        ['type4', 'type3 + type4', 'type2 + type1 + type4'],
        $form->radio('test_2_d', 'test_2_d')->options([1 => '1', 2 => '2'])
        //...
    );
```

### when的使用

基本格式`when($cases, ...$toggleFields)`;

第二参数`$toggleFields`的3种使用方式：

- 1. 作为可变参数：

`when($cases, $field1, $field2, $field3, $fieldN, );`

- 2. 作为数组元素[作为1的折衷方案，可变参数最后跟随一个,号，在低版本php中会报错，放在数组中可避免]

`with($cases, [$field1, $field2, $field3, $fieldN, ]);`

- 3. 作为匿名方法中的语句

`with($cases, function($form){$field1;$field2;$field3;$fieldN;});`

```php
$form->radio('test1', '测试1')->options(['1' => '选项1', '2' => '选项2', '3' => '选项3', '4' => '选项4'])->default(1)
    ->when(
        1,
        $form->text('test_1_a', 'test_1_a')->required(),
        $form->textarea('test_1_b', 'test_1_b'),
        //... 更多字段
    )->when(
        2,
        [
            $form->text('test_1_c', 'test_1_c')->required(),
            $form->textarea('test_1_d', 'test_1_d'),
            //... 更多字段
        ]
        
    )->when(
        [3, 4],
        function(\tpext\builder\common\Form $_form) use ($form){
            //$_form 和 $form 是同一个东西，实际中使用其中一种方式即可。
            $_form->text('test_1_e', 'test_1_e')->required();
            $form->textarea('test_1_f', 'test_1_f');
            //... 更多字段
        }
        
    );
```

若第二参数`$toggleFields`不传，则可再调用`with(...$toggleFields)`方法。

```php
$form->radio('test1', '测试1')->options(['1' => '选项1', '2' => '选项2', '3' => '选项3', '4' => '选项4'])->default(1)
    ->when(1)->with(
        $form->text('test_1_a', 'test_1_a')->required(),
        $form->textarea('test_1_b', 'test_1_b'),
        //... 更多字段
    )
    ->when(2)->with(
       [
            $form->text('test_1_c', 'test_1_c')->required(),
            $form->textarea('test_1_d', 'test_1_d'),
            //... 更多字段
        ]
    )
    ->when([3, 4])->with(function(\tpext\builder\common\Form $_form) use ($form){
            //$_form 和 $form 是同一个东西，实际中使用其中一种方式即可。
            $_form->text('test_1_e', 'test_1_e')->required();
            $form->textarea('test_1_f', 'test_1_f');
            //... 更多字段
    });
```

#### 注意，第二个参数`$toggleFields`的传入时机

要么`when`的时候传入，要么`when`的时候不传，然后再调用`with`方法传入。不要两种方式同时使用，如下面的用法是错误的:

```php
$form->radio('test1', '测试1')->options(['1' => '选项1', '2' => '选项2', '3' => '选项3', '4' => '选项4'])->default(1)
    ->when(
        1,
        $form->text('test_1_a', 'test_1_a')->required(),
        //... 更多字段
    )->with(
       [
            $form->text('test_1_b', 'test_1_b'),
            $form->textarea('test_1_c', 'test_1_c'),
            //... 更多字段
        ]
    );
```

### 拓展用法，利用`with`实现分散布局

```php
$text1 = $form->text('test_1_a', 'test_1_a')->required();
//
$radio1 = $form->radio('test1', '测试1')->options(['1' => '选项1', '2' => '选项2'])->default(1);
//
$text2 = $form->text('test_1_b', 'test_1_b')->required();
$text3 = $form->text('test_1_c', 'test_1_c')->required();
//
$radio1->when(1)->with($text1, $text2);
$radio1->when(2)->with($text3);
//text1,text2,text3在文档中的位置相对于radio1有前有后是分散开的，如果在when中传入，那位置是受限的，使用`with`则更灵活。
```

### 切换fields

```php
$form->radio('test1', '测试1')->options(['1' => '选项1', '2' => '选项2'])->default(1)
    ->when(1)->with(
        $form->left(12)->with(
            //fields
        )
    )
    ->when(2)->with(
        $form->left(12)->with(
            //fields
        )
    );
```

### 表单提交

- 切换后被隐藏的元素，表单提交时是被忽略的，后台获取不到对应的字段

- 可以在不同的`case`里面重复同一个字段

```php
$form->radio('test1', '测试1')->options(['1' => '选项1', '2' => '选项2', '3' => '选项3'])
    ->when(1)->with(
        $form->text('test_1', 'test_1')->required()-help('case-1 的test_1'),
        $form->text('test_2', 'test_2')->required(),
    )
    ->when(2)->with(
        $form->text('test_1', 'test_1')->required()-help('case-2 的test_1'),//不同case的字段重复是允许的，只有其中一个会提交
        $form->text('test_3', 'test_3')->required(),
    )
    ->when(3)->with(
        $form->text('test_4', 'test_4')->required(),
    );
```

- 切换后隐藏的字段js验证暂时取消，重新切换回来后重新生效
