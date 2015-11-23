# PHP授权流程
适用于通过server-side获取token的场景,分为两步:

* [获取token](#获取token)
* [获取资源](#获取资源)

##phpsdk说明
#####下载地址
> https://github.com/webeautiful/Oauth2_client/releases

#####基本配置
1.
php安装curl库
2.
修改`src/Oauth2_client/`下`cache`目录的权限为777

```bash
$ cd src/Oauth2_client
$ chmod 777 cache
```
##获取token
#####参考实例
> `https://github.com/webeautiful/Oauth2_client/blob/master/examples/get_token_by_client.php`

1.
修改配置

```php
$config = array(
    'cache_token_key'=> 'your_token_cache_name',
    'client_id'=> 'your_app_key',
    'client_secret'=> 'your_app_secret',
    'auth_url'=> 'http://api.pigai.org/oauth2/access_token'
)
```
2.
配置参数说明

| 配置项 | 说明 |
| --- | --- |
| cache_token_key | 设置缓存/获取有效token的键名 |
| client_id | 必须,创建应用时分配的App key |
| client_secret | 必须,创建应用时分配的App secret |
| auth_url | 获取token的认证地址.固定值, `http://api.pigai.org/oauth2/access_token` |


3.
返回值为token字符串,如: `8d734bf19bc9e7b0dbec5642204e7988a05cc222`

##获取资源
######请求方式: GET

#####方法: 请参考[JSDK授权流程](./implicit.html#JSDK获取资源)

