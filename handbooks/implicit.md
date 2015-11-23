# JSDK授权流程

jsdk是通过jsonP方式实现跨越获取token、资源，总带来说需要下面2个步骤：
+ [JSDK:获取token](#JSDK:获取token)
+ [JSDK:获取资源](#JSDK:获取资源)

##JSDK:获取token

  请参考  [2.2 授权流程 中的 API:请求用户授权](../handbooks/workflows.html) ，这边的不需要认证，而直接通过 client_id 获取token

>http://api.pigai.org/oauth2/authorize2

######请求方式: get , jsonP
#####请求参数
|参数名称 | 参数说明 |
|---|---|
| client_id | 必须,应用的唯一标识，对应于 APIKey |
| response_type | 必须，必须为token。 |
| callback | 必须，自定义JavaScript函数，建议使用jsonP来做。|
| state | 可选，服务器会把state值原样传回客户端,用于防止csrf攻击 |

#####返回参数

返回的格式为js的callback(jsondata) 函数,其中callback为自定义定义的。

下文为jsondata 返货款参考：


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

##JSDK:获取资源

>http://api.pigai.org/essays/rapid_experience

######请求方式: GET,jsonP
#####请求参数
| 参数名称 | 参数说明 |
| :--: | :--: |
| title | 作文标题 |
| comcontext | 作文内容 |
| tpl | 输出格式，固定值all_json、html_json |
| callback | 必须，自定义JavaScript函数，建议使用jsonP来做。|

#####返回参数说文



