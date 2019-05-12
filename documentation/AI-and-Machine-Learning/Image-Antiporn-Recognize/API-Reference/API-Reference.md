# 智能鉴黄 

## 一、接口描述 
  
### 1.功能描述 

基于业界领先的深度学习图像识别技术，对图片影像的肤色、姿态和场景等进行智能识别
，准确快速的输出每张图片“色情”、"低俗”、“性感”、“正常”的概率，其中色情图片准确
率高达 99.95%，有效的规避涉黄风险，让您的内容轻松过审核，成倍的解放审核人力！

### 2.接口数据要求
> 1. 图片格式：jpg/jpeg、png
> 2. 图片文件大小：小于2M


### 3.接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明 

### 1. 接口地址

```
https://aiapi.jdcloud.com/jdai/localCvImage
```

### 2. 请求方式
https `post` aiapi.jdcloud.com/jdai/localCvImage

### 3. 请求参数
#### （1）header请求参数

名称 | 类型 | 必填 | 示例值	| 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/octet-stream ,text/plain ...| 二进制流，文件类型..
Authorization | String | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数

名称 | 类型 | 必填 | 示例值	| 描述
------|------|-----|-----|-----
 无 | ByteArrayRequestEntity| 是 | 略 | 图片二进制流

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

## 三、返回说明 ##
### 1.公共返回参数 ###
名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

### 2.业务返回参数 ###

result参数信息

名称 | 类型 | 必填 | 示例值	| 描述
------|------|-----|-----|-----
status | int | 是 | 0	 | 状态码，参见[错误码](Error-Code.md)-业务级错误码
message | String | 是 | 正常 |  具体消息，参见[错误码](Error-Code.md)-业务级错误码
request_id | String | 是 | 03ac182a-03e1-4802-840b-a33bd985619d	 | 请求id
sexyScore | double | 是 | 0.2877 | 性感分数
pornScore | double | 是 | 0.2183 | 成人分数
vulgarScore | double | 是 | 0.1532 | 低俗分数
normalScore | double | 是 | 0.3409 | 正常分数

### 3.返回实例 ###
```
{
    "code":"10000",
    "charge":false,
    "remain":0,
    "msg":"查询成功",
    "result":{
        "status":0,
        "message":"ok",
        "request_id":"46e78874-3491-4a30-834e-98c0d76a1800",
        "sexyScore":0.2877,
        "pornScore":0.2183,
        "vulgarScore":0.1532,
        "normalScore":0.3409
    }
}
```






