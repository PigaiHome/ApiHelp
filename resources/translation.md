# 翻译资源

## 句子翻译
> API: http://api.pigai.org/translation/trans_sentence

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
            "cate_score": {
                "1": 85.30076, // 词汇
                "2": 70.73441, // 句子
                "3": 81.8885, // 篇章结构
                "4": 93.32474 // 内容相关
            },
            "pingyu": "文中词汇表达灵活多样请继续保持，高级词汇积累也做的很棒；从句数量偏少；全文结构较为严谨。", // 总评
        },
        "sentences": [ // 逐句分析
            {
                "sid": 0, // 第几句
                "para_id": 1, // 段落, 从1开始
                "text": "Urbanization presents a process that rural people migrate into the cities.",
                "comment": [
                    {
                        "class": "error",
                        "cat": "句子错误",
                        "msg": "本句语法不规范，请检查。",
                    },
                    {
                        "class": "error_trp",
                        "cat": "拓展辨析",
                        "msg": "<b>people</b>表示“人，民族”。查看与<a href=\"http://bbs.pigai.org/forum.php?mod=viewthread&tid=12942&page=1&extra=#pid30263\" target=\"_blank\"><b>person</b></a>的区别。",
                    }
                ]
            },
            {
                "sid": 1,
                "pid": 1,
                "text": "A key index of a nation’s urbanization level is the distribution of its population in urban a nd rural areas.",
                "comment": [
                    {
                        "class": "error_trp",
                        "cat": "学习提示",
                        "msg": "<b>nation</b>表示“国家”。注意与<b>country</b>的区别。<a href=\"http://bbs.pigai.org/forum.php?mod=viewthread&tid=12961&page=1&extra=#pid30320\" target=\"_blank\">详情点击</a>",
                    }
                ]
            },
            {
                "sid": 2,
                "pid": 1,
                "text": "The urbanization rate of China registered over 50% last year, which marks that our country has stepped into a new “city-based society”.",
                "comment": [
                    {
                        "class": "error", # 分为四类: warn 警告，error 错误，error_trp 提示，great 好
                        "cat": "大小写错误",
                        "msg": "确认 <b>city-based</b> 大小写使用正确。",
                    },
                    {
                        "class": "error_trp",
                        "cat": "学习提示",
                        "msg": "易混词汇: <b>new</b>, fresh, novel, original, innovative 均含“新的”之意。",
                    }
                ]
            },
            {
                "sid": 3,
                "pid": 1,
                "text": "Urbanization becomes an importa nt part of our society and economic development.",
                "comment": [
                    {
                        "class": "error",
                        "cat": "词语错误",
                        "msg": "请检查<b>importa</b>，确认拼写正确。",
                    },
                    {
                        "class": "error_trp",
                        "cat": "学习提示",
                        "msg": "易混词汇: <b>development</b>, evolution 都表示“发展，进化”之意。",
                    }
                ]
            },
            {
                "sid": 4,
                "pid": 1,
                "text": "By offering better education and job opportunities to urban citizens, it not only improves people’s living standards, but also it makes their culture colorful.",
                "comment": [
                    {
                        "class": "error_trp",
                        "cat": "拓展辨析",
                        "msg": "动名搭配 <b>improve...standard</b> 在语料库中出现过 <a target=\"_blank\" href=\"corpus/snt/?q=improve standard/von\">193</a> 次",
                    }
                ]
            }
        ],
        "id": "0",
        "score": 77.94199 // 总得分
    }
}
```
