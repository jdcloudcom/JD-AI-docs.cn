# 增值税发票识别

## 一、接口描述 

### 1. 功能描述  

基于业界领先的深度学习技术，利用光学字符识别技术，将图片上的文字转换为可编辑的文本，为您提供场景丰富的整图文字检测和识别服务。
  
### 2. 接口数据要求：  
> 1. 图片格式：jpg(jpeg)、png、jijf
> 2. 图片大小：小于5M 

### 4. 接口使用：  

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。


在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/ocr_invoice
```
### 2. 请求方式：  
https  `post`aiapi.jdcloud.com/jdai/ocr_invoice
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
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

## 三、返回说明
### 1、返回参数
#### （1）公共返回参数  

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1001 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code|	string|	0|	参见[错误码](Error-Code.md)-业务级错误码
message|	string|	success|	状态码描述，参见[错误码](Error-Code.md)-业务级错误码
request_id|	string|	cb4f53b8c60e9589445cc4cd895cf5b6|	为方便定位问题的32位uuid
result|	json|	{...}|	返回识别结果

result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
buyer_name|string|华电虎林凤力发电有限公司|购买方名称
buyer_tax_no|string|372569065123562|购买方税号
code|string|3700081650|发票代码
invoice_amount|string|2324.79|发票金额
invoice_date|string|20090424|开票日期
invoice_no|string|01599485|发票号码
invoice_type|string|04|发票类型
saler_name|string|山东阳谷振璃工艺制品司|销售方名称
saler_tax_no|string|372522168018036|销售方税号
tax_amount|string|13675.21|发票税额
total_amount|string|16000.00|价格合计
verify_code|string|44095028783173850994|校验码

### 2、返回示例   


```
{
    "code": 0,
    "message": "success",
    "request_id": "815774d6ed6ca43e5d0cce316d36d822",
    "result": {
        "buyer_name": "华电虎林凤力发电有限公司",
        "buyer_tax_no": "372569065123562",
        "code": "3700081650",
        "invoice_amount": "2324.79",
        "invoice_date": "20090424",
        "invoice_no": "01599485",
        "invoice_type": "04",
        "saler_name": "山东阳谷振璃工艺制品司",
        "saler_tax_no": "372522168018036",
        "tax_amount": "13675.21",
        "total_amount": "16000.00",
        "verify_code": "44095028783173850994"
    }
}

```

