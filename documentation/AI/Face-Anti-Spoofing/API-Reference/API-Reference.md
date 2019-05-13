#人脸活体检测

## 一、接口描述 

### 1.功能描述

人脸活体检测API主要用于针对用户上传图像，返回该图像中的人脸是否为真人

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。


使用接口前，需要先完成API的下单购买，然后可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3.图片要求

> 1. 图片格式：bmp, jpg, jpeg, png, jfif
> 2. 图片像素尺寸：最小 48\*48 像素，最大 4096\*4096 像素
> 3. 图片文件大小：小于2mb

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/face_AntiSpoof
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/face_AntiSpoof

### 3. 请求参数  


#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名


#### （2）body请求参数
业务请求参数
```
imageBase64=xxxx
```
其中参数定义

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
imageBase64 | string | 是 | 图像Base64编码值，由于过长，不给出示例 | 图片Base64编码


### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)
 
## 返回说明

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
status | int | 0 | 返回结果，0表示成功；非0为对应错误，参见[错误码](Error-Code.md)-业务级错误码
request_id | string | 5893465d31284468a8014de6ee430f8e | 便于双方定位问题
message | string | Success | 错误信息，参见[错误码](Error-Code.md)-业务级错误码
score | float | 0.009 | 假体分数，严格的阈值为0.2，大于0.2为假体，正常的阈值为0.38，大于0.38为假体


### 2、返回示例 

```Json
{
    "code": "10000",
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
    "result": {
      "score":0.009237812383223,
      "status": 0, 
      "message": "success",
      "request_id": "5893465d31284468a8014de6ee430f8e"
    }
}
```
