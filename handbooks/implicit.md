# 批改网开放接口 JSDK

批改网JSDK提供JavaScript的接口，可轻松将批改作文结果部署到网页中

jsdk是通过jquery的jsonP方式实现跨越获取授权、资源，总体来说需要下面2个步骤：

+ [JSDK：获取授权](#获取授权)
+ [JSDK：获取资源](#获取资源)


######JSDK完整Demo
在看下面步骤前可以先试一试我们的demo
>http://pigai.org/g2016.html


##获取授权

  请参考  [授权流程](../handbooks/workflows.html) ，这边免去“请求用户授权”，而直接通过 client_id（APIKEY） 获取token

>http://api.pigai.org/oauth2/authorize2

######请求方式: get , jsonP
#####请求参数
|参数名称 | 参数说明 |
|---|---|
| client_id | 必须,应用的唯一标识，对应的 APIKey |
| response_type | 必须，必须为token。 |
| callback | 必须，自定义JavaScript函数，建议使用jsonP来做。|
| state | 可选，服务器会把state值原样传回客户端,用于防止csrf攻击 |

#####返回参数

返回的格式为js的callback(jsondata) 函数,其中callback为自定义定义的。

下文为jsondata 返货款参考：


######成功
```json
{
"access_token":"fc21ed0947c99cd8987da173857c89278682d908"
,"expires_in":"7200"
,"token_type":"Bearer"
,"state":"xyz"
}
```
|参数名称 | 参数说明 |
|---|---|
| access_token | 临时token |
| expires_in | 过期时间限制，默认为2个小时。 |
| state | 带过来的state 防止crsf攻击 |

######失败
```json
{
    "error": "原因",
    "error_code": 21329,
    "error_description": "原因描述"
}
```

###DEMO

  >http://api.pigai.org/oauth2/authorize2?callback=myfun&response_type=token&client_id=APIKEY&state=xyz

#####返回

```js
myfun({"access_token":"8d734bf19bc9e7b0dbec5642204e7988a05cc222","expires_in":"7200","token_type":"Bearer","state":"xyz"})
```

#####JsonP的实例

```js
$.ajax({
	   url: 'http://api.pigai.org/oauth2/authorize2',
	   type: 'get',
	   data: {
		response_type: 'token',
		client_id: '提供APIKEY',
		state: 'xyz'
	   },
	   dataType: 'jsonp'
	}).done(function(d) {
		alert( d.access_token );
		console.log(d.access_token);
	});
```

##获取资源

>http://api.pigai.org/essays/rapid_experience

######请求方式: GET,jsonP
#####请求参数
| 参数名称 | 参数说明 |
| :--: | :--: |
| access_token | 第一个步骤获取的token |
| title | 作文标题 |
| comcontext | 作文内容 |
| tpl | 输出格式，固定值all_json、html_json |
| callback | 必须，自定义JavaScript函数，建议使用jsonP。|

#####返回参数说明

返回的数据格式，可遵循[资源列表](../handbooks/resource.html)的返回格式，如果成功数据都在 data中，data中数据根据 tpl的值 'all_json'、'html_json' 提供2中返回数据

#####JsonP的实例

```js
$.ajax({
	   url: 'http://api.pigai.org/essays/rapid_experience',
	   data: {
		access_token: 'token',
		title: 'title',
		comcontext: 'English is a internationaly language which becomes importantly for modern world. ',
		tpl: 'all_json' // 或者可用 html_json
	   },
		   dataType: 'jsonp'
		}).done(function(rep) {

		});

```

######tpl为'all_json'的

```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
        "score": 40.5,
        "score_cat": {
            "1": {
                "name": "词汇",
                "tip": "",
                "score": 0.442630385488
            },
            "2": {
                "name": "句子",
                "tip": "",
                "score": 0.477608817276
            },
            "3": {
                "name": "篇章结构",
                "tip": "",
                "score": 0.413793103448
            },
            "4": {
                "name": "内容相关",
                "tip": "",
                "score": 0.3
            }
        },
        "comment": "采用了简单的衔接手法，行文流畅；多多加强句法知识；文章用词太过单一，且单词拼写错误较多。",
        "sentences": [
            {
                "sid": 0,
                "pid": 1,
                "text": "English is a internationaly language which becomes importantly for modern world.",
                "comment": [
                    {
                        "class": "error",
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
        ]
    }
}
```

######tpl为'html_json'返回格式

```json
{
    "error": "success",
    "error_code": 0,
    "error_description": "success",
    "data": {
        "score": 68,
        "score_cat": " ....",
        "sentences": "..."
    }
}
```





