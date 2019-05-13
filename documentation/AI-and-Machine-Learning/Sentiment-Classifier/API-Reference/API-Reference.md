# 情感分析

## 一、接口描述 

### 1. 功能描述
判断输入的文本的情感极性类别。

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。


在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。


## 二、类型1-sentiment

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/sentiment
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/sentiment

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Content-Type | string | 是 | application/json | 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
type | int | 是 | 1 | 情感模型的类型：<br>1: 针对通用场景的评论短语文本，情感极性类别为正负中三维<br/>positive, negative, other<br/>3: 针对客服对话场景的短语文本，情感极性类别为七维<br/>other, anxiety, anger, happy, lost, sad, fear<br/>5: 针对客服对话场景的短语文本，情感极性类别为八维<br/>other, anxiety, anger, happy, lost, sad, fear, satiric<br/>
text | string | 是 | 我的为什么是这样？这是买对了吧？<br/>我是在京东搜索然后下单的，没买错吧？ | 输入文本

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

### 5、返回参数
#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


#### （2）业务返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status | int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | ok | 参见[错误码](Error-Code.md)-业务级错误码
request_id | string | 5893465d31284468a8014de6ee430f8e | 便于双方定位问题
sentiment | list |  [{"sentiment": "other",<br/>"probability": 0.5814915299415588},...]  | 情感分析结果，包括情感名称和概率，<br/>按照概率从大到小排列，详情见sentiment字段说明


#### sentiment字段说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
sentiment | string | positive | 情感名称
probability | double | 0.05233341082930565 | 情感概率

### 6、返回示例    

```
{
    "code": "10000",
    "charge": false,
    "remain": 7943,
    "msg": "查询成功",
    "result": {
        "status": 0,
        "request_id": "7b52458a-5479-4ef1-a5da-434a2ed577f9",
        "message": "ok",
        "sentiment": [
            {
                "sentiment": "other",
                "probability": 0.5814915299415588
            },
            {
                "sentiment": "negative",
                "probability": 0.29118022322654724
            },
            {
                "sentiment": "positive",
                "probability": 0.12732817232608795
            }
        ]
    }
}
```


## 三、类型2-sentimentV2

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/sentimentV2
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/sentimentV2

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Content-Type | string | 是 | application/json | 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名


#### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
type | int | 是 | 3 | 情感模型的类型：<br>  positive, negative, other<br/>3: 针对客服对话场景的短语文本，情感极性类别为七维<br/>other, anxiety, anger, happy, lost, sad, fear<br/>5: 针对客服对话场景的短语文本，情感极性类别为八维<br/>other, anxiety, anger, happy, lost, sad, fear, satiric<br/>
text | string | 是 | 周三了，怎么还没有到货啊 | 输入文本

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见本页一接口描述中的2接口使用

### 5、返回参数
#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status | int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | ok | 参见[错误码](Error-Code.md)-业务级错误码
request_id | string | 5893465d31284468a8014de6ee430f8e | 便于双方定位问题
sentiment | list |  [{"sentiment": "other","levelList": [],"probability": 0.8068467378616333,"optional": {}},...] | 情感分析结果，包括情感名称和概率，<br/>按照概率从大到小排列，详情见sentiment字段说明


#### sentiment字段说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
sentiment | string | positive | 情感名称
levelList | list | [{"probability": 0.9996317625045776,"degree": 2},...] | 情感浓度，四个类别：high，medium，low，other，<br>按照浓度值从高到低排列，详情见levelList字段说明<br>目前只有情感分类的分值最高的是生气或者焦虑的时候，<br/>才返回levelList，其他情绪分类levelList为空<br/>
probability | double | 0.0756475105881691 | 情感概率
optional | map |  | 拓展字段，暂时未使用


#### levelList字段说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
degree | int | 1 | 浓度类别，3----high，2----medium，1----low，0----other
probability | double | 0 | 浓度值


 
### 6、返回示例    

```
{
    "code": "10000",
    "charge": false,
    "remain": 139,
    "msg": "查询成功",
    "result": {
        "status": 0,
        "request_id": "cc729697-b47b-41a7-9750-c865b7830b5a",
        "message": "ok",
        "sentiment": [
            {
                "sentiment": "anxiety",
                "levelList": [
                    {
                        "probability": 0.9996317625045776,
                        "degree": 2
                    },
                    {
                        "probability": 0.00022687739692628384,
                        "degree": 1
                    },
                    {
                        "probability": 0.00011544523295015097,
                        "degree": 3
                    },
                    {
                        "probability": 0.00010048089461633936,
                        "degree": 0
                    }
                ],
                "probability": 0.46904614567756653,
                "optional": {}
            },
            {
                "sentiment": "lost",
                "levelList": [],
                "probability": 0.0005221770261414349,
                "optional": {}
            },
            {
                "sentiment": "other",
                "levelList": [],
                "probability": 0.0002466812147758901,
                "optional": {}
            },
            {
                "sentiment": "anger",
                "levelList": [
                    {
                        "probability": 1,
                        "degree": 0
                    },
                    {
                        "probability": 0,
                        "degree": 1
                    },
                    {
                        "probability": 0,
                        "degree": 2
                    },
                    {
                        "probability": 0,
                        "degree": 3
                    }
                ],
                "probability": 0.00002687030973902438,
                "optional": {}
            },
            {
                "sentiment": "fear",
                "levelList": [],
                "probability": 0.000003612826958487858,
                "optional": {}
            },
            {
                "sentiment": "sad",
                "levelList": [],
                "probability": 6.862741201985045e-7,
                "optional": {}
            },
            {
                "sentiment": "happy",
                "levelList": [],
                "probability": 9.415043855653948e-9,
                "optional": {}
            }
        ]
    }
}
```


## 四、类型3-sentimentSeries

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/sentimentSeries
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/sentimentSeries

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Content-Type | string | 是 | application/json | 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
type | string | 是 | 0 | 情感模型的类型：0:<br> 一段会话中情感状态的变化，分为三类，turn_good（情绪好转），<br>turn_bad（情绪恶化）和keep_smooth（情绪平稳）<br/>
texts | List&lt;string&gt; | 是 | ["货还没送到",<br/>"货还没收到",<br/>"他妈这个厂家真不是人来的",<br/>"还是纠纷那个单",<br/>"都投诉N次了",<br/>"都仲裁N次了，没结果"<br/>]| 输入文本，这是一段会话的若干个文本，<br/>ist里的每一个元素为单次的会话文本


### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见本页一接口描述中的2接口使用

### 5、返回参数
#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


#### （2）业务返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status | int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | ok | 参见[错误码](Error-Code.md)-业务级错误码
request_id | string | 5893465d31284468a8014de6ee430f8e | 便于双方定位问题
sentiment | list |  [{"sentiment": "turn_bad","probability": 0},...]  | 情感分析结果，详情见sentiment字段说明

#### sentiment字段说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
sentiment | string | turn_bad | 情感变化
probability | double | 0 | 情感概率
 
### 6、返回示例    

```
{
    "code": "10000",
    "charge": false,
    "remain": 7941,
    "msg": "查询成功",
    "result": {
        "status": 0,
        "request_id": "1be54229-a51e-4ad0-8bda-ce9a68b3e94d",
        "message": "ok",
        "sentiment": [
            {
                "sentiment": "turn_bad",
                "probability": 0
            }
        ]
    }
}
```



