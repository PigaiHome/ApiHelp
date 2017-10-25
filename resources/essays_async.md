# 批改作文API资源

### 介绍
为了保证在大访问量高并发下，对外服务的稳定性，满足客户的业务需求，批改网增加作文分析异步接口。

异步分析接口，在正常情况下，返回分析结果的速度很快，用户几乎感知不到和同步接口的区别; 当并发量比较大时，会采用排队机制，先将作文存入队列，然后交由分布式分析引擎进行处理, 分析完成后, 再主动通知接入的第三方(需要提供接收接口)。

### 作文分析(异步)
异步分析: `http://api.pigai.org/essays/rapid_experience_async`

###### 请求参数(POST/GET)

###### GET方式
> curl 'http://api.pigai.org/essays/rapid_experience_async?title=english&comcontext=english&scope=all_json&access_token=Your_Access_Token'

###### POST方式
> curl http://api.pigai.org/essays/rapid_experience_async -d 'title=english&comcontext=english&scope=all_json&access_token=Your_Access_Token'


| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| title | 必须，作文标题 |
| comcontext | 必须，作文内容 |
| scope | 必须, 资源访问控制，固定值:all_json |
| solution | 选填(只支持post)，作文标准答案范文(用于跑题度检测)，string |
| lang | 选填，`zh_cn`, `zh_tw`, `en` |
| rid | 选填，批改网作文号, 用于设置打分公式(高级版功能) |
| config | 选填,自定义打分配置项(高级版功能) |
| unique_id | `scope=storage_result`时必须(高级版功能) |

>config 格式如下:

```
{
    "word_cnt": { //字数限制
        "low": 100,
        "high": 200
    },
    "index_words": [ //要点设置
        "hi/hello",
        "watch/see"
    ]
}
```

### 资源scope
根据`appkey`的作用范围，开发者每次通过认证获取的access_token都有一个作用域`scope`,决定了该token能否从批改网的api获取正确的返回值。

### 返回结果
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
###### 失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```

###### 异步返回分析结果数据格式
> 注: 下面的分析数据将会以POST方式push到接入方指定的接收接口。
>
> header设置：Content-Type: application/json

