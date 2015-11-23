# 资源列表
###作文
1.
快速体验: `http://api.pigai.org/essays/rapid_experience`

######请求参数(post)

| 参数名称 | 参数说明 |
| :--: | :--: |
| title | 作文标题 |
| comcontext | 作文内容 |
| api | 统计ID |
| tpl | 输出格式，固定值all_json |

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
