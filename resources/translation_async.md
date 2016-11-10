# 翻译资源

## 句子翻译(异步)
> API: http://api.pigai.org/translation/trans_sentence_async

######请求参数(POST/GET)

| 参数名称 | 参数说明 |
|---|---|
| comcontext | 必须(只支持post)，String，答案 |
| solution | 必须(只支持post)，String，翻译的标准参考答案 |
| info_word | 选填(只支持post), JSON串，限定词, 格式如: '["word1", "word2"]' |
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
    "data": {
        "key": "PG2_emoapp_a345dd676b7975b22f45cc85c775bd90"
    }
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

######异步返回数据格式
> 注: 以下数据将会以参数`data={...}` 形式,以POST方式push到接入方指定的接收接口。

```json
{
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
        "degree": 0.9990287 // 跑题度(0~1之间, 值越大跑题度越大)
    },
    "meta_data": { //自定义参数
        "xxx": "xxxx"
    },
    "key": "PG2_emoapp_bb1f71d46d236eb3819a41c59eca920d"
}
```