```json
{
    "score": 79.5, //总得分
    "score_cat": { //四个维度
        "1": {
            "name": "词汇",
            "score": 0.8426485
        },
        "2": {
            "name": "句子",
            "score": 0.74554825
        },
        "3": {
            "name": "篇章结构",
            "score": 0.7881277
        },
        "4": {
            "name": "内容相关",
            "score": 0.7233994
        }
    },
    "comment": "采用了适当的衔接手法，层次清晰；句式变化多样，句法方面做的很棒；作者词汇基本功很好，高级词汇表达也比较恰当。", //总评
    "sentences": [
        {
            "sid": 0, // 第几句, 从0开始
            "pid": 1, // 段落, 从1开始
            "text": "Firstly, no accomplishment can be achieved in a transitory time, and success asks for continuous industrious work and efforts.",
            "comment": [
                {
                    "class": "error_trp",
                    // 四大类: warn 警告，error 错误，error_trp 提示，great 好
                    "cat": "学习提示",
                    "msg": "易混词汇: <b>effort</b>, trouble, pains, endeavour, struggle 均表示“努力”之意。",
                    "word_list": "efforts", //关键词
                    "rank": 0
                }
            ]
        },
        {
            "sid": 1,
            "pid": 1,
            "text": "One can taste the feeling of success only when he is more diligent than others.",
            "comment": [
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>only</b> :&nbsp;<span class='suggest'>just/merely/barely/singly/solely/rarely</span>",
                    "word_list": "only",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "学习提示",
                    "msg": "易混词汇: <b>diligent</b>, industrious 均表示“勤奋的”之意。",
                    "word_list": "diligent",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 2,
            "pid": 1,
            "text": "It is not only an attempt to theory discussion, but also the need of practice.",
            "comment": [
                {
                    "class": "error_trp",
                    "cat": "学习提示",
                    "msg": "易混词汇: drill, exercise, <b>practice</b>, training, discipline 都有“练习，训练，锻炼”之意。",
                    "word_list": "practice",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 3,
            "pid": 1,
            "text": "As the saying goes,\"Genius only means hard-working all one's life.\"",
            "comment": [
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>hard-working</b> :&nbsp;<span class='suggest'>diligent/assidious/industrious</span>",
                    "word_list": "hard-working",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "拓展辨析",
                    "msg": "动名搭配 mean...life 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=mean life/von\"> 34</a> 次",
                    "word_list": "",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>only</b> :&nbsp;<span class='suggest'>just/merely/barely/singly/solely/rarely</span>",
                    "word_list": "only",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>hard-working</b> :&nbsp;<span class='suggest'>assiduous</span>",
                    "word_list": "hard-working",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 4,
            "pid": 1,
            "text": "From my own perspective, firstly, efforts is more important, if you have not acquired the knowledge, your talent will not be used, but will be devoid of silence.",
            "comment": [
                {
                    "class": "error",
                    "cat": "句子错误",
                    "msg": "请检查<b>is</b>，确认主谓一致。",
                    "word_list": "is",
                    "rank": 100
                },
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>if</b> :&nbsp;<span class='suggest'>provided that</span>",
                    "word_list": "if",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "拓展辨析",
                    "msg": "动名搭配 acquire...knowledge 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=acquire knowledge/von\"> 37</a> 次",
                    "word_list": "",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 5,
            "pid": 1,
            "text": "To name only a few, Edison said,\"Success is 1% inspiration and perspiration\".",
            "comment": [
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>only</b> :&nbsp;<span class='suggest'>just/merely/barely/singly/solely/rarely</span>",
                    "word_list": "only",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "学习提示",
                    "msg": "易混词汇: little, <b>few</b>, several 均含“少量的”之意。",
                    "word_list": "few",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 6,
            "pid": 1,
            "text": "It demonstrates the importance of hard-working.",
            "comment": [
                {
                    "class": "warn",
                    "cat": "语法警示",
                    "msg": "确认<b>of hard-working</b>符合语法规范。",
                    "word_list": "of hard-working .",
                    "rank": 99
                },
                {
                    "class": "error_trp",
                    "cat": "拓展辨析",
                    "msg": "动名搭配 demonstrate...importance 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=demonstrate importance/von\"> 35</a> 次",
                    "word_list": "",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>hard-working</b> :&nbsp;<span class='suggest'>assiduous</span>",
                    "word_list": "hard-working",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 7,
            "pid": 1,
            "text": "Also be said that God rewards the dilligent.",
            "comment": [
                {
                    "class": "error",
                    "cat": "词语错误",
                    "msg": "请检查<b>dilligent</b>，确认拼写正确。",
                    "word_list": "dilligent",
                    "rank": 100
                }
            ]
        },
        {
            "sid": 8,
            "pid": 1,
            "text": "What's more, every single person is different and we all have kinds of unique talent.",
            "comment": [
                {
                    "class": "great",
                    "cat": "闪光短语",
                    "msg": "<b>what's more</b>有助于提高文章衔接",
                    "word_list": "^ what 's more ,",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "拓展辨析",
                    "msg": "动名搭配 have...kind 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=have kind/von\"> 809</a> 次",
                    "word_list": "",
                    "rank": 0
                },
                {
                    "class": "great",
                    "cat": "闪光短语",
                    "msg": "<b>what's more</b>意思是<b>另外，而且…</b>，是经典补充类词组。",
                    "word_list": "what 's more",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 9,
            "pid": 1,
            "text": "There is one more point, some will soar-but many more than previously will not find work to match their talents, qualifications or even quite modest ambitions for a job and a home.",
            "comment": [
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>or</b> :&nbsp;<span class='suggest'>otherwise/if not/before/or else</span>",
                    "word_list": "or",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "推荐表达",
                    "msg": "<b>quite</b> :&nbsp;<span class='suggest'>fairly</span>",
                    "word_list": "quite",
                    "rank": 0
                },
                {
                    "class": "error_trp",
                    "cat": "拓展辨析",
                    "msg": "动名搭配 match...talent 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=match talent/von\"> 17</a> 次",
                    "word_list": "",
                    "rank": 0
                }
            ]
        },
        {
            "sid": 10,
            "pid": 1,
            "text": "Try to find the best way possible to convert your talent to something that gives service to people, Obviously, success always smiles upon people who are diligent.",
            "comment": [
                {
                    "class": "error",
                    "cat": "大小写错误",
                    "msg": "请检查<b>Obviously</b>，疑似大小写错误",
                    "word_list": "Obviously",
                    "rank": 100
                },
                {
                    "class": "error_trp",
                    "cat": "拓展辨析",
                    "msg": "<b>people</b>表示“人，民族”。查看与<a href=\"http://bbs.pigai.org/forum.php?mod=viewthread&tid=12942&page=1&extra=#pid30263\" target=\"_blank\"><b>person</b></a>的区别。",
                    "word_list": "people",
                    "rank": 0
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

