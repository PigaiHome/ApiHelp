# 批改作文API资源
###作文
分析结果: `http://api.pigai.org/essays/rapid_experience`


######请求参数(POST/GET)

######GET方式
> curl 'http://api.pigai.org/essays/rapid_experience?title=english&comcontext=english&scope=all_json&access_token=Your_Access_Token'

######POST方式
> curl http://api.pigai.org/essays/rapid_experience -d 'title=english&comcontext=english&scope=all_json&access_token=Your_Access_Token'


| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| title | 必须，作文标题 |
| comcontext | 必须，作文内容 |
| solution | 选填(只支持post)，作文标准答案范文(用于跑题度检测)，string |
| rule | 选填，设置打分规则:`scanning`-手写识别打分公式（高中）|
| scope | 资源访问控制，可为json,html_json,all_json，默认为all_json |

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
        "score": 40.5, // 总得分
        "score_cat": {
            "1": {
                "name": "词汇",
                "score": 0.442630385488
            },
            "2": {
                "name": "句子",
                "score": 0.477608817276
            },
            "3": {
                "name": "篇章结构",
                "score": 0.413793103448
            },
            "4": {
                "name": "内容相关",
                "score": 0.3
            }
        },
        "comment": "采用了简单的衔接手法，行文流畅；多多加强句法知识；文章用词太过单一，且单词拼写错误较多。",
        "sentences": [ // 逐句分析
            {
                "sid": 0, // 第几句
                "pid": 1, // 段落, 从1开始
                "text": "English is a internationaly language which becomes importantly for modern world.",
                "comment": [
                    {
                        "class": "error", // 分为四类: warn 警告，error 错误，error_trp 提示，great 好
                        "cat": "拼写错误",
                        "msg": "<b>internationaly</b> 疑似拼写错误"
                    },
                    {
                        "class": "error",
                        "cat": "冠词错误",
                        "msg": "请检查<b>a internationaly</b>，疑似冠词错误。"
                    },
                    {
                        "class": "error",
                        "cat": "词语错误",
                        "msg": "词性错误，建议将<b>becomes importantly</b>改为<b>becomes important</b>。"
                    },
                    {
                        "class": "error",
                        "cat": "介词错误",
                        "msg": "介词误用，建议将<b>for modern world</b>改为<b>in modern world</b>。"
                    },
                    {
                        "class": "warn",
                        "cat": "其他",
                        "msg": "<b>for modern world</b>疑似冠词缺失或<a target='_blank' href='http://wiki.pigai.org/index.php?doc-view-2'>可数名词单用</a>。"
                    }
                ]
            }
        ],
        "deviation": {
            "status": "ok", // ok:检测成功, failure: 检测失败
            "rid": "481981", // 作文号
            "degree": 0.9990287 // 跑题度(0~1之间, 值越大跑题度越大)
        }
    }
}
```
