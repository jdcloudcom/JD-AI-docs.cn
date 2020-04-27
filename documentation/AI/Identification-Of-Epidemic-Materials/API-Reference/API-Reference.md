# 疫情物资识别

## 一、接口描述

### 1. 功能描述
> 本接口能够识别图片中的医疗防疫物资，包括口罩、手套、防护服、护目镜、额温枪、防护面屏、消毒产品等。支持返回识别物品的一级类目和二级类目，以及型号、执行标准等额外信息。

### 2. 接口使用

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 2. 能力说明

本接口基于图片检测、分类、特征表示能力，以及商品识别和OCR能力，提供图片中医疗物资商品的检测与识别能力，识别结果能够达到二级分类粒度，并支持物资信号、规格、执行标准等额外信息识别。

### 3. 数据要求

> * 图片格式：图片Base64编码
> * 图片像素：最小 201 \* 201
> * 图片类型：jpg, jpeg, png

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/medical_material_recognize
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/medical_material_recognize

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | text/plain | 标准编码格式
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）query请求参数

#### （3）body请求参数

业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
image_content | string | 是 | 【略】 | 图片的Base64编码

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
code| int | 0 | 参照业务错误码
message | string | "SUCCESS" | 参照业务错误信息
category1 | string | "口罩" | 识别物资的一级类目
category2 | string | "医用防护口罩" | 识别物资的二级类目
is_medical | int | 0 |  0非医用，1可医用，2可医用(待检），3无医用区分
spec_no | string | "N95" | 规格型号
extra_info | array | ["防护"] | 额外信息

### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": false,
  "remainTimes": 4998,
  "remainSeconds": -1,
  "msg": "查询成功",
  "result": {
    "code":0,
    "category1":"口罩",
    "category2":"医用防护口罩",
    "message":"SUCCESS",
    "extra_info":["防护","外科"],
    "is_medical":1,
    "spec_no":"R95"
  }
}
```

### 3、业务错误码
业务错误码（status）| 对应message | 说明
------|------|------
2005 | "IMAGE_TOO_SMALL" | 图片过小
2006 | "BROKEN_BASE64_OR_URL" | 无效的base64或url
3014 | "INVALID_IMAGE_CONTENT" | 不合法的图片
3031 | "SEARCH_PRODUCT_IMAGE_ERROR" | 查询商品图片异常
3054 | "NOT_SUPPORT_IMAGE" | 不支持的图片格式
5000 | "INTERNAL_SERVER_ERROR" | 内部服务错误
5001 | "INVALID_PARAMETER_JSON" | 非法的JSON参数格式
6001 | "OCR_API_ERROR" | OCR接口调用错误
6002 | "MPR_API_ERROR" | MPR接口调用错误