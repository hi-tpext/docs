#### 配置范例
```json
{
    "name": "youname/modulename",
    "description": "thinkphp extension",
    "type": "library",
    "keywords": [
        "thinkphp"
    ],
    "homepage": "http://your-web-site.com/",
    "license": "Apache-2.0",
    "authors": [
        {
            "name": "youname",
            "email": "youname@email.com"
        }
    ],
    "require": {
        "topthink/framework": "5.1.*",
        "ichynul/tpext": "^1.0.1",
        "ichynul/tpextbuilder": "^1.0.1"
    },
    "autoload": {
        "psr-4": {
            "tpext\\modulename\\": "src/"
        },
        "files": [
            "src/helper.php"
        ]
    }
}
```
#### 说明
>autoload>psr-4:定义命名空间[`"tpext\\modulename\\": "src/"`]

>autoload>files:定义helper[`src/helper.php`]

#### helper.php
```php
<?php

use tpext\common\ExtLoader;
use tpext\myadmin\common\hooks\Auth;
use tpext\myadmin\common\hooks\Log;
use tpext\myadmin\common\hooks\Setup;

$classMap = [
    'tpext\\myadmin\\common\\Module'
];

//注册扩展，重要，不然你的扩展无法自动启动
ExtLoader::addClassMap($classMap);

//hooks
ExtLoader::watch('module_init', Setup::class, '替换错误及跳转模板', false);
ExtLoader::watch('module_init', Auth::class, '权限验证', false);
ExtLoader::watch('app_end', Log::class, '记录日志', false);

```