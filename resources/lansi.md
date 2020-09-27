# 蓝思阅读测评

## 介绍

蓝思阅读测评体系从读物难度和读者阅读能力两个方面进行衡量，使用的是同一个度量标尺，因此读者可以根据自己的阅读能力，轻松地选择适合自己的读物。蓝思阅读测评体系使用数字加字母“L”作为衡量难度的度量标尺，难度范围为0L~1700L，数字越小表示读物难度越低或读者阅读能力越低，反之则表示读物难度越高或读者阅读能力越高。

## 句子翻译(异步)
> API: http://api.pigai.org/translation/lexile

######请求参数(POST/GET)

| 参数名称 | 参数说明 |
|---|---|
| doc | 必须(只支持post)，String，文章内容 |
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
> 注: 下面的分析数据将会以POST方式push到接入方指定的接收接口。
>
> header设置：Content-Type: application/json
```json
{
    "lansi": 470,			// 蓝思得分
    "score_words": 27.657058143238,	// 单词得分
    "score_sent_len": 18.803418803419,	// 句子得分
    "score_doc": 23.230238473329,	// 文章得分
    "num_sent": 3,			// 句子数量
    "num_word": 25,			// 单词数量
    "num_word_uniq": 22,		// 去重后的单词数量
    "num_zhongkao": 17,			// 新课标中考词汇表中单词数量
    "num_gaokao": 2,			// 新课标高考词汇表中单词数量
    "num_daxue": 0,			// 大学1-4级词汇表中单词数量
    "num_unknown": 3,			// 未在词汇表中单词（超纲词汇）数量
    "unknown_words": [			// 未在词汇表中单词（超纲词汇）
        "usage",
        "code",
        "complexity"
    ]
}
```
