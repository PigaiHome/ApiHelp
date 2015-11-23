# 了解OAuth2.0
###客户端应用授权
1.
引导需要授权的用户到如下地址：
```
http://api.pigai.org/oauth2/authorize?response_type=token&client_id=Your_Client_Id&redirect_uri=Your_Registered_Redirect_Uri&state=Your_State"
```
2.
如果授权成功,页面跳转至 `Your_Registered_Redirect_Uri/#access_token=TOKEN`

###OAuth2.0 错误码
批改网OAuth2.0实现中，授权服务器在接收到验证授权请求时，会按照OAuth2.0协议对本请求的请求头部、请求参数进行检验，若请求不合法或验证未通过，授权服务器会返回相应的错误信息，包含以下几个参数：

>`error`: 错误码  
`error_code`: 错误的内部编号  
`error_description`: 错误的描述信息  
>`error_url`: 可读的网页URI，带有关于错误的信息，用于为终端用户提供与错误有关的额外信息。

######错误信息的返回方式有两种：
1. 当请求授权Endpoint：http://api.pigai.org/oauth2/authorize 时出现错误，返回方式是：跳转到redirect_uri，并在uri的query parameter中附带错误的描述信息。
2. 当请求access token endpoint: http://api.pigai.org/oauth2/access_token 时出现错误，返回方式：返回JSON文本。例如：
```json
{
    "error": "unsupported_response_type",
    "error_code": 21329,
    "error_description": "不支持的ResponseType."
    "data": {}
}
```

######OAuth2.0错误响应中的错误码定义如下表所示：

| 错误码(error) | 错误编号(error_code) | 错误描述(error_description) |
| --- | --- | --- |
| redirect_uri_mismatch | 21322 | 重定向地址不匹配 |
| invalid_request | 21323 | 请求不合法 |
| unsupported_grant_type | 21328 | 不支持的 GrantType |
| unsupported_response_type | 21329 | 不支持的 ResponseType |
