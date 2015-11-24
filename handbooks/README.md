# 批改网API手册

批改API是使用OAuth2进行用户授权、获取API资源，这也是OAuth2的二大步骤。

目前的资源仅提供批改网的作文分析结果包括 分数、按句点评、四大类别分项分数和评语，后续批改网会提供更加丰富的API资源。


###API规范

目前此套API使用OAuth2接入用户账号

API返回格式均为JSON，除非服务器或者网络故障，请求的HTTP status均为200

**注意：往批改网post或者get的参数请使用UTF8编码并urlencode过**

####API访问频次

```

单个用户  500次/小时

一个用户通过一个应用 100次/小时
```

####API返回结果示例
```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {}
}
```
####API返回字段说明

| 字段 | 说明 |
| --- | --- |
| error | 提示信息，成功为SUCCESS，否则返回错误的提示信息 |
| error_code | 错误代码，成功为0，参考错误代码  |
| error_description | 错误描述 |
| data |  请求返回的数据，一般为json格式 |

####error_code 参考错误代码
| 错误编号 | 错误码 | 错误描述 |
| --- | --- | --- |
| 0 | success | 成功信息 |
| 10002 | insufficient_scope | 超出作用范围 |
| 10003 | invalid_token | 提供的token无效 |
| 20002 | incorrect_response_parameter | 不正确的响应参数 |
| 20003 | get_resource_failed | 获取资源失败 |
