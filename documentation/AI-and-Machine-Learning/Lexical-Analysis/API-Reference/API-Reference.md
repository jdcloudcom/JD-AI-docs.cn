# 词法分析

## 一、接口描述 

### 1. 功能描述
提供中文分词、词性标注、命名实体识别三个功能，解析自然语言中的基本语言元素，并赋予词性，进一步将文本中的特定类型的事物名称或符号识别出来，使机器能更准确的理解内容，支撑自然语言的准确理解。

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。


## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/lexer
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/lexer

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
appId | string | 否 | 0 | 应用id，同一调用方可以创建多个应用。appId不填或者为0时表示使用通用的分词模型。
text | string | 是 | 克林顿访问中国 | 输入文本
type | int | 是 | 0 | 选择所需的词法分析的结果，包括"分词"、"词性标注"和"命名实体识别”一个或多个的组合。<br>0: 提供分词，词性标注以及命名实体识别的结果<br/>1: 提供分词的结果<br/>2: 提供分词和词性标注的结果<br/>3: 提供分词和命名实体的结果<br/>如输入其它数值，默认按0情况处理

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


## 三、返回说明
### 1、返回参数
   
#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


#### （2）业务返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
status | int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | ok | 参见[错误码](Error-Code.md)-业务级错误码
request_id | string | 5893465d31284468a8014de6ee430f8e | 便于双方定位问题
text | string | 克林顿访问中国 | 输入文本
tokenizedText | list |  [{"offset": 0,"pos": "NR","length": 3,"ner": "PERSON","word": "克林顿"},...]  | 词法分析结果，详情下面tokenizedText字段说明


#### tokenizedText字段说明

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
word | string | 克林顿 | 分词
pos | string | NR | 词性
ner | string | PERSON | 命名实体识别
offset | int | 0 | 距离起始位置偏移
length | int | 3 | 分词长度


### 2、返回示例    

```
{
    "code": "10000",
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
    "result": {
        "status": 0,
        "request_id": "ac7be2c2-c5c6-4bd4-b52d-e03b03fc5b58",
        "message": "ok",
        "text": "克林顿访问中国",
        "tokenizedText": [
            {
                "offset": 0,
                "pos": "NR",
                "length": 3,
                "ner": "PERSON",
                "word": "克林顿"
            },
            {
                "offset": 3,
                "pos": "VV",
                "length": 2,
                "ner": "O",
                "word": "访问"
            },
            {
                "offset": 5,
                "pos": "NR",
                "length": 2,
                "ner": "GPE",
                "word": "中国"
            }
        ]
    }
}
```
