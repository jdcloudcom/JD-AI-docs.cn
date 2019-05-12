# 文本分类



## 一、接口描述 
### 1. 功能描述  
识别用户话术的领域信息，当前版本在13个领域上进行分类：歌曲、广播、故事、百科、天气、时间、新闻、生活查询、岀行、股票、购物、音箱指令、家居指令、闲聊、翻译、计算机、闹钟。

types | 0 | 1 | 2 | 3 | 4 | 5 | 6
------|-----|-----|-----|-----|-----|-----|-----
domain name | other | calcu | chat | info | instruct | local | news

types | 7 | 8 | 9 | 10 | 11 | 12
------|-----|-----|-----|-----|-----|-----
domain name | radio | reject | song | story | weather | shopping

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)。


## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/textClassification
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/textClassification

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
text | string | 是 | 克林顿访问中国 | 输入文本

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

## 三、返回说明
### 1、返回参数
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
types | list |  [{"type": 3, "probability": 0.727774441242218, "domainName": "info"},,...]  | 文本分类结果，详情下面types字段说明

#### types字段说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
type | int | 3 | 分类序号
probability | double | 0.727774441242218 | 分类概率
domainName | string | info | 分类名称

### 2、返回示例

```
{
    "code": "10000",
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
    "result": {
                "status": 0,
                "request_id": xxx,
                "message": "ok",
                "types": [
                  {
                    "type": 3,
                    "probability": 0.727774441242218,
                    "domainName": "info"
                  },
                  {
                    "type": 8,
                    "probability": 0.2294873297214508,
                    "domainName": "reject"
                  },
                  {
                    "type": 9,
                    "probability": 0.042706381529569626,
                    "domainName": "song"
                  }
                ]
              }
}
```
