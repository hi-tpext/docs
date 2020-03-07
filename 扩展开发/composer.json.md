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