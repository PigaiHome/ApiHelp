# 授权流程
批改网的API使用OAuth2进行用户授权。

##授权接口
+ [API:请求用户授权](#请求用户授权)
+ [API:获取token](#获取token)

###请求用户授权

>http://api.pigai.org/oauth2/authorize

######请求方式: GET
######请求参数
|参数名称 | 参数说明 |
|---|---|
| client_id | 必须,应用的唯一标识，对应于 APIKey |
| response_type | 必须,必须为code或者token其中一个。 |
| state | 可选,服务器会把state值原样传回客户端,用于防止csrf攻击 |
| redirect_uri | 可选,用户授权完成后的回调地址，应用需要通过此回调地址获得用户的授权结果。|

###获取token

>http://api.pigai.org/oauth2/access_token

######请求方式: POST
######请求参数
|参数名称 | 参数说明 |
|---|---|
| client_id | 必须,创建应用时分配的App key |
| client_secret | 必须,创建应用时分配的App secret |
| grant_type | 必须，值为`authorization_code` |
| code | 必须，上一步获取的`code` |
| redirect_uri | 必须,需要和创建应用时填写的回调地址相同 |
