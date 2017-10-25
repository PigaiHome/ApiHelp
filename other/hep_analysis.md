# 批改作文API资源

`高教社` `天学网`

## 接口列表
+ [提交分析请求](#api1)
+ [取分析结果](#api2)

### 访问域名
> http://api.pigai.org

<div id="api1"></div>
### API1：提交分析请求

> POST /essays/rapid_experience_async  
> GET &nbsp;&nbsp;&nbsp;/essays/rapid_experience_async

#### 请求参数(POST/GET)

| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| scope | 必须, 资源访问控制，固定值:storage_result |
| unique_id | 作文唯一标识 |
| title | 选填, 作文标题 |
| comcontext | 必须，作文内容 |

#### 资源scope
根据`appkey`的作用范围，开发者每次通过认证获取的access_token都有一个作用域`scope`,决定了该token能否从批改网的api获取正确的返回值。

#### 返回结果
##### 失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```
##### 成功
```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
        "page_url": "http://api.pigai.org/guest.html?key=demoa1%2Fe1962ef40db314ea8ea6875818267aa7",
        "key": "PG2_emoapp_a345dd676b7975b22f45cc85c775bd90"
    }
}
```

<div id="api2"></div>
### API2：取分析结果

> GET /essays/result

#### 请求参数(POST/GET)

| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| scope | 必须, 资源访问控制，固定值:storage_result |
| unique_id | 作文唯一标识 |

#### 返回结果
##### 失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```
##### 成功

```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
        "page_url": "http://api2.pigai.org/guest.html?key=demoa1%2Fe1962ef40db314ea8ea6875818267aa7.json",
        "score": 31.5, //总得分
        "result": {
            "score": 31.5,
            "score_cat": { //四个维度
                "1": {
                    "name": "词汇",
                    "score": 0.55290356
                },
                "2": {
                    "name": "句子",
                    "score": 0.2755165
                },
                "3": {
                    "name": "篇章结构",
                    "score": 0.5397758
                },
                "4": {
                    "name": "内容相关",
                    "score": 0.61569084
                }
            },
            "comment": "采用了简单的衔接手法，行文流畅；高级词汇比较灵活，总体用词较为单一，有一些拼写错误；简单句偏多了。",
            "sentences": [
                {
                    "sid": 0, // 第几句, 从0开始
                    "pid": 1, // 段落, 从1开始
                    "text": "my grandmother was growing vegetables in the affternoon.",
                    "comment": [
                        {
                            // 四大类: warn 警告，error 错误，error_trp 提示，great 好
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "my",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "拼写错误",
                            "msg": "请检查<b>affternoon</b>，确认拼写正确。",
                            "word_list": "affternoon",
                            "rank": 100
                        }
                    ]
                },
                {
                    "sid": 1,
                    "pid": 1,
                    "text": "and i was helping with growing potatoes.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "and",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "确认 <b>i</b> 大小写使用正确。",
                            "word_list": "i",
                            "rank": 100
                        },
                        {
                            "class": "error_trp",
                            "cat": "拓展辨析",
                            "msg": "查看<a href=\"http://bbs.pigai.org/t36413-1-1.html\" target=\"_blank\"><b>and</b></a>用于句首的用法。",
                            "word_list": "^ and",
                            "rank": 0
                        }
                    ]
                },
                {
                    "sid": 2,
                    "pid": 1,
                    "text": "when i arrived at the grandmom garden.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "拼写错误",
                            "msg": "请检查<b>grandmom</b>，确认拼写正确。",
                            "word_list": "grandmom",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "确认 <b>i</b> 大小写使用正确。",
                            "word_list": "i",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "when",
                            "rank": 100
                        },
                        {
                            "class": "error_trp",
                            "cat": "学习提示",
                            "msg": "易混词汇: attain, reach, achieve, <b>arrive</b> 均有“达到”之意。",
                            "word_list": "arrived",
                            "rank": 0
                        }
                    ]
                },
                {
                    "sid": 3,
                    "pid": 2,
                    "text": "i am so happy.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "搭配错误",
                            "msg": "请检查<b>i .. am</b>，确认搭配使用正确。",
                            "word_list": "i .. am",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "i",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "句子错误",
                            "msg": "请检查<b>am</b>，确认主谓一致。",
                            "word_list": "am",
                            "rank": 100
                        },
                        {
                            "class": "error_trp",
                            "cat": "学习提示",
                            "msg": "易混词汇: favourable, fortunate, <b>happy</b>, lucky 都可表示“有利的，好运的，顺利的”之意",
                            "word_list": "happy",
                            "rank": 0
                        }
                    ]
                },
                {
                    "sid": 4,
                    "pid": 2,
                    "text": "the place is very cool.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "the",
                            "rank": 100
                        },
                        {
                            "class": "error_trp",
                            "cat": "学习提示",
                            "msg": "易混词汇: cold, <b>cool</b>, chilly, frosty, freezing, icy 均含“冷，凉”之意。",
                            "word_list": "cool",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "overwhelmingly/exceedingly/extremely与短语<b>very</b> 意思相近，overwhelmingly/exceedingly/extremely 更地道，推荐使用。",
                            "word_list": "very",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "more than与短语<b>very</b> 意思相近，more than 更地道，推荐使用。",
                            "word_list": "very",
                            "rank": 0
                        }
                    ]
                },
                {
                    "sid": 5,
                    "pid": 2,
                    "text": "there are so many vegetables,such as potatoes,tomatos...and so on.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "there",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "拼写错误",
                            "msg": "以O为结尾的名词，变为复数形式，通常有生命的东西加<b>es</b>，无生命的东西加<b>s</b>,建议改为<b>tamatoes</b>。",
                            "word_list": "tomatos",
                            "rank": 100
                        },
                        {
                            "class": "warn",
                            "cat": "标点警示",
                            "msg": "英文标点符号之后需要空格。",
                            "word_list": "",
                            "rank": 99
                        }
                    ]
                },
                {
                    "sid": 6,
                    "pid": 2,
                    "text": "i always help my grandmother with looking after her vegetables in her garden every weekend.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "i",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "句子错误",
                            "msg": "请检查<b>help</b>，确认主谓一致。",
                            "word_list": "help",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "搭配错误",
                            "msg": "搭配 <b>look vegetable</b>在语料库中无此用法，疑似中式英语。",
                            "word_list": "look vegetable",
                            "rank": 100
                        },
                        {
                            "class": "warn",
                            "cat": "标点警示",
                            "msg": "英文标点符号之后需要空格。",
                            "word_list": "",
                            "rank": 99
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "do sb. a favor与短语<b>help</b> 意思相近，do sb. a favor 更地道，推荐使用。",
                            "word_list": "help",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "attend to与短语<b>looking after</b> 意思相近，attend to 更地道，推荐使用。",
                            "word_list": "looking after",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "拓展辨析",
                            "msg": "动名搭配 help...grandmother 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=help grandmother/von\"> 6</a> 次",
                            "word_list": "",
                            "rank": 0
                        }
                    ]
                },
                {
                    "sid": 7,
                    "pid": 2,
                    "text": "at first i want to know how grow vegetables .",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "at",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "确认 <b>i</b> 大小写使用正确。",
                            "word_list": "i",
                            "rank": 100
                        },
                        {
                            "class": "warn",
                            "cat": "标点警示",
                            "msg": "英文标点符号之前无须空格",
                            "word_list": "",
                            "rank": 99
                        },
                        {
                            "class": "error_trp",
                            "cat": "拓展辨析",
                            "msg": "动名搭配 grow...vegetable 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=grow vegetable/von\"> 93</a> 次",
                            "word_list": "",
                            "rank": 0
                        }
                    ]
                },
                {
                    "sid": 8,
                    "pid": 2,
                    "text": "in the end ,i know grow vegetables is very diffcultly.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "确认 <b>i</b> 大小写使用正确。",
                            "word_list": "i",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "句子错误",
                            "msg": "请检查<b>know</b>，确认主谓一致。",
                            "word_list": "know",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "句子错误",
                            "msg": "请检查<b>is</b>，确认主谓一致。",
                            "word_list": "is",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "拼写错误",
                            "msg": "请检查<b>diffcultly</b>，确认拼写正确。",
                            "word_list": "diffcultly",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "in",
                            "rank": 100
                        },
                        {
                            "class": "warn",
                            "cat": "标点警示",
                            "msg": "英文标点符号之前无须空格",
                            "word_list": "",
                            "rank": 99
                        },
                        {
                            "class": "warn",
                            "cat": "句子警示",
                            "msg": "请检查<b>know grow</b>，疑似双谓语错误。",
                            "word_list": "know grow",
                            "rank": 99
                        },
                        {
                            "class": "error_trp",
                            "cat": "学习提示",
                            "msg": "易混词汇: aim, goal, purpose, <b>end</b>, target, object, objective 均有“目标，目的”之意。",
                            "word_list": "end",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "overwhelmingly/exceedingly/extremely与短语<b>very</b> 意思相近，overwhelmingly/exceedingly/extremely 更地道，推荐使用。",
                            "word_list": "very",
                            "rank": 0
                        }
                    ]
                },
                {
                    "sid": 9,
                    "pid": 2,
                    "text": "so,protecting our environment is very imoportant.",
                    "comment": [
                        {
                            "class": "error",
                            "cat": "大小写错误",
                            "msg": "请确认句首单词大写。",
                            "word_list": "so",
                            "rank": 100
                        },
                        {
                            "class": "error",
                            "cat": "拼写错误",
                            "msg": "请检查<b>imoportant</b>，确认拼写正确。",
                            "word_list": "imoportant",
                            "rank": 100
                        },
                        {
                            "class": "warn",
                            "cat": "标点警示",
                            "msg": "英文标点符号之后需要空格。",
                            "word_list": "",
                            "rank": 99
                        },
                        {
                            "class": "error_trp",
                            "cat": "拓展辨析",
                            "msg": "动名搭配 protect...environment 在语料库中出现过<a target=\"_blank\" href=\"http://www.pigai.org/corpus/snt/?q=protect environment/von\"> 407</a> 次",
                            "word_list": "",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "more than与短语<b>very</b> 意思相近，more than 更地道，推荐使用。",
                            "word_list": "very",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "therefore/thus/consequently/accordingly/as a result/for that reason/hence与短语<b>so</b> 意思相近，therefore/thus/consequently/accordingly/as a result/for that reason/hence 更地道，推荐使用。",
                            "word_list": "so",
                            "rank": 0
                        },
                        {
                            "class": "error_trp",
                            "cat": "推荐表达",
                            "msg": "overwhelmingly/exceedingly/extremely与短语<b>very</b> 意思相近，overwhelmingly/exceedingly/extremely 更地道，推荐使用。",
                            "word_list": "very",
                            "rank": 0
                        }
                    ]
                }
            ],
            "deviation": {
                "status": "failure",
                "reason": "Not providing the right parameter"
            },
            "meta_data": {
                "attach_question_id": "4512",
                "attach_user_id": "337659",
                "scope": "storage_result",
                "unique_id": "test"
            },
            "key": "PG1_emoapp_21bfb2135c9092dd9bb5e40e538bd7f5"
        }
    }
}
```
