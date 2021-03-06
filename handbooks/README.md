# 批改网API开发手册

批改API是使用OAuth2进行用户授权、获取API资源，这也是OAuth2的二大步骤。

目前的资源仅提供批改网的作文分析结果包括 分数、按句点评、四大类别分项分数和评语，后续批改网会提供更加丰富的API资源。


### API规范

目前此套API使用OAuth2接入用户账号

API返回格式均为JSON，除非服务器或者网络故障，请求的HTTP status均为200

**注意：往批改网post或者get的参数请使用UTF8编码并urlencode过**

### API访问频次

```
一个用户通过一个应用 1200次/分钟
```

### API返回结果示例
```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {}
}
```
##### API返回字段说明

| 字段 | 说明 |
| --- | --- |
| error | 提示信息，成功为SUCCESS，否则返回错误的提示信息 |
| error_code | 错误代码，成功为0，参考错误代码  |
| error_description | 错误描述 |
| data |  请求返回的数据，一般为json格式 |

##### error_code 参考错误代码
批改网OAuth2.0实现中，授权服务器在接收到验证授权请求时，会按照OAuth2.0协议对本请求的请求头部、请求参数进行检验，若请求不合法或验证未通过，授权服务器会返回相应的错误信息，包含以下几种类型：

| 错误编号 | 错误码 | 错误描述 |
| --- | --- | --- |
| 0 | success | 成功信息 |
| 10002 | insufficient_scope | 需要更高权限的token |
| 10003 | invalid_token | 提供的token无效 |
| 10004 | invalid_client | appkey无效 |
| 10005 | invalid_request | 请求参数无效 |
| 20002 | incorrect_response_parameter | 不正确的响应参数 |
| 20003 | get_resource_failed | 获取资源失败 |
| 20004 | access_frequency_restrict | API访问频次限制 |
| 20005 | account_expired | 账号已过期 |
| 20006 | incorrect_request_parameter | 不正确的请求参数 |
| 20007 | must_parameter_unique_id | unique_id为必填参数 |

