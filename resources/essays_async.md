# 批改作文API资源

###介绍
为了保证在大访问量高并发下，对外服务的稳定性，满足客户的业务需求，批改网增加作文分析异步接口。

异步分析接口，在正常情况下，返回分析结果的速度很快，用户几乎感知不到和同步接口的区别; 当并发量比较大时，会采用排队机制，先将作文存入队列，然后交由分布式分析引擎进行处理, 分析完成后, 再主动通知接入的第三方(需要提供接收接口)。

###作文分析(异步)
异步分析: `http://api.pigai.org/essays/rapid_experience_async`

######请求参数(POST/GET)

######GET方式
> curl 'http://api.pigai.org/essays/rapid_experience_async?title=english&comcontext=english&scope=all_json&access_token=Your_Access_Token'

######POST方式
> curl http://api.pigai.org/essays/rapid_experience_async -d 'title=english&comcontext=english&scope=all_json&access_token=Your_Access_Token'


| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| title | 必须，作文标题 |
| comcontext | 必须，作文内容 |
| solution | 选填(只支持post)，作文标准答案范文(用于跑题度检测)，string |
| scope | 资源访问控制，固定值:all_json |
| lang | 选填，`zh_cn`, `zh_tw`, `en` |
| rid | 批改网作文号(高级版功能) |
| config | 选填,自定义打分配置项(高级版功能) |

>config 格式如下:

```
{
    "word_cnt": { //字数限制
        "low": 100,
        "high": 200
    }
}
```

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

######异步返回分析结果数据格式
> 注: 下面的分析数据将会以POST方式push到接入方指定的接收接口。
>
> header设置：Content-Type: application/json

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
