# 银行卡识别

## 一、接口描述 

### 1. 功能描述  

  基于业界领先的深度学习技术，利用光学字符识别技术，将图片上的文字转换为可编辑的文本，为您提供场景丰富的整图文字检测和识别服务。
  
### 2. 接口数据要求：  
> 1. 图片格式：jpg(jpeg)、png
> 2. 图片大小：小于5M 
> 3. 目前只支持横卡，暂不支持竖卡。

### 4. 接口使用：  
公测期间用户可以免费（0元）进行测试，根据[购买流程](http://neuhub.jd.com/ai/api/ocr/bankcard)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](https://aidoc.jd.com/user/auth.html)规则进行相应开发，整体流程详见   [接入流程](https://aidoc.jd.com/user/flow.html)  。

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/ocr_bankcard
```
### 2. 请求方式：  
https  `post`aiapi.jdcloud.com/jdai/ocr_bankcard
### 3. 请求参数    

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Content-Type | String | 是 | application/octet-stream | 标准编码格式
Authorization | String | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
无 | binary | 是 | 无 | 图片内容，传入图片

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](未发布)

## 三、返回说明
### 1、返回参数
#### （1）公共返回参数  

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1001 | 参见下方错误码-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见下方错误码-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code|	string|	0|	参照四、错误码-业务错误码
message|	string|	success|	状态码描述
request_id|	string|	cb4f53b8c60e9589445cc4cd895cf5b6|	为方便定位问题的32位uuid
result|	json|	{...}|	返回识别结果

result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
bank_name|string|邮政银行北京分行|银行名称
bank_number|string|6221881000046221446|银行卡号
card_count|string|19|卡号位数
card_name|string|绿卡银联标准卡|卡名称
card_type|string|储蓄卡|卡类型

### 2、返回示例   


```
{
    "code": 0,
    "message": "success",
    "request_id": "815774d6ed6ca43e5d0cce316d36d822",
    "result": {
        "bank_name": "邮政银行北京分行",
        "bank_number": "6221881000046221446",
        "card_count": "19",
        "card_name": "绿卡银联标准卡",
        "card_type": "储蓄卡"
    }
}

```

