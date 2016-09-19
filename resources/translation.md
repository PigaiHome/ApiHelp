# 翻译资源

## 句子翻译
> API: http://api.pigai.org/translation/trans_sentence

######请求参数(POST/GET)

| 参数名称 | 参数说明 |
|---|---|
| rid | String，批改网作文号 |
| snt | String，要翻译的句子 |
| info_word | JSON串，限定词, 格式如: '["sentence1", "sentence2"]' |
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| scope | 资源访问控制，固定值:all_json |

###资源scope
根据`appkey`的作用范围，开发者每次通过认证获取的access_token都有一个作用域`scope`,决定了该token能否从批改网的api获取正确的返回值。

###返回结果
######成功
```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {}
}
```
######失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```

######scope为all_json的返回详细格式

```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
    }
}
```
