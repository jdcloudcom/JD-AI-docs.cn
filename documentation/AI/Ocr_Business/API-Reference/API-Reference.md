# 营业执照识别

## 一、接口描述

### 1. 功能描述
> 识别营业执照的关键字段，包括企业名称、法定代表人、经营场所、经营期限、社会信用代码等

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 图片要求

> 1. 图片格式：jpg/jpeg/png/jfif/bmp
> 2. 图片大小：小于5M

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/ocr_business
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/ocr_business

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名
Content-Type | String | 是 | application/octet-stream | 标准编码格式

#### （2）query请求参数

#### （3）body请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
无 | binary | 是 | 无 | 图片内容，传入图片

### 4. 请求代码示例
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
服务器返回的识别结果采用 JSON 格式：

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code|	int|	0|	参照四、错误码-业务错误码
message|	string|	success|	状态码描述
request_id|	string|	cb4f53b8c60e9589445cc4cd895cf5b6|	为方便定位问题的32位uuid
resultData|	object|	{...}|	返回识别结果

resultData参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | String | 91510107MA61TTCA4E | 社会信用代码
name | String | 成都天润文化传媒有限公司 | 企业名称
valid_time | String | 2016年3月15日至永久 | 经营期限
address | String | 成都市武侯区科华北路43号附4号 | 经营场所
owner | String | 王全伟 | 法定代表人
registration_time | String | 2016年3月15日 | 注册时间
money | String | (人民币)壹佰万元 | 注册资金
business_type | String | 有限责任公司(自然人投资或控股) |  	企业类型
composition | String | xxx | 组成形式
registration_code | String | 32062319960622626X | 注册号

### 2、返回示例

```JSON
{
    "code":1000,
    "charge":false,
    "remainTimes": 4998,
    "remainSeconds": -1,
    "msg":"查询成功",
    "result":{
         "code": 0,
         "resultData": {
             "owner": "王全伟",
             "code": "91510107MA61TTCA4E",
             "address": "成都市武侯区科华北路43号附4号",
             "money": "(人民币)壹佰万元",
             "registration_code": "",
             "composition": "",
             "business_type": "有限责任公司(自然人投资或控股)",
             "name": "成都天润文化传媒有限公司",
             "valid_time": "2016年3月15日至永久",
             "registration_time": "2016年3月15日"
         },
         "message": "success",
         "request_id": "9d93622c17b2b7bee57aa46a148bac2b"
    }
}
```

### 3、业务错误码
业务错误码（code）|对应message|说明
------|------|------
12001|"image does not exist"|图像不存在
12002|"image format error"|图像格式错误
12003|"image size error"|图像大小错误
13004|"no content recognition"|无内容识别
13005|"system error"|系统错误