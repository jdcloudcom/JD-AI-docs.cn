# 人脸口罩识别

## 一、接口描述

### 1. 功能描述
> 基于业界领先的深度学习技术，利用人脸识别技术针对当下疫情防控，检测人群中是否有未戴口罩着，大大减少人工防疫成本，且准确度高于业界领先水平。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 接口数据要求：
> 1. 图片格式：jpg、jpeg、png、bmp
> 2. 图片大小：小于5M

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/mask_detect
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/mask_detect

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）query请求参数

#### （3）body请求参数（二选一）

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
imageUrl | String | 是 | imageUrl=https://img10.360buyimg.com/n1/.....a43.jpg | 完整图片url
imageBase64Str | String | 是 | imageBase64Str=/9j/4AAQSk... | 图片base64编码

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

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status|	int|	0|	参照四、错误码-业务错误码
message|	string|	success|	状态码描述
request_id|	string| cb4f53b8c60e9589445cc4cd895cf5b6|	为方便定位问题的32位uuid
resultData|	array[]| []|	返回检测结果

resultData参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
confidence | float | 0 | 置信度(推荐0.5作为阈值)
location | String | {"x":151,"width":90,"y":72,"heigth":30} | 人脸区域

### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": true,
  "remain": 9992,
  "remainTimes": 9992,
  "remainSeconds": -1,
  "msg": "查询成功,扣费",
  "result": {
    "status": 0,
    "message": "success",
    "request_id": "d41d8cd98f00b204e9800998ecf8427e",
    "resultData": [
      {
        "confidence": 1.0,
        "location": {
          "x": 283.2704772949219,
          "y": 54.19200134277344,
          "width": 36.98736572265625,
          "heigth": 45.974609375
        }
      },
      {
        "confidence": 0.0,
        "location": {
          "x": 237.12486267089844,
          "y": 59.80866241455078,
          "width": 25.013351440429688,
          "heigth": 31.863121032714844
        }
      }
    ]
  }
}
```

### 3、业务错误码
业务错误码（status）|对应message|说明
------|------|------
12001|"image does not exist"|图像不存在
12002|"image format error"|图像格式错误
12003|"image size error"|图像大小错误
12004|"parameter does not exit"|参数不存在
12005|"parameter value is null"|参数值为null
13002|"time out"|超时
13004|"no face detected"|无人脸检测到
13005|"internel error"|内部错误