# 授权流程
批改网的API使用OAuth2进行用户授权。

##授权接口
+ [获取token方法](#获取token方法)

##获取token方法

`适用场景：`服务器端获取token，如：php，java等

>http://api.pigai.org/oauth2/access_token

######请求方式: POST
```bash
$ curl http://api.pigai.org/oauth2/access_token \
       -d "grant_type=client_credentials&client_id=Your_App_Key&client_secret=Your_App_Secret"
```
#####请求参数
|参数名称 | 参数说明 |
|---|---|
| grant_type | 必须，值为`client_credentials` |
| client_id | 必须,应用的唯一标识,创建应用时分配的App key |
| client_secret | 必须,创建应用时分配的App secret |

#####返回结果
######成功
```json
{
    "access_token":"336342b797d895c2fafcfa547f751bfd326dc168",
    "expires_in":7200,
    "token_type":"Bearer",
    "scope":null
}
```
|参数名称 | 参数说明 |
|---|---|
| access_token | 临时token |
| expires_in | 过期时间限制，默认为2个小时。 |
| token_type | token 模式 Bearer  |
| state | 带过来的state 防止crsf攻击 |
######失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```
