# 菜品识别

## 一、接口描述 
### 1. 功能描述  
菜品识别（food classification）API为用户提供菜品识别功能，输入一张菜品图片，返回识别结果。

### 2. 能力说明：   
输入图像限定为菜品图像，不能提供其他类别图像的识别能力。

### 3. 接口数据要求：  
- 图片格式：base64编码
- 图片类型：JPEG,BMP,PNG,GIF
- 图片像素尺寸：最小 50\*50 像素，最大 2048\*2048 像素
- 图片文件大小：小于2M

### 4. 接口使用： 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

使用接口前，需要先完成API的下单购买，然后可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/FoodApi
```

### 2. 请求方式：  
https `post` aiapi.jdcloud.com/jdai/FoodApi

### 3. 请求参数 
#### （1）header请求参数
业务请求参数
 
名称 | 类型 | 必填 | 示例值 | 描述 
------|-----|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名 


#### （2）body请求参数
业务请求参数
 
名称 | 类型 | 必填 | 示例值 | 描述 
------|-----|-----|-----|-----
image | string | 是 | {"image":"4AAQSk..."} | 图像base64编码 


### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


## 三、返回说明
### 1、返回参数

#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述 
------|-----|-----|-----
code | string | 10000 | 参见[错误码](Error-Code.md)-系统级错误码 
charge | boolean | false 或 true | false：不扣费， true：扣费 
remain | long | 1305 | 按天计算剩余调用次数 
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果 

#### （2）业务返回参数
 
名称 | 类型 | 示例值 | 描述 
------|-----|-----|-----
status | int | 1000 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | OK | 参见[错误码](Error-Code.md)-业务级错误码
result | string | 红烧肉 | 返回菜品识别结果 
used_time | int | 606 | 整个请求花费的时间，单位为毫秒 

### 2、返回示例  

```
{
    "code": "10000",
    "charge": false,
    "remain": 0,
    "msg": "查询成功",
    "result": {
        "message":"ok ",
        "status": 1000,
        "used_time": 606 
        "result": "红烧肉"
    }
}
```
