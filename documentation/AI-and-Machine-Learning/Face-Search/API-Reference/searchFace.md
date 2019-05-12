# 人脸搜索

## 一、接口描述 

### 1.功能描述

人脸搜索也称为1：N识别，即在一个已有人脸集合中找出与指定人脸最相似的一张或多张人脸。

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

使用接口前，需要先完成API的下单购买，然后可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3.图片要求

> 1. 图片格式：bmp, jpg, jpeg, png, jfif
> 2. 图片像素尺寸：最小 48\*48 像素，最大 4096\*4096 像素
> 3. 图片文件大小：小于2MB

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/faceSearch
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/faceSearch

### 3. 请求参数  
 
#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）query请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
groupId | string | 否 | 6979e9bd79b944b49e0d6e74079d5098 | 分组Id
groupName | string | 否 | test | 分组名称,若groupId不为空则以groupId作为分组的唯一标识

#### （3）body请求参数
业务请求参数
```
imageBase64=xxxx
```
其中参数定义

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
imageBase64 | string | 是 | 图像Base64编码值，由于过长，不给出示例 | 图片的Base64编码


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
status | int | 0 | 返回结果，0表示成功；非0为对应错误号，参见[错误码](Error-Code.md)-业务级错误码
message | string | Success | 返回错误信息，参见[错误码](Error-Code.md)-业务级错误码
result | string | Success | 返回人脸唯一标识faceId

### 2、返回示例

```Json
{
    "status": 0, 
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
		"result": "
			{\"faceSearchResults\":
				[{\"conf\":0.9999682,
						\"faceID\":
						{\"faceId\":\"771ff9c6668c4a538b7ec514fbffc97f\",\"index\":0,\"outerId\":\"fu2\",\"sim\":1.0},
						\"height\":1006.3228,
						\"left\":575.8482,
						\"top\":594.26544,
						\"width\":769.7747
				}]
			}",
    "requestid": "c34efa5cb8d040b6b641fc3e57404f87",
    "message": "success",
    "status": 0
}
```
