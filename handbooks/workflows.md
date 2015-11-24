# 授权流程
批改网的API使用OAuth2进行用户授权。

##授权接口
+ [获取token方法一](#获取token方法一)
+ [获取token方法二](#获取token方法二)

##获取token方法一
`适用场景：`客户端获取token，如：javascript

>http://api.pigai.org/oauth2/authorize2

######请求方式: GET，JSONP
######请求参数
|参数名称 | 参数说明 |
|---|---|
| client_id | 必须,应用的唯一标识，对应于 APIKey |
| response_type | 必须,固定值token。 |
| callback | 必须，自定义JavaScript函数，建议使用jsonP来做。|
| state | 可选,服务器会把state值原样传回客户端,用于防止csrf攻击 |

#####返回参数

返回的格式为js的callback(jsondata) 函数,其中callback为自定义的。

下文为jsondata 返回值参考：

######成功
```json
{
"access_token":"fc21ed0947c99cd8987da173857c89278682d908"
,"expires_in":"7200"
,"token_type":"Bearer"
,"state":"xyz"
}
```
|参数名称 | 参数说明 |
|---|---|
| access_token | 临时token |
| expires_in | 过期时间限制，默认为2个小时。 |
| state | 带过来的state 防止crsf攻击 |

######失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```

###DEMO

  >http://api.pigai.org/oauth2/authorize2?callback=myfun&response_type=token&client_id=APIKEY&state=xyz

#####返回

```js
myfun({"access_token":"8d734bf19bc9e7b0dbec5642204e7988a05cc222","expires_in":"7200","token_type":"Bearer","state":"xyz"})
```

#####JsonP的实例

```js
$.ajax({
	   url: 'http://api.pigai.org/oauth2/authorize2',
	   type: 'get',
	   data: {
		response_type: 'token',
		client_id: '提供APIKEY',
		state: 'xyz'
	   },
	   dataType: 'jsonp'
	}).done(function(d) {
		alert( d.access_token );
		console.log(d.access_token);
	});
```



##获取token方法二

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
| state | 带过来的state 防止crsf攻击 |
######失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```



