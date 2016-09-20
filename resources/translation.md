# 翻译资源

## 句子翻译
> API: http://api.pigai.org/translation/trans_sentence

######请求参数(POST/GET)

| 参数名称 | 参数说明 |
|---|---|
| rid | 必须，Integer，批改网作文号 |
| snt | 必须，String，答案 |
| referer | 选填，JSON串，参考答案, 格式如: '["referer1", 'referer2']'|
| info_word | 选填, JSON串，限定词, 格式如: '["word1", "word2"]' |
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| scope | 必须，资源访问控制，固定值:all_json |

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
        "info": {
            "time": 15,
            "my_port": 7095,
            "rid": "717464",
            "my_ip": "192.168.1.17",
            "did": "0",
            "cate_score": {
                "0": 0,
                "1": 77.86882, # 词汇
                "2": 76.61284, # 句子
                "3": 48.14169, # 篇章结构
                "4": 100 # 内容相关
            },
            "formula_id": "54",
            "final_score": 68.96297,
            "pingyu": "作者句法知识扎实，但从句稍微偏少；高级词汇表达比较恰当，仍需注意积累词汇量；结构良好，但是语言不流畅。", # 总评
            "pingyu_key": "ast:9_cld:4_sntc:9 ttr1:2_b3:8_spell:9 discd:1_pvd:9 "
        },
        "id": "0",
        "status": "ok",
        "score": 51.26656 # 总得分
    }
}
```
