# 特定人物识别

## 一、接口描述 
### 1. 功能描述  
  特定人物识别主要用于对传入的图片中所有人脸进行分析，判断是否为特定审核人物。
### 2. 能力说明：  
  目前可支持国内外政要人物，也可以支持明星演员，运动员，名人等公众人物或进行自定义人物审核库，根据自己的业务进行配置人物的审核策略。
### 3. 接口数据要求：  
> 1. 图片格式：支持jpeg/jpg、png
> 2. 图片像素：最小 48 \* 48 像素，最大 4096 \* 4096 像素
> 3. 图片大小：小于2MB

### 4. 接口使用：  

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。


在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明
### 1. 接口地址 ：

```
http://aiapi.jdcloud.com/jdai/PoliticiansRecognition
```

### 2. 请求方式：  
https  `post`aiapi.jdcloud.com/jdai/PoliticiansRecognition
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
无 | Binary | 是 | 略 | 图片文件的二进制流

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

result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status|	int|	0|	参见[错误码](Error-Code.md)-业务级错误码
message|	string|	"Success."|	参见[错误码](Error-Code.md)-业务级错误码
request_id| string| "hJe+Bn3QhgfE2BKQ/HsD5g=="| 请求id
name|	string|	"金正恩"|	检出的人物姓名，若为空值，则未检出

### 2、返回示例    
```
    {
        "status": 0,
        "message": "Success.",
        "request_id": "hJe+Bn3QhgfE2BKQ/HsD5g==",
        "name": "金正恩"
    }
```

