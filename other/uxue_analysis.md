# u学统计分析
## 接口列表
+ [TOP10错误](#错误排行榜)
+ [根据指定qid和错误类型，获取句子和句评](#根据指定qid和错误类型，获取句子和句评)
+ [获取指定qid对应的各词性个数](#获取指定qid对应的各词性个数)
+ [获取指定qid对应词性的top200个单词](获取指定qid对应词性的top200个单词)
+ [获取分数分布](#获取分数分布)
### 错误排行榜
API: `http://api.pigai.org/analysis/uxue_top_error?qid=3834&access_token=xxx`

######请求参数(GET)

| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| qid | 必须，作文id |

###返回结果
######成功

```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
        "qid": 3834,
        "top_error": [
            {
                "name": "标点符号",
                "type": "spell/punct",
                "total": 3682
            },
            {
                "name": "拼写",
                "type": "spell/spell",
                "total": 1395
            },
            {
                "name": "主谓一致",
                "type": "snt/nvagree",
                "total": 946
            },
            {
                "name": "其它搭配",
                "type": "trp/others",
                "total": 876
            },
            {
                "name": "大小写",
                "type": "spell/case",
                "total": 742
            },
            {
                "name": "冠词",
                "type": "word/art",
                "total": 704
            },
            {
                "name": "连词",
                "type": "word/conj",
                "total": 527
            },
            {
                "name": "成分缺失",
                "type": "snt/incomplete",
                "total": 407
            },
            {
                "name": "动宾搭配",
                "type": "trp/von",
                "total": 259
            },
            {
                "name": "其它不规范",
                "type": "snt/others",
                "total": 250
            }
        ]
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

### 根据指定qid和错误类型，获取句子和句评
API: `http://api.pigai.org/analysis/uxue_error?qid=3834&type=spell/punct&access_token==xxx`

######请求参数(GET)

| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| qid | 必须，作文id |
| type | 必须，错误分类 (查看 [错误说明](#错误说明))|

###返回结果
######成功

```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
        "qid": 3834,
        "sentences": [
            {
                "uid": "314625",
                "text": "The+south+most+grow+paddy+in+China.People+always+eat+rice+as+staple+food%2CBut+the+most+of+the+north+China+can+not+plant+paddy+because+of+too+cold+or+too+dry.The+main+crop+is+wheat+in+that%2C",
                "comment": [
                    {
                        "name": "标点符号",
                        "type": "spell/punct",
                        "msg": "疑似标点符号缺失。"
                    }
                ]
            },
            {
                "uid": "313772",
                "text": "The majority of people in the south China grow rice,who usually feeding rice as their staple food.",
                "comment": [
                    {
                        "name": "标点符号",
                        "type": "spell/punct",
                        "msg": "英文标点符号之后通常须加空格。"
                    }
                ]
            },
            {
                ... ...
            },
            {
                "uid": "317039",
                "text": "A lot of parts in SouthChina plant ,people always eat mice.",
                "comment": [
                    {
                        "name": "标点符号",
                        "type": "spell/punct",
                        "msg": "英文标点符号之前无须空格。"
                    }
                ]
            }
        ]
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

## 错误说明
![](/asserts/err_cate.png)



### 获取指定qid对应的各词性个数
API: `http://api.pigai.org/analysis/uxue_word_sum?qid=3834&access_token==xxx`

######请求参数(GET)

| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| qid | 必须，作文id |

###返回结果
######成功

```json
{
	error: "success",
	error_code: 0,
	error_description: "success",
	data: {
		qid: 3834,
		category: [
			{
				key: "n",
				sum: 37592
			},
			{
				key: "a",
				sum: 24853
			},
			{
				key: "p",
				sum: 19053
			},
			{
				key: "pu",
				sum: 15412
			},
			{
				key: "v",
				sum: 15411
			},
			{
				key: "d",
				sum: 14440
			},
			{
				key: "c",
				sum: 5562
			},
			{
				key: "r",
				sum: 2165
			},
			{
				key: "md",
				sum: 1690
			}
		]
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


#####词性简称说明
| 词性简称 | 词性 |
|---|---|
| n | 名词 |
| a | 形容词 |
| p | 介词 |
| v | 动词 |
| d | 副词 |
| c | 连词 |
| r | 代词 |
| md | 情态动词 |
| pu | 标点 |


### 获取指定qid对应词性的top200个单词
API: `http://api.pigai.org/analysis/uxue_word_top?qid=3834&cate=n&access_token==xxx`

######请求参数(GET)

| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| qid | 必须，作文id |
| cate | 必须，词性简称(见表-词性简称说明) |

###返回结果
######成功

```json
{
	error: "success",
	error_code: 0,
	error_description: "success",
	data: {
		qid: 3834,
		ret: [
			{
				key: "rice",
				doc_count: 4923
			},
			{
				key: "china",
				doc_count: 4709
			},
			{
				key: "people",
				doc_count: 3282
			},

			...

		]
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


#####词性简称说明
| 词性简称 | 词性 |
|---|---|
| n | 名词 |
| a | 形容词 |
| p | 介词 |
| v | 动词 |
| d | 副词 |
| c | 连词 |
| r | 代词 |
| md | 情态动词 |
| pu | 标点 |


### 获取分数分布
API: `http://api.pigai.org/analysis/uxue_score_range?qid=3834&type=1&access_token==xxx`

######请求参数(GET)

| 参数名称 | 参数说明 |
|---|---|
| access_token | 必须，这个token如何获取是通过[授权流程](../handbooks/workflows.html)得到这个token |
| qid | 必须，作文id |
| type | 必须，1：翻译；2：作文 |

###返回结果
######成功

```json
{
	error: "success",
	error_code: 0,
	error_description: "success",
	data: {
		qid: 3834,
		ret: [
			{
				range: "*-60.0",
				count: 3140
			},
			{
				range: "60.0-69.0",
				count: 47
			},
			{
				range: "70.0-79.0",
				count: 15
			},
			{
				range: "80.0-89.0",
				count: 1
			},
			{
				range: "90.0-100.0",
				count: 0
			}
		]
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

